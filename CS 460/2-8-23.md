## Rubber Band Program

## [Rubber Band Source Code Line by Line](https://www.cs.odu.edu/~price/cs460/examples/rubber_band_c.html)
[Display Recording](https://drive.google.com/file/d/1mludqpCn9-cvTa6_JwdZZHMZ5fdHXohX/view?usp=share_link)

[Lecture Walkthrough Recording](https://drive.google.com/file/d/1jGHFOYBqrMVnrQH6L6nTWcy6QqR6VVhj/view?usp=share_link)

1. INITIALIZATION STEP (these are the 5 steps we were talking about for last class)

````
#include < X11/Xlib.h >
#include < stdio.h >

#define FORE "light goldenrod" 
#define BACK "midnight blue"
````
* forground and background colors
* Color is done with RGB and there is a list of known colors like at the top of the program
    * it automatically lists in the numbers for that recognized color (eg. midnight blue)
* colors are graphical objects in the server and must be loaded
    * black and white are the only ones that are preloaded
* `display` ptr is a part of every command because the server has to know what you want it to do when you place a command
* Every window has a parent window *except* the root window (which you can't see)
````
main(argc,argv)
int argc;
char **argv;
{
    Display *display; 
````
* Is a ptr to a server (not the screen)
````
    Window root, window;
    long fgcolor, bgcolor;
````
* Foreground color, background color
````
    int screen, pointx, pointy, eventmask = ExposureMask|ButtonPressMask;
````
* supports multiple screens so they must be specified
    * X windows and open gl allow for 4 different screens

* first is the expose event and mouse button press events
* `|` is a bitwise or
    * button press event = 01000000
    * expose event       = 01010000
    * :. events         == 01010000
````
    int curx, cury;
    XEvent event;
    XColor exact, apparant;
    XGCValues gcval;
    GC draw, erase;
````
* X, GC, and XGC are data structures (so they store things)
* GC is graphics content; it is a drawable
* XGC is a data structure that has a bunch of content much like an event where you only want a slim amount of data from it
```

    if (!(display = XOpenDisplay(NULL))) {
	perror("XOpenDisplay");
	exit(1);
    }
````
* `XOpenDisplay()`: open machine; this is a dummy check to make sure that the server is accessable
    * NULL is the machine you are running it on/where you sit (rather than a different one)
    * eg. we had to run X2go on the computer when we ran it, if it wasn't then the server wouldn't be accessable

````
    root = RootWindow(display,screen = DefaultScreen(display));

    XAllocNamedColor(display,DefaultColormap(display,screen),
		     FORE,&apparant,&exact);
    fgcolor = apparant.pixel;
    XAllocNamedColor(display,DefaultColormap(display,screen),
		     BACK,&apparant,&exact);
    bgcolor = apparant.pixel;
````
* Exact (with reference to  color) is what you ask for, aparent is what you get
    * modern day they are often the same
````

    window = XCreateSimpleWindow(display,root,0,0,400,400,2,fgcolor,bgcolor);

    gcval.foreground = fgcolor;
    gcval.background = bgcolor;
    draw = XCreateGC(display,window,GCForeground|GCBackground,&gcval);

    gcval.foreground = bgcolor;
    erase= XCreateGC(display,window,GCForeground|GCBackground,&gcval);

    XSelectInput(display,window,eventmask);
    XMapWindow(display,window);


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