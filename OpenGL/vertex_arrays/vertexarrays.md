# Vertex Arrays
+ Specific to OpenGL
+ *Not* buffers, vertex or otherwise
    + Extremely similar to vertex buffers, however
+ A way to bind vertex buffers with specifications for its layout
+ Useful for repeated draws or recalibration of the OpenGL state machine

## Reasons
+ After binding the vertex buffer and setting it up, specifying the layout can get repetitive
+ Using vertex arrays allows us to simplify that process
+ Especially useful in larger / more complicated projects
+ Simplifies basic structure

## Logistics
+ For large projects, the steps to use the vertex buffer are as follows
1. Bind the shader
1. Bind the vertex buffer
    1. Specify the layout
	    + Not actually stored in the buffer
1. Bind the index buffer
1. Draw the object
+ This can get extremely lengthy and complicated
    + Have to rebind every time
    + Gets tedious when there are multiple objects
+ Already using a vertex array behind the scenes with `glVertexAttribPointer()`
    + Already mandatory
    + Created by default with the compat. profile
    + **Core profile does not do this!**
	    + Necessary to bind it manually
+ Using the vertex arrays properly allows us to simply bind the vertex array object
    + No extra hassle!
    + Will bind a `GL_ARRAY_BUFFER`
    + Works with single or multiple buffers
