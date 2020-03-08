# Uniforms

Uniforms are a way for us to get data from C++ into our shader. For example, using a uniform to determine the color in a shader allows us to define that color in C++ and update it as necessary. 

## Table of Contents

1.  All About Uniforms
2.  Adding a Uniform to a Shader
    1.  Steps
    2.  Getting the Uniform's Location
    3.  Setting the Uniform's Data
3.  Going the Extra Mile
4.  Resources

## All About Uniforms

As mentioned before, uniforms help transfer data from the C++ code to a shader. They differ from buffers because they get set per draw. This means you can set up a uniform right before you draw to the screen. Since uniforms communicate between the application and the shader, we need to add them to both.

## Adding a Uniform to a Shader

It's pretty easy to add a uniform into a shader; they are essentially just another variable with an extra identifier. A fragment shader that uses a uniform to control the color of a pixel would look like this:

```glsl
#version 330 core

layout(location = 0) out vec4 color;

uniform vec4 u_Color; // Define our uniform

void main()
{
    color = u_Color; // Use it to determine the color
};
```

Pretty simple right? That's all we need to do to control the color using a uniform in GLSL. Now we'll take a look at how to set that value in C++. Be sure to remember the type and name of the uniform in the shader; we'll be using it in our main application.

## Adding a Uniform to C++

### Steps

>   Make sure these go after a shader has been bound by `glUseProgram()`

1.  Get the uniform's location
    1.  Make sure the location isn't -1 or an invalid location
2.  Set the uniform's data

### Getting the Uniform's Location

To do this, we'll need to know the name of the shader and the name of the uniform we want to access. Next, we need to store the location of the uniform in a variable. Finally, we need to make sure the location isn't invalid, and then we're ready to start sending it data. Example code doing these things is shown below:

```c++
int location = glGetUniformLocation(shader, "u_Color"); // Gets the location
ASSERT(location != -1); // Uses the ASSERT macro from error handling
```

### Setting the Uniform's Data

We can set the data of the uniform using one function in OpenGL. However, it is important to know the type of the uniform, because the actual name of the function depends on it. In our case, since we're using a `vec4` (4 `float`s), we'll use `glUniform4f()`.

```c++
glUniform4f(location, 0.2f, 0.3f, 0.8f, 1.0f);
```

And then we're done! Very simple, very easy, very powerful.

## Going the Extra Mile

As mentioned before, we can set the uniform's data right before drawing. So, to do a simple animation, we can modulate the red channel value right before drawing each frame.

```c++
float r = 0;
float increment = 0.1f;
while(!glfwWindowShouldClose())
{
    // ...
    r += increment;
    if (r > 1.f)
    {
        increment = -0.1f;
    }
    else if (r < 0.f)
    {
		increment = 0.1f;
    }
    
    glUniform4f(location, r, 0.3f, 0.8f, 1.0f);
    // ...
}
```

Finally, we'll sync the framerate of our program with the refresh rate of our monitor to achieve a smoother result. This can go anywhere before the draw loop, but let's put it right after we get a valid OpenGL context.

```c++
glfwSwapInterval(1);
```

And we're done! We now have a glowing rectangle, all thanks to uniforms.

## Resources

-   [The Cherno](https://www.youtube.com/watch?v=DE6Xlx_kbo0&list=PLlrATfBNZ98foTJPJ_Ev03o2oq3-GGOS2&index=12&t=658s) on YouTube
-   [My Previous Notes](https://github.com/Nohmayne/Notes/tree/master/OpenGL) 

