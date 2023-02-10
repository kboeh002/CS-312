# CS 460
### 2/2/23
## Transformations
* 3 main types of transformations:
1. Scale
2. Rotate
3. Translate: to move something
* all done with matrix multiplication where you have points that describe an object and then use the matrixmultiplication matrix and multiply it by the transformation matrix to find the new coords
* Grand Transformation matrix is applied to a point and is the final product
* send primitives one at a time from the graphics pipeline for our transformations and afterwards we will do shading and such
* graphics card does the multiplication for the transformation and is implied that the points are floating point values
    * NOTE: in this class you will never have to deal with the matrix multiplication because the graphics card does it
    * you need to be careful for the order you do rotates and scales
### 2D
* All translations are relative translations because it is relative to where the points are originally
    * must use a 3x3 matrix
    * homogonous coordinates
## INSERT TRANSFORMATION FIGURES
* so these are 2D transformations

* You should basically just use 3x3 for all because then you don't have to keep remaking it
### 3D
* formula for rotation is only for around a specific axis (x, y, or z)
* you are rotating around wherever the 1 is
## INSERT TRANSFORMATION FIGURES
* if multiple translates are *next to eachother* in a chain then the dx, dy, dz can be added together

**TEST QUESTION:** Gives you a list of transformation and write the transformation series (don't solve, but just write it)
    * can do in order given, or the most efficient order
    * one will be on the midterm, one will be on the final
