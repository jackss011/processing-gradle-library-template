# Build Processing library using Gradle
This template allows you to create a processing library which can be packaged using gradle.

A list of available tasks can be shown using `gradlew tasks` in the terminal.

Every task must be executed in same directory of `gradle.build` file.

## Task summary
- compile - compile the library in .class file
- package- create a jar file in `<root>/libarary`
- examples - show a list of all available example, contained in `<root>/examples`
- run - run the selected example
- open - open the selected example

To select an example see (Examples Management)[#examples-management]

## Prerequisites
- Good knowledge of Processing projects.
- Good knowledge of Processing library structure. See the [Official Documentation](https://github.com/processing/processing/wiki/Library-Overview).
- Basic knowledge of Gradle build system. See See [Gradle docs](https://gradle.org/docs).

## Precessing library basics
Processing libraries consist in a folder (here called *library folder* or `<root>` in paths) placed in `[...]/<sketch-folder>/libraries`.
`<sketch-folder>` is  where your processing skecthes are stored. This folder can be configured in `File > Preferences` in the Processing IDE.

The packaged jar library is contained in `<root>/library`.
The jar file is generated by Gradle using `gradlew package`. See below for a better description.

Examples of the library usage can be provided. See [Example management](#examples-management).

More infos about Processing libraries can be found  on the officials
[Library Guidelines](https://github.com/processing/processing/wiki/Library-Guidelines) or
[Library Basics](https://github.com/processing/processing/wiki/Library-Basics).

## How to setup

### Step 1: Download
Download the zipped repository and exctract it in a folder in `<your processing sketch folder>/libraries`
> ex .../Processing/libraries/library-folder

Note: *library folder* must contain only letters and numbers.


### Step 2: Configure
- Setup **libraries.properties**.

  This file contains processing library infos (such as name, author, repo, ecc.).

- Setup **lib-user.json**.

  This file is used to store the processing installation directory (`processing`) and the selected example (`selected`).
  Since these are user-specific values the file shouldn't be included in VCS.

  Note: the file in **NOT** included with the template and must be manually created.

  While the processing installation directory must be specified in order to compile and package the library,
  the selected example is added automatically by the `gradlew <example-folder-name>` task and thus can be omitted
  > ex. D:/Programs/Processing/processing-3.2.1  
  ```json
  {
    "processing": "your/processing/directory",
    "selected": "selected/example"
  }
  ```


### Step 3: Write the library
Write library java code inside the `<root>/src` folder. A default package is provided containing a basic library class.

You can replace this package with your own.

The package will be available for `import` in .pde files in the editor once the library is packaged.
  ```java
  import my.library.*;  //name of the package
  ```


### Step 4: Package the library
Run `gradlew package` in the terminal.

This task compile the source code into a jar placed in `<root>/library` and named `<root>.jar`.


### Step 5: Add the library to your .pde project
You can use the library once packaged in a standard project or in a example project (placed in `<root>/examples`)
directly from processing: `Sketch > Import Library > YourLibrary`.

The library name in `Import Library` dropdown is the one defined in library.properties.



## Examples management
This template allows to run and compile examples directly from the terminal.

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
  |   ∟ my
  |      ∟ package
  |           ProcessingLib.java
  ∟ library
  |  ∟ root.jar
  ∟ build.gradle
  ```
Note:
- The main .pde file (which contains `setup()` and `draw()`) and its parent folder must have the same name.  i.e. ".../FirstExample/FirstExample.pde".

Use `gradlew examples` to show a list of examples contained in `<root>/examples`.

Use `gradlew <example-folder-name>` to select an example. ex: `gradlew FirstExample`.
The example name is cached in the **lib-user.json** file.

Use `gradlew run` to package the library if needed and run the selected example.
