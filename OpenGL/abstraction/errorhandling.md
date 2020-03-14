# Error Handling

## What we have

Right now we've got a custom assertion that we have to call on every OpenGL function to get errors which is located at the beginning of our single `.cpp` file. This stuff is fairly common and should probably be abstracted.

## Abstraction

To make this code easier to handle, let's put it in a different class.

1. Create a `.cpp` and `.hpp` files for the renderer
1. Cut and paste the code from the top of the file over into the new `.hpp` file
1. Add necessary external header files
1. Modify the code to work in a `.hpp`
1. Implement it in the `.cpp` file

Since copying and pasting the code is fairly simple, we'll jump to step 3.

### Adding necessary external headers

In the case of our error handling, we only need to `#include <GL/glew.h>`. That's about it.

### Modifying the code

First thing's first, we should make our functions declarations, not definitions. We'll define them in the `.cpp` file. Then we should also remove any `static` keywords since they're in a header file. Our final header file should have our assertion, and then the method headers with no definition.

### CPP implementation

After modifying our header file, we can now actually define the functions in our `.cpp` file (after including the `.hpp` file of course). Because we use `std::cout` in our functions, we'll also need to include `<iostream>`.

Now we should be finished, and we can just include the `.hpp` file in our main application to be able to use the assertion and `GLCall()` macros we made.

