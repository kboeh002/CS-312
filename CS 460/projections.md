# Projections

* we are interested in an *orthographic* projection
* it doesn't matter how far away the object is because it will still be projected at its original size


*[projections drawing](https://drive.google.com/file/d/16lrCCzEHveLhfQZtfzwUkVMs-VHMjlMi/view?usp=sharing)*

$\left[\begin{array}{ccc}
1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 \\
0 & 0 & 0 & 0 \\
0 & 0 & 0 & 1 \\
\end{array}\right]$

*[prism](https://drive.google.com/file/d/16lrCCzEHveLhfQZtfzwUkVMs-VHMjlMi/view?usp=sharing)*
* View volume is rectangular and the front and the back are all the same size
    * it projected onto this thing by the matrix

## Perspective Projections
INSERT PICTURE (projection plane)
* You have a center of projection
* perspective projection is the first realism mechanism we have seen
* d: distance between the center and the projection plane
* Projection plane is *not* the same as the xy plane
    * x' = $\frac{x}{z/d}$
    * y' = $\frac{y}{z/d}$
    * W = $\frac{z}{d}$

## Windowing Systems
* Windowing Environment
INSERT DRAWING
* Windowing screens were to make a virtual screen
* sockets are block oriented and are on every operating system
    * streams can also be used but are not standard on every operating system

Has the same five steps
1. Initialize - establishes the hook between the users setup (the double ended arrow in the [drawing](https://drive.google.com/file/d/16lrCCzEHveLhfQZtfzwUkVMs-VHMjlMi/view?usp=sharing))
2. Build your graphical objects (eg. images, fonts, colors)
    * They are all loaded in the window's server in order to minimize communications
    * Three ways to minimize communications:
        * Asynchronous communications: don't get anything back
        * Move functionality to the server so they can be accessed via number
3. Register Evts and CBs
4. Realize graphical objects
5. Evt loop



*NOTE: Preliminaries for the project- windowing systems*

