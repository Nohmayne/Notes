# Replacement

*Now that we've abstracted, let's modify our original application to reflect that*

## Error handling

Simply removing the error handling code at the beginning of our file and including the renderer header file should do it for this step. Not to shabby!

## VBOs

Being sure to include both header files, we can now replace much of our code involving both with new abstracted versions.

Our code creating, binding, and setting the data of our vertex buffer can be replaced with the instantiation of a new `VertexBuffer` object, including our data and its size in the constructor as follows:

```c++
VertexBuffer vbo(positions, 4 * 2 * sizeof(float));
```

Since we automatically bind the VBO upon creation, we don't need to call `vbo.bind()` at all.

## IBOs

We'll follow a similar process for VBOs, supplying the constructor with our data and count of indices.

## Drawing

When we expand the renderer, we can use it to draw, but for now we'll do it the same way we've been doing it.

Instead of binding our index buffer the traditional way before drawing, we can just call `ibo.bind()` and draw.

## Cleaning Up

To avoid the program persisting after close due to trying to clean up our stack allocated objects even though there's no OpenGL context, we can just put everything from before the `positions` array to just before we terminate GLFW, fixing the problem.

