## Acknowledgments
This project is based on [GLSL-Shader-Includes](https://github.com/tntmeijs/GLSL-Shader-Includes), licensed under the MIT License.

# GLSL Includes Expanded
A utility class which allows the end user to make use of statements such as include in a shader file.
This is a C++ class but any programmer that has basic knowledge of his / her programming language of choice, should be able to quickly convert the code to another language within a couple minutes. It is that simple.

## Using this class
Since the entire class is a static class, you only have to add this to to your project:

```cpp
#include "Shadinclude.hpp"
```
```cpp
std::string shaderSource = Shadinclude::load("./path/to/shader.extension", "customKeyword");
```

Now, you might be wondering, what is the point of using your code for something so trivial as to loading a file and calling the "std::getline()" function on it?

Well, besides loading the shader source code from a single file, the loader also supports custom keywords that allow you to include external files inside your shader source code! Since all of this loading is still fairly trivial but cumbersome to write over and over again, it has been uploaded to this repository for you to use.

## Supported keywords

### Include

```cpp
#include "../Libraries/lib/lygia/generative/random.glsl"
```

This will (recursively) extract the source code from the shader file.

### Define

```cpp
#define RANDOM_SINLESS
```

This is defines a macro for [ifdef and ifndef](ifdef-ifndef-else-and-endif) and does nothing else.

```cpp
#define QTR_PI 0.78539816339
```

This is defines a macro for [ifdef and ifndef](ifdef-ifndef-else-and-endif). Also, all 'QTR_PI' strings are replaced by '0.78539816339'

### Ifdef, Ifndef, Else and Endif

```cpp
#ifndef RANDOM_SCALE
    #ifdef RANDOM_HIGHER_RANGE
        #define RANDOM_SCALE vec4(.1031, .1030, .0973, .1099)
    #else
        #define RANDOM_SCALE vec4(443.897, 441.423, .0973, .1099)
    #endif
#endif
```

This will check if 'RANDOM_SCALE' is defined. If not, it checks whether 'RANDOM_HIGHER_RANGE' is defined. If this is true, 'RANDOM_SCALE' is defined as 'vec4(.1031, .1030, .0973, .1099)'. If this is false, 'RANDOM_SCALE' is defined as 'vec4(443.897, 441.423, .0973, .1099)'.

Not every #ifdef or #ifndef have to have an #else, but they have to be closed by an #endif.