---
layout: default
title: Installation
---   

Before installing Edgware ensure that your system meets the [prereqs](prereqs.html).

Download the [latest stable release](http://edgware-fabric.org/download) of Edgware from [http://edgware-fabric.org](http://edgware-fabric.org). The `.zip` or `.gzip` contains a top-level folder called `edgware-X.Y.Z` where `X.Y.Z` is the version number. Once extracted, from within that top-level folder, run the appropriate command for your operating system:

**Linux and OS X**

    $ ./fabinstall.sh
    
**Windows**

	> fabinstall

**Note:** it is important to choose the appropriate file for your system, `.zip` for
Windows or `.gzip` for Linux, to ensure that file permissions are set correctly when
the file is unpacked.

At the end of the installation script a message will be displayed indicating that two environment variables must be set:

1. `JAVA_HOME`: the Java home directory (may already be set for your system).
2. `FABRIC_HOME`: the root directory for the Edgware installation; this is the directory containing the `fabinstall` script.

Both of these are required for Edgware to run.

#### Development code

If you want to run the very latest development code then you can clone the source repository directly from GitHub:

    $ git clone https://github.com/edgware/edgware.git
    
Whilst we alway try to ensure the repository is bug-free please note that it may contain features that are still under development.
