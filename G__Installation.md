
# Installation

GAMA comes in 6 different versions (32 & 64 bits for Windows, Linux and MacOS). You first need to determine which version you are going to use (it depends on your computer, which may, or not, support 64 bits instructions, but also on the version of Java already installed, as the number of bits of the two versions must match).

You can then download the right version from the [Downloads page](https://code.google.com/p/gama-platform/wiki/G__Downloads), expand the zip file wherever you want on your machine, and [launch GAMA](G__Launching).


## Table of contents 

* [Installation](#installation)
	* [System Requirements](#system-requirements)
	* [Installation of Java](#installation-of-java)
		* [On MacOS X (Lion, Mountain Lion, Mavericks)](#on-macos-x-lion-mountain-lion-mavericks)
		* [On MacOS X (Yosemite)](#on-macos-x-yosemite)
		* [On Windows 7 & 8 64 bits](#on-windows-7-&-8-64-bits)
		* [On Ubuntu & Linux](#on-ubuntu-&-linux)


## System Requirements

GAMA requires that Java 1.6 or 1.7 be installed on your machine, approximately 200MB of disk space is available and that a minimum of RAM (4GB is recommended) is installed (to increase the portion of memory usable by GAMA, please refer to [these instructions](G__Troubleshooting#Memory_problems)).



## Installation of Java

On Windows and Linux the recommended Java Virtual Machine under which GAMA has been tested is the one distributed by Oracle. On MacOS X, it is (still) the one distributed by Apple (see below). It may work with others — or not. For better performances, you may also want to install the JDK version of the JVM (and not the standard JRE), although is it not mandatory  (GAMA should run fine, but slower, under a JRE).

### On MacOS X (Lion, Mountain Lion, Mavericks)
The latest version of GAMA requires a JVM (or JDK) compatible with Java 1.6 to run. There are two of them available for MacOS X. JDK 1.7 is distributed by Oracle, while JDK 1.6 is distributed by Apple.
Because of this bug in SWT (https://bugs.eclipse.org/bugs/show_bug.cgi?id=374199), GAMA will not run correctly under JDK 1.7 (all the displays will appear empty).

If JDK 1.7 is already installed, it is then necessary to also install the JDK 1.6 distributed by Apple in order to run GAMA. The latest version, « Java for OS X 2014-001 », can be obtained here : http://support.apple.com/kb/DL1572. Alternatively, you might want to go to https://developer.apple.com/downloads and, after a free registration step if you're not an Apple Developer, get the complete JDK from the list of downloads.


### On MacOS X (Yosemite)
If you upgrade your Mac OS X version to **Yosemite** (latest version, aka Mac OS X 10.10), some changes in the management of Java Virtual Machines might prevent the GAMA displays from working and it will make your models crash the platform. One fix for this behavior is, **after** having upgraded Mac OS X, to install (or reinstall in case you have already installed it) the same « Java for OS X 2014-001 », available here: http://support.apple.com/kb/DL1572.

If you run the developer version of GAMA (i.e. under Eclipse), it is necessary, in that case, to reconfigure the "Installed JREs" (Preferences > Java > Installed JREs) so as to point JDK1.6 to the location where Yosemite now installs it (i.e. in `/System/Library/Java/JavaVirtualMachines/1.6.0.jdk/Contents/Home`). See [here](http://stackoverflow.com/questions/26450420/osx-10-10-and-eclipse-luna-own-app-crashes-when-started-from-inside-eclipse) for related information.


### On Windows 7 & 8 64 bits
Please notice that, by default, Internet Explorer and Chrome browsers will download a 32 bits version of the JRE. Running GAMA 32 bits for Windows is ok, but you may want to download the latest JDK instead, in order to both improve the performances of the simulator and be able to run GAMA 64 bits.

  * To download the appropriate java version, follow this link: [Java download section](http://www.java.com/fr/download/manual.jsp)
  * Execute the downloaded file
  * You can check that a **Java\\jre7** folder has been installed at the location **C:\\Program Files\\**

In order for Java to be found by Windows, you may have to modify environment variables:

  * Go to the **Control Panel**
  * In the new window, go to **System**
  * On the left, click on **Advanced System parameters**
  * In the bottom, click on **Environment Variables**
  * In System Variables, choose to modify the **Path** variable
  * At the end, add **;C:\\Program Files\\Java\\jre7\\bin**

### On Ubuntu & Linux

To have a complete overview of java management on Ubuntu, have a look at:

  * [Ubuntu Java documentation](https://help.ubuntu.com/community/Java)
  * for French speaking users: http://doc.ubuntu-fr.org/java#installations_alternatives

Basically, you need to do:
```
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java7-installer
```

You can then switch between java version using:
```
sudo update-alternatives --config java
```

See [the troubleshooting page](G__Troubleshooting#Ubuntu) for more information on workaround for problems on Unbuntu.