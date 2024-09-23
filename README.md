# GenericCppMakefile

A pair of easy-to-use generic Makefiles to be used in C++ projects of any size on Linux.
They should also be cross-platform, provided they are used in a unix-like environment, but I currently do not guarantee anything besides Linux (GNU Make) in this regard, as I have yet to test anything else.

I created these Makefiles with the intent to make compiling C++ projects easier for myself, as C++ build-systems on Linux are just not as plug-and-play simple as I want them to be.

I will continue working on these Makefiles in the future and extend their functionality according to my needs. Thus, I will __not__ take Pull-Requests. Feature suggestions are welcome, however.

Feel free to fork, alter and redistribute these Makefiles as you see fit. I shared it in hopes of making it easier for people to quickly get a project going, as well as to let the less experienced coders among us have a simple way into the world of C++ development on Linux.

Lastly, this is my first time sharing an open-source project on the internet, so please do let me about any mistakes I may have made on the distribution or documentation side, or anywhere else really. Thank you for checking out this little project, I hope you will find it helpful.

## Capabilites

- Build C++ projects of sizes ranging anywhere from single-file to multi-file to multi-project
- Simple, yet powerful set of options for customizing build behavior (inside the Makefile)
- Flexible compilation to any target from the terminal
- Easily integrate 3rd party libraries into your applications (especially when paired with a package-manager)
- Simple cleanup of output-files when needed
- Print a summary of your project and some related stats
- Package your project (limited, but more on it later)
- Can be used with C as well, albeit with some relatively basic manual modifications
  
To come (perhaps):
- More Cross-Platform support (if I have time and willpower for it)
- built-in git commands (unlikely)

## Usage

To use these Makefiles, you will need:
- some basic knowledge about shell (like how file paths work)
- some very rudementary knowledge about Makefiles (if you do not have any, don't worry just follow the examples and be vary of whitespaces)

Firstly as you will notice there are two Makefiles:
- MakefileGenericCpp is for single projects with any number of source files
- MakefileGenericCppSuperproj is for large scale projects that connect together any number of sub-projects
This means the file Structure of a Single Project will look something like:
```
Proj/
|-output/
| |- ...
|-lib/
| |- ...
|-src/
| |-main.cpp
| |-myClass.h
| |-myClass.cpp
|-Makefile
```
A Superproject will on the other hand look more like:
```
SuperProj1/
|-Proj1/
| |- ...
|-Proj2/
| |- ...
|-Proj3/
| |- ...
|-SuperProj2/
| |-Proj4/
| | |- ...
| |-Proj5/
| | |- ...
| |-Makefile
|-Makefile
```
As you may have guessed, you must use the appropriate makefile in the appropriate Project type. I will explain this in further detail in the following sections.

### Single Projects

For simple projects utilizing MakefileGenericCpp, you need to be aware of two things:

__Firstly__, the build options of your project. These are available inside of the Makefile underneath the `### Project Specific` comment.
Each Option has a brief explanation beside it, so I will not go into them here. (if there is any demand for a deeper explanation write a message on this project)

__Secondly__, the available Make targets. A list of these is available at the top of the Makefile.
If you have no idea how make works I suggest reading into the manual (https://man.archlinux.org/man/make.1).
If you scroll down, you will also find a short description next to their definitions, I will however explain them here:

TODO





