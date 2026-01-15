---
title: "Part 2: Getting started with git"
teaching: 10 # teaching time in minutes
exercises: 10 # exercise time in minutes
---

:::::::::::::::::::::::::::::::::::::: questions 

- How do I manage some files with git?
- What are the most basic git commands?
- How do I use them?
- Why are we using the command line?!

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Learn the basics of a simple git workflow, adding and committing files
- Try out and understand the core git commands that all git users need to know

::::::::::::::::::::::::::::::::::::::::::::::::

## Getting started with git

##### Why are we using the command line?

Git can be a complex tool to work with but if you understand it properly, it's
extremely powerful and can save you from losing files or help you recover when
something breaks!

While there are now various graphical user interfaces for git, for example
[GitHub Desktop](https://github.com/apps/desktop), or git integration with a
wide range of text and code editors, these tools often obfuscate key elements
of the git workflow and the tasks being carried out. We feel that learning the
basics of git through its low-level command line interface offers the best
route to properly understanding git.

### Set up a simple project directory and git repository

1. Open your shell/terminal, change into your home directory and create a project
   directory...
   
   _If you're on Windows, ensure you open the Git Bash application which will
   open a bash shell (on of the standard Linux/Unix shells), rather than the
   Windows command prompt or PowerShell._

   ```bash
   $ cd    # This will take you to your home directory, in case you're not there by default
   $ pwd   # print working directory - will tell which directory you're in
   $ mkdir git-intro      # Create a new git-intro directory
   $ cd git-intro         # Change into this directory
   ```

2. Create a simple file in this directory to start working with...

   For this simple example, we'll pretend we're working with a 3D printer which
   needs a configuration file. That configuration file is going to be in
   [YAML](https://yaml.org/) format.

   You can edit the file in a text editor of your choice. If you're not
   familiar with any basic command line text editors, many systems have `nano`
   available and this is a good choice. (_`nano` should also be available in Git
   Bash on Windows_).

   ```bash
   $ nano printer-config.yaml
   ```

   Paste the following content into the file (_with thanks to GPT-5 which
   kindly generated this ultra-short, pseudo-realistic config file in YAML -
   note that this file does not represent a real configuration for any printer
   device and shouldn't be used as such - all values are placeholders
   parameters are examples._)

   ```
   printer: { model: "PrintExpert3D-400", kinematics: cartesian, bed: { x: 220, y: 220, z: 250 } }
motion: { vmax: 200, amax: 3000, z: { vmax: 12, amax: 80 } }
axes:
  x: { travel: [0,220], home: min }
  y: { travel: [0,220], home: min }
  z: { travel: [0,250], home: probe }
extruder: { nozzle: 0.4, filament: 1.75, temp_max: 260, min_extrude_temp: 170 }
bed: { temp_max: 120 }
probe: { offsets: [-30,-5,0] }
mesh: { area: { min: [20,20], max: [200,200] }, grid: [5,5] }
macros:
  start: "M140 S{bed|60}; M104 S{hotend|200}; G28; M190 S{bed|60}; M109 S{hotend|200}"
  end:   "G91; G1 E-2 Z10; G90; M104 S0; M140 S0; M106 S0"
notes: "Demonstration pseudo‑config file for training purposes; all values are placeholders."
   ```

   If you're not familiar with `nano`, you can exit using Ctrl-x and you'll be asked if you want to save the file. You can also save first by using Ctrl-o. If you've not made any further changes after saving, Ctrl-x will then exit straight away.


3. Initialise a git repository in your `git-intro` directory.

   Here we're telling git that we want to be able to use it to manage files within this directory (and all directories below this one - i.e. all subdirectories.)

   ```bash
   $ git init     # initialise a git repository in this directory
   ```

   You've learnt your first git command! If you run `ls -al` now, you should
   see a `.git` directory present. This is what git created when you ran `git
   init`. So, we now have a directory with a file in it, and we've initialised
   a git repository in that directory. How do we tell git to actually do
   something useful?! 

