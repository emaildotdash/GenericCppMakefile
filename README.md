# GenericCppMakefile

A pair of easy-to-use generic Makefiles to be used in C++ projects of any size on Linux.\
They should also be cross-platform, provided they are used in a Unix-like environment, but I currently do not guarantee anything besides Linux (with GNU Make) in this regard, as I have yet to test anything else.

I created these Makefiles with the intent to make compiling C++ projects easier for myself, as C++ build-systems on Linux are just not as plug-and-play simple as I want them to be.

I will continue working on these Makefiles in the future and extend their functionality according to my needs. Thus, I will __not__ take Pull-Requests. Feature suggestions are welcome, however.

Feel free to fork, alter and redistribute these Makefiles as you see fit. I shared it in hopes of making it easier for people to quickly get a project going, as well as to let the less experienced coders among us have a simple way into the world of C++ development on Linux.

> NOTE: In the following weeks I plan on uploading a video explaining how to use the Makefile for those who prefer that. I will also do some testing, as I have __NOT__ tested a lot of use cases yet, so I cannot guarantee that the Makefile will work in every scenario. If you find a problem, feel free to open an issue about it.

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


## Prerequisites

The Makefiles depend on:
- Bash-like shell with Unix commands (cd, mv, cp, ls, rm, pwd, mkdir, echo, ar, find, realpath, ...)
- A version of Make (for instance: GNU Make)
- The gcc compiler

In terms of knowledge, you will need:
- A basic understanding of shell (like how file paths work)
- Some very rudimentary knowledge about Makefiles (all you need are the basics of the syntax for variable declarations (see https://makefiletutorial.com/))


## Usage

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

---

__Firstly__, the build options of your project. These are available inside of the Makefile underneath the `### Project Specific` comment.\
Each Option has a brief explanation beside it, so I will not go into them here. (if there is any demand for a deeper explanation here, please open an issue about it)

> Note: Make sure you understand the syntax for variable declarations in Make (see https://makefiletutorial.com/)

---

__Secondly__, the available Make targets. A list of these is available at the top of the Makefile.\
If you have no idea how make works, I suggest reading into the manual (https://man.archlinux.org/man/make.1) . \
If you scroll down, you will also find a short description next to their definitions, I will however explain them here:

| MakefileGenericCpp Targets | Description |
|---------------|---------------|
| `make` or `make all` | will build the project according to the specifications set in the beginning portion of the makefile |
| `make exec`, `make dynamic` and `make static` | will build the project as an executable, a dynamic-library and a static-library respectively |
| `make run` | will build the project and subsequently run it if target in question is an executable |
| `make clean` or `make clear` | will clean up any files in the directory of the currently selected build target (release and debug directories) |
| `make cleanall` or `make clearall` | will clean up all files in the output directory |
| `make info` | will print a brief summary of the project and related information |
| `make package` | will copy all files required for the execution of the built project from the execution path to a separate folder, excluding any source files and the output directory |
| `make liblist` | convenience script for Linux : will list the /lib directory |
| `make fetch` | convenience script for updating the Makefile itself : will copy the version of the makefile stored in the ~/Templates directory if available, otherwise will create a copy there |

> NOTE: passing release or debug after a build call as SPECIFICALLY the second target will build the project with that in mind\
> e.g.: make all release, make static debug\
> This will work with the targets: `all`, `exec`, `dynamic`, `static`, `run`, `clean`, `clear`\
> Beware, though, that running `make clean debug` with `OPTIMIZATION := debug_nodir` will have the same effect as running `make cleanall`


### Superprojects

Larger Superprojects utilizing MakefileGenericCppSuperproj are a relatively simple compared to Single projects, though you need to be aware of how they work before using them.

Superprojects consist of main-projects and dependency-projects, where the all output files (except for static-libs) of dependency-projects are copied into all main-projects (specifically the first listed extra-library-folder).
Thus, main-projs are effectively the outputs and you can have as many of them as you want.
You can also have multiple Superprojects inside of each other as either main- or dep-projects and have an ultra-giga-mega-project (or whatever you want to call it).
This means you have a great amount of flexibility for creating projects of any scale and the Makefiles will do the hard work of tying them together for you.

One caveat is that there is currently no packaging script attached to the Superproj makefile, which means that to package one, you will have to go into the main-project directories and run `make package` there, after having built the Superproj.

There are only three build options and they're explained within the Makefile itself.

As for Make targets:

| MakefileGenericCppSuperproj Targets | Description |
|---------------|---------------|
| `make` or `make all` | will build all subprojects according to the specifications set in the beginning portion of the makefile |
| `make run` | will build and run one listed main-project; if there is more than one main-proj listed, it will run a dialogue first |
| `make runall` | will build and run all main-projects in sequence |
| `make clean` or `make clear` | will clean up any files in the directory of the currently selected build target (release and debug directories) of all subprojects |
| `make cleanall` or `make clearall` | will clean up all files in the output directory of all subprojects |
| `make info` or `make list` | will print a brief summary and related information for all subprojects |
| `make fetch` | convenience script for updating the Makefile itself : will copy the version of the makefile stored in the ~/Templates directory if available, otherwise will create a copy there |
| `make fetchall` | runs fetch for all subprojects |
| `make liblist` | convenience script for Linux : will list the /lib directory |

> NOTE: Passing release or debug as the second target works here in just the same way as well (see the note in the Single Projects section)


### Summary

In summary, use the single project Makefile for small to medium sized projects and connect multiple such single or even super-projects up using the Superproject Makefile.
Set your options and make use of the convenient build targets
