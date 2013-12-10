How to Run Jekyll on Windows
============================

Sadly, getting [Jekyll](http://jekyllrb.com) to run on Windows is not as easy as it is on Mac OS X or Linux,
which is also why it is not officially supported or documented.

Running Jekyll on Windows is not impossible though. In fact, there are a lot of tutorials out there, some
more, some less helpful. Most of these are written as blog posts which is often why they become outdated and
inaccurate over time.

This repository is intended to provide Windows users with instructions to successfully run Jekyll - not just
at the time of its creation but hopefully also in the future, when common solutions become outdated once
again.

A few notes before we get started
---------------------------------

* Except where otherwise noted, content in this repository is licensed under a Creative Commons Attribution
3.0 license. You can find a copy of the license in the [LICENSE file](LICENSE).
* Liability claims regarding damage caused by the use of any information provided, including any kind of
incorrect or sparse information, will be rejected. **USE THE INFORMATION PROVIDED ON THIS PAGE AT YOUR OWN RISK**.

* * *

## Overview ##

Below, you'll find instructions to install...

* ... Ruby. [jump to section](#install-ruby)
* ... the Ruby Dev Kit to be able to build native extensions. [jump to section](#install-the-ruby-devkit)
* ... the Jekyll gem. [jump to section](#install-the-jekyll-gem)
* ... Python to be able to use Pygments, a common syntax highlighter, with Jekyll. [jump to section](#install-python-environment)
* ... Python setup\_tools and pip to install the Python part of Pygments. [jump to section](#install-setup\_tools)
* ... the working version of the Pygments gem. [jump to section](#install-python-part-of-pygments)

Finally, you'll be able to [Run Jekyll](#run-jekyll) on Windows using one last trick.

## Install Ruby ##

Ruby is the language Jekyll is written in. We'll need to install it first to get started.

1. Download a RubyInstaller from [rubyinstaller.org](http://rubyinstaller.org/downloads/).
  * Version 2.0.0 should work fine.
  * Make sure to download the right package depending on your system's architecture: x86 / x64
2. Execute the installer which will guide you through the installation.
  * The only customization you need to make for our purposes is to check the box "Add Ruby executables to your
    PATH" on the last screen before the actual installation.
3. After you click on Install, you're all set with Ruby!

## Install the Ruby DevKit ##

Some of Jekyll's dependencies need to be built as "native extensions". To do that, you'll need the Ruby DevKit.

1. Download the package from [rubyinstaller.org](http://rubyinstaller.org/downloads/).
  * The DevKit's version number and target architecture (32/64 bit) need to match your Ruby installation.
2. What you have now is a self-extracting archive.
  * Execute the file.
  * Change the extraction destination to something like `C:\rubydevkit\`.
  * Extract the archive.
  * **Note**: For some reason, the extraction might fail if you have lots of other programs running.
3. Initialize the DevKit and bind it to your Ruby installation (via your preferred command line tool).
  * Navigate to the folder you extracted the DevKit into.

            cd "C:\rubydevkit\"

  * Auto-detect Ruby installations and add them to a configuration file.

            ruby dk.rb init

  * Install the DevKit.

            ruby dk.rb install

## Install the Jekyll gem ##

This is it.

1. Install Jekyll from the command line.

        gem install jekyll

2. Watch and enjoy.


* * *

You now have Jekyll installed on your Windows computer. If you are sure you'll never need to use Pygments,
you can skip to the [Run Jekyll](#run-jekyll) section. Otherwise, read on to get Pygments running as well.

* * *

## Install Python Environment ##

If you want to use Pygments, which is a default Jekyll dependency, for syntax highlighting on Windows, you need to
install Python, setup_tools and pip.

### Install Python ###

1. Download the Python installer from [python.org](http://www.python.org/download/).
  * Python 3 is currently known not to work with Jekyll. Use Python 2.7.5.
  * Again, make sure to download the package intended for your system.
2. Execute the installer. All default values should be fine.

### Install setup_tools ###

1. Download the setup_tools installer that matches your system and your Python installation from
   [here](http://www.lfd.uci.edu/~gohlke/pythonlibs/#setuptools).
2. Execute the installer.
  * If you used the default values when installing Python, you can do the same here. Otherwise, enter the correct
    path.

### Install pip ###

1. Download the pip installer that matches your system and your Python installation from
   [here](http://www.lfd.uci.edu/~gohlke/pythonlibs/#pip).
2. Execute the installer.
  * If you used the default values when installing Python, you can do the same here. Otherwise, enter the correct
    path.

### Add pip and Python to your PATH environment variable ###

Before you can use pip from the command line to install Pygments, you need to add your Python environment to your
PATH environment variables.

1. Add `C:\path-to-your-python-installation\Scripts;` to the _beginning_ of your **user** PATH variable. The semicolon is
   important! Without it, you'll mess up your PATH. If you used all the default settings, the string to add should
   be `C:\Python27\Scripts;`. Of course, you can also put the semicolon before the new path and add it to the _end_
   of your **user** PATH variable: `;C:\Python27\Scripts`
2. Add `C:\path-to-your-python-installation\;` to the _beginning_ of your **system** PATH variable. The semicolon is
   important! Without it, you'll mess up your PATH. If you used all the default settings, the string to add should
   be `C:\Python27\;`. Of course, you can also put the semicolon before the new path and add it to the _end_
   of your **system** PATH variable: `;C:\Python27\`

## Install Python part of Pygments ##

Open a new command line window and run the following command:

    pip install Pygments

## Install working version of Ruby part of Pygments ##

Pygments.rb currently has a bug that causes Jekyll to fail when trying to compile sites that use Pygments. As s
workaround, you can install an older version of the Pygments gem that doesn't have this problem.

1. Find out which version of Pygments you have installed.
  * Run `gem list` and look for pygments in the output. There should be a version number like `0.5.2` listed next
    to it.
  * If you already have version 0.5.0 (and only that version) installed, you're already good to go.
2. Uninstall the broken version of Pygments. Confirm that you want to break Jekyll's dependency (temporarily).

        gem uninstall pygments.rb --version "=your.installed.version"
        (e.g. gem uninstall pygments.rb --version "=0.5.2")
        ...
        Continue with Uninstall? [yN] y
3. Install the old, working version of Pygments.

        gem install pygments.rb --version "=0.5.0"

## Run Jekyll ##

To run Jekyll, change the command line's encoding to UTF-8, navigate to your site source folder and run the
Jekyll command of your choice.

    chcp 65001
    cd "C:\my-site\"
    jekyll serve

If you don't change the encoding, Jekyll will likely fail to build your site because of special
characters it doesn't understand. You need to do this every time you open a new command prompt before running Jekyll.
