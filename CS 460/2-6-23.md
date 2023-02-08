# CS 460
### 2/6/23

## Input Handling
* main concern is timeing like moving a mouse while clicking
    * Techniques
        * polling output devices
        * request driven: using interrupts ot request permission to speak
        * event driven: (there are 28 different events) uses timestamps and an event queuen now used by all window systems
            * events are *interrupt driven*
* eg. of eventss
    * Button Click
    * Button Release
    * Movement
    * Realistate Modulation: movement into a different window (eg. moving pointer into another window and then having to click the window in order to interact with the new window)
    * Property Notify: the syncronization of two processes
        * Property is a process linked to a window
    * Expose Event: when a window becomes visible (eg. for the first time, is uncovered, or unminimized)
    * expose events
* events are put on an event queue in the order in which they occur
* you have to tell the computer what kind of events you want to hear about 
    * eg. you only want mouse clicks, not key presses

### The 5 Steps For All Windowing
1. Initialize connection to user set up
2. Build Graphical Objects
3. Register Events and Call-Backs
    * must register the call back function associated with that event driven entry
    * it doesn't know what you want so you need to tell it what you want it to do for each event
4. Realize Graphical Objects: means display what you want it to display
    * you want it to display something specific, not each window from each event
    * basically "draw the ones you need now" with a map (reveal) function and unmap (hide, *not close*; eg. go back) function
        * may be the "master" or the pop out windows
5. Event Loop: get the next event, use the case statement to get to the type of event it is, then follow that case's statements/instructions, then repeat infinitely...
    * basically right out of pascal eg...
        ````
        while(constant doomsday == true){
            if(eventOccurs){
                doomsday == false;
            } 
        }
            /** has no way out of it unless you put something to get out of it */
        ````
    * is a fetch to pull an event off of the queue, now you have a case statement
    * case statement goes into a data structure you can access (local variable) and what kind of event it is, then a series of things that you want to have execute when the event occurs
    * case statements are all based on the type of event

## Output Handling
* How do we handle "expose" events since windows cna be thought of as being a 3D stack?
1. Put each window in its entirety into main memory
2. Just put the covered up part into main memory


# Come to Dragas 1100A (office) next class (2/8/23) to see program rubberband.c in his office