# CS 460
### 3/15/23
## Creating Polygon Meshes
* Simplistic polygon that we want to simplify the polygon into a mesh
* Tesilation: turn a surface into a series of polygons to turn it into a polygon mesh

    * methods to store a polygon into a mesh
    1. Explicit: Each of the polygons is stored as a n-tuple of XYZ coordinate pairs in an arry
        * simplest
        * each vertex has 3 values to it

        | X | Y | Z | | V2 | | | V4 | | V2 | V3 | V4 |
        |:-----|:-----|:----|:-----|:----|:-----|:----|:-----|:----|:-----|:----|:----|
        | V1 | V1 |V1| | P1| P1| P1| P1|P2|P2|P2|

        * Worried about shared verticies, edges
        * outside edges are less shared than inside edges
        * inefficient storage
        * The more complex the mesh is, the less efficient it is
        * doesn't check for anything shared
    * **THERE IS A QUESTION ON THE FINAL ABOUT THIS**

    2. Pointer to Vertex List: Verticies stored as XYZ tuples, Polygons are created from verticies
        * We are going to set up a vertex list
        * not pointers per say; index into an array of the list
        * more efficient than Explicit
        * the more points the more efficient it gets
        * doesnt deal with shared edges and verticies; doesn't check for anything shared
    3. Pointer to Edge List (Explicit Edge): Verticies stored as XYZ tuples; edges
        * Going to start out with the same v-list
        * now we are going to create edges
        * has polygon and vertex to where it belongs in it
        * V-List:
            |V1|V2|V3|V4|
            |:---|:---|:---|:---|
        * E-List:
            * E1 =
                |V2|V4|P1|P2|
                |:---|:---|:---|:---|
            * ...
            * E5 =
                |V2|V4|P1|P2|
                |:---|:---|:---|:---|
        * Point List:
            * P1 =
                |E1|E5|E4|
                |:---|:---|:---|
            * P2 =
                |E2|E3|E5|
                |:---|:---|:---|

        * Not as efficient as a Pointer to a vertex list
        * deals with shared edges
        * doesn't deal with shared verticies

<br>

* things to worry about when storing
    * efficiency of storage
        * All use array storage with array acess mechanisms to transfer to a specific spot
        * array indexing is very efficient
        * basically arrays of arrays
    * have pointers to a...
        * vertex list
        * edge list
* We are getting into realism mechanisms next
    * only one we have learned so far is anti-aliasing