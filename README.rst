======================================
How To Add Three20 to a iPhone Project
======================================

:Author: Stefan Eletzhofer
:Date: 2011-02-23


Abstract
========

These are my notes on how to add three20 to a iphone project.

Steps
=====

Create new Project using XCode
------------------------------

- create a new project using xcode, I used a simple `window based` iPhone
  project

- initialize git repo::

     seletz@QuickBrett: Three20Test $ git init
     seletz@QuickBrett: Three20Test $ git add -f Classes/ Three20Test.xcodeproj/project.pbxproj *.m *.pch *.xib
     seletz@QuickBrett: Three20Test $ git ci -m "XCode template"
  
Add Three20 as a GIT submodule
------------------------------

- I'll create a `Libraries` directory to keep all external libraries, and
  I'll add a GIT submodule for *three20* there::

     seletz@QuickBrett: Three20Test $ mkdir Libraries
     seletz@QuickBrett: Three20Test $ git add Libraries/
     seletz@QuickBrett: Three20Test $ git submodule add https://github.com/facebook/three20.git Libraries/three20

Using `ttmodule.py` to add three20
----------------------------------

The nice developers from *three20* have created a nifty python script::

    seletz@QuickBrett: Three20Test $ python Libraries/three20/src/scripts/ttmodule.py 
    Usage: ttmodule.py [options] module(s)

    The Three20 Module Script.
    Easily add Three20 modules to your projects.

    Modules may take the form <module-name>(:<module-target>)

    module-target defaults to module-name if it is not specified
    module-name may be a path to a .pbxproj file.

    Examples:
      Most common use case:
      > ttmodule.py -p path/to/myApp/myApp.xcodeproj Three20

      Print all dependencies for the Three20UI module
      > ttmodule.py -d Three20UI

      Print all dependencies for the Three20 module's Three20-Xcode3.2.5 target.
      > ttmodule.py -d Three20:Three20-Xcode3.2.5

      Add the Three20 project settings specifically to the Debug and Release configurations.
      By default, all Three20 settings are added to all project configurations.
      This includes adding the header search path and linker flags.
      > ttmodule.py -p path/to/myApp.xcodeproj -c Debug -c Release

      Add the extThree20XML module and all of its dependencies to the myApp project.
      > ttmodule.py -p path/to/myApp.xcodeproj extThree20XML

      Add a specific target of a module to a project.
      > ttmodule.py -p path/to/myApp.xcodeproj extThree20JSON:extThree20JSON+SBJSON

    Options:
      -h, --help            show this help message and exit
      -d, --dependencies    Print dependencies for the given modules
      -v, --verbose         Display verbose output
      -p PROJECTS, --project=PROJECTS
                            Add the given modules to this project
      -c CONFIGS, --config=CONFIGS
                            Explicit configurations to add Three20 settings to
                            (example: Debug). By default, ttmodule will add
                            configuration settings to every configuration for the
                            given target


Well, then, let's try it::

    seletz@QuickBrett: Three20Test $ python Libraries/three20/src/scripts/ttmodule.py -p ./Three20Test.xcodeproj/ Three20

Build::

    seletz@QuickBrett: Three20Test $ xcodebuild -configuration DEBUG
    ...
    ** BUILD SUCCEEDED **
    

And that is all!

Links
=====

**three20**
    https://github.com/facebook/three20

..  vim: set ft=rst tw=75 nocin nosi ai sw=4 ts=4 expandtab:
