
### 2/10/23
## Initialization
*We went over the initialization step last class (2/8/23)*
````
main(argc,argv)
int argc;
char **argv;
{
    Display *display; 

    Window root, window;
    long fgcolor, bgcolor;

    int screen, pointx, pointy, eventmask = ExposureMask|ButtonPressMask;

    int curx, cury;
    XEvent event;
    XColor exact, apparant;
    XGCValues gcval;
    GC draw, erase;

    if (!(display = XOpenDisplay(NULL))) {
	perror("XOpenDisplay");
	exit(1);
    }
````
# Step 2
* now we need to create the root window
````
    root = RootWindow(display,screen = DefaultScreen(display));

    XAllocNamedColor(display,DefaultColormap(display,screen),
		     FORE,&apparant,&exact);
    fgcolor = apparant.pixel;
    XAllocNamedColor(display,DefaultColormap(display,screen),
		     BACK,&apparant,&exact);
    bgcolor = apparant.pixel;
````
* 0 is also considered the default screen
* Now that the root window is set we need to allocate colors
* Can use different color maps for different screens
* The `&` in front of them is using the address by reference
    * Aparent color is what it gives you
    * Exact color is what you asked for
* *Now* we have the root window object and color object
````
    window = XCreateSimpleWindow(display,root,0,0,400,400,2,fgcolor,bgcolor);
````
* Now, we create a window
* This is the parent root
    * (0,0) is the top corner
    * (400, 400) is the bottom corner
    * 2 is the line width in pixels
* Next we will create the drawn graphics context...
````
    gcval.foreground = fgcolor;
    gcval.background = bgcolor;
    draw = XCreateGC(display,window,GCForeground|GCBackground,&gcval);

    gcval.foreground = bgcolor;
    erase= XCreateGC(display,window,GCForeground|GCBackground,&gcval);
````
* All we want is something that has a different foreground and background than black and white
* `XCreateGC()` draws
* We have built our graphical objects
## Step 3 Register Events and Callbacks
* In this case we don't have any callbacks
* We are setting up an event queue for a particular window
    * We do this using an expose mask: 
    * `int screen, pointx, pointy, eventmask = ExposureMask|ButtonPressMask;`
    
### Step 4 Realize Graphical Objects
````
    XSelectInput(display,window,eventmask);
    XMapWindow(display,window);
````

(Event Mask =        01000000)
+
(Button Press Mask = 00010000) 
= (01010000 = Environtment Mask)
````
    for (;;) {
	XNextEvent(display,&event);
	switch (event.type) {
	  case Expose:
	    XClearWindow(display,window);
	    XDrawLine(display,window,draw,25,25,375,375);    
	    break;
	  case ButtonPress:
	    fprintf(stderr,"point set (%d,%d)\n",event.xbutton.x,
		    event.xbutton.y);
	    if (eventmask & PointerMotionMask) {
		XDrawLine(display,window,erase,pointx,pointy,curx,cury);
		XDrawLine(display,window,draw,pointx,pointy,event.xbutton.x,
			  event.xbutton.y);
		XSelectInput(display,window,eventmask &= ~PointerMotionMask);
	    } else {
		curx = pointx = event.xbutton.x;
		cury = pointy = event.xbutton.y;
		XSelectInput(display,window,eventmask |= PointerMotionMask);
	    }
	    break;
	  case MotionNotify:
	    XDrawLine(display,window,erase,pointx,pointy,curx,cury);
	    XDrawLine(display,window,draw,pointx,pointy,curx = event.xmotion.x,
		      cury = event.xmotion.y);
	    break;
	  default:
	    fprintf(stderr,"Unexpected event: %d\n",event.type);
	}
    }
}
```` 
* Now, we are onto the event loop
    * it is an infinite loop
    * we are taking the event queue and puting it into the variable event
    * then we put it into a switch statement based on the event type
* first event is always an expose event in this case
    * puts it back to state 0, where the only thing left is the background color (everything drawn is erased)
* button press are the only options initially

* We have a test of pointer motion mask
    * note masks are normally in 32, not 8 digits
`Pointer Motion Mask = 00000010`
* when we are doing our check/test we are doing a bitwise OR comparing the Environment Mask and Pointer Motion Mask
is the same as 
* if it is false, we proceed to the else
    * the first time we want to anchor the point and turn on the motion notify event

#### The Math: 
````
x+=6
EnvironmentMask = EnvironmentMask | PointerMotionMask
EnvironmentMask |= PointerMotionMask = 01010010
````
To get the new Environment Mask...
````
    Environment Mask  = 01010010
+
    PointerMotionMask = 00000010
    ----------------------------
                        00000010
````
Now we need to turn the motion notify event off...
````
Environment Mask = Environment Mask & ~PointerMask
````
**||||** *End Proof*