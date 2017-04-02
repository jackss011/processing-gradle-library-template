# Build Processing library using Gradle
This template allows you to create a processing library which can be packaged using gradle.

## Prerequisites 
- Good knowledge of Processing projects.
- Good knowledge of Processing library structure. See the [Official Documentation](https://github.com/processing/processing/wiki/Library-Overview).
- Basic knowledge of Gradle build system. See See [Gradle docs](https://gradle.org/docs).

## Precessing library basics
Processing library are basically a folder (here called *library folder* or `<root>`) placed in `.../<sketch-folder>/libraries`.
`<sketch-folder>` is  where your processing skecthes are stored. This folder can be configured in `File > Preferences` in the Processing IDE.

The most important sub-directory is the *library folder* is `<root>/library` which contains your packaged library.
This file is generated by Gradle using `gradle packJAr`. See below for a better description.

Examples of your library usage can be provided. See [Example management](#examples-management).

More infos about Processing libraries can be found  on the officials
[Library Guidelines](https://github.com/processing/processing/wiki/Library-Guidelines) or 
[Library Basics](https://github.com/processing/processing/wiki/Library-Basics).

## How to setup

### Step 1: Download
Download the zipped repository and exctract it in a folder in `<your processing sketch folder>/libraries`
> ex .../Processing/libraries/my-lib


### Step 2: Configure
- Setup **libraries.properties**. 

  This file contains processing library infos (such as name, author, repo, ecc.).

- Setup **build.gradle**.

  If you want to run library examples from gradle, you must setup in the following closures the processing install location
  > ex. D:/Programs/Processing/processing-3.2.1  
  ```groovy
  processing {
    directory: 'your/processing/directory'
  }
  ```


### Step 3: Write your library
Write library java code inside the `<root>/src` folder. A default package is provided containing a basic library class.
  
You can replace this package with your own.
  
The package will be available for `import` in .pde files in the editor.
  ```java
  import my.library.*;
  ```


### Step 4: Compile the library
Run `gradle packJar`in the terminal in the same directory of `build.gradle` and `processing-lib.gradle`.

This task compile the source code into a jar placed in `<root>/library`.


### Step 5: Add the library to your .pde project
You can use the library once compiled in a standard project or in a example project (placed in `<root>/examples`)
directly from processing: `Sketch > Import Library > YourLibrary`. 

The library name in `Import Library` dropdown is the one defined in library.properties.



## Examples management
Using this template allows you to run examples contained in your library from the terminal, automatically building the library.

Examples *must* be stored in `<root>/examples` following this structure:
  ```
  root
  ∟ examples
  |   ∟ FirstExample
  |      ∟ FirstExample.pde
  |   ∟ SecondExample
  |      ∟ SecondExample.pde
  |      ∟ OtherClass.pde
  ∟ src
  ∟ library
  ∟ build.gradle
  ```
Note:
- The main .pde file which contains `setup()` and `draw()` must be in a parent folder with the same name of it.  i.e. ".../FirstExample/FirstExample.pde".

Use `gradle examples` to show a list of examples contained in `<root>/examples`.

Use `gradle <example-name>` to select an example. `<example-name>` is the name of the example folder. i.e. `gradle FirstExample`.
The example name is cached in a .txt file in the `<root>/build folder`.

Use `gradle run` to package the library if needed and run the last selected example.
