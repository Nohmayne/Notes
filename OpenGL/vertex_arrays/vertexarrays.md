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
+ Using the vertex arrays properly allows us to simply bind the vertex array object instead
    + No extra hassle!
    + Will bind a `GL_ARRAY_BUFFER`
    + Works with single or multiple buffers

## Changing Profiles
Earlier we talked about how using the core profile will force the developer to make their own vertex arrays. This isn't all bad, and can actually be advantageous for the final product. To change our profile, we'll need to add a few lines of code before creating the window and/or context. We need to:

1. Set the major OpenGL version
1. Set the minor OpenGL version
1. Set the current OpenGL profile to be "core"

Setting these can be done in `glfw` through a `glfwWindowHint()` call. The major and minor versions correspond to the "`major`.`minor`" version of the API, so setting major and minor versions to "3" means setting the OpenGL version as `3.3`. Setting the profile can be done using `glfw` enums with a call to the same function. The code should read as follows.

```c++
glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 3); // set major version
glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 3); // set minor version
glfwWindowHint(GLFW_OPENGL_PROFILE, GLFW_OPENGL_CORE_PROFILE); // set profile to core
```

After execution, this code will set the OpenGL version to `3.3` and the profile to `GLFW_OPENGL_CORE_PROFILE` (the `glfw` enum for the core profile).

Unfortunately, this change means that we lose access to the default VAO (vertex array object) object 0 created by the compatibility context. We can, however, create our own.

## Creating the VAO
Before we create the vertex buffer, we should create our vertex array. The VAO is created in a very similar manner to the other OpenGL objects:

1. Create an ID variable
1. Generate the actual VAO
1. Bind the VAO

These three very simple steps will create and bind a VAO, which will allow the program to work again, even using the "core" profile. After the VAO is created, the binding of the subsequent VBO and setting of the layout will be tied to the currently bound VAO. Then, in the draw loop, instead of having to enable the vertex attrib. array, set the layout of the vertex attrib. array, and then bind the buffer, we can simply bind the vertex array and the IBO, and OpenGL will have all the information it needs to draw to the screen properly.

```c++
unsigned int vao; // Create the ID
glGenVertexArrays(1, &vao); // Generate the VAO
glBindVertexArray(vao); // Bind the VAO

// ...

/* Draw Loop */
while (!glfwWindowShouldClose(window))
{
    // clearing screen, setting shader...

    glBindVertexArray(vao);
    glBindBuffer(GL_ELEMENT_ARRAY_BUFFER, ibo);

    // ...draw call, swapping buffers, etc.
}
```

This code should do everything in the steps outlined above.

Something important to note is the actual line that tells OpenGL to use the vertex array. This line is the `glVertexAttribPointer()` line, with the first argument stating the index of the currently bound VAO to be linked with the currently bound VBO.

After linking the VBO and VAO, OpenGL can then sort out the information it needs to parse the VBO using the VAO, and can draw to the screen.

## Methodology
There are essentially two schools of thought when it comes to VAOs.

1. Use one VAO throughout the entire application, binding different VBOs and setting layouts as you go
1. Use a VAO for every object you want to draw and just bind that instead

Which one to use depends entirely on the use case, but in most scenarios, the first option will most likely get you faster results. Whether or not it's good to do this is a matter of choice and opinion, but when it comes to performance there is a notable difference. NVIDIA has said in the past that they recommend not using VAOs due to performance issues, but that doesn't mean that it's what you have to do.

Ultimately, OpenGL recommends using VAOs, and for good reason. They allow for neater and easier to manage code, and they are part of the API and are there to be used. If performance is paramount, then using one VAO is better, but the readability that comes from using multiple VAOs is really very nice.

## Conclusion
VAOs allow us to very quickly and easily bind an object to be drawn to the screen without having to reiterate over code we've already written. This increases readability and maintainability of the code, although coming at a slight performance cost. Using VAOs is recommended based on the use case, but in general if performance isn't crucial then it's good to use them.

### Resources
+ [The Cherno](https://www.youtube.com/watch?v=Bcs56Mm-FJY&list=PLlrATfBNZ98foTJPJ_Ev03o2oq3-GGOS2&index=12)
+ The [OpenGL wiki](https://www.khronos.org/opengl/wiki/Vertex_Specification)
+ [docs.gl](docs.gl)
