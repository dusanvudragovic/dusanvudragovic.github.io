---
title:  HP LaserJet 1000 on OS X Mavericks
layout: default
---

[HP LaserJet 1000](http://h20565.www2.hp.com/portal/site/hpsc/template.PAGE/public/psi/swdHome?sp4ts.oid=45675&ac.admitted=1406812827187.876444892.492883150) is an old printer model that is not supported on [Mac OS X](https://www.apple.com/osx/). However, using [foo2zjs](http://foo2zjs.rkkda.com/) printer driver for [ZjStream protocol](http://www.undocprint.org/formats/page_description_languages/zjstream) it is possible to configure [OS X Mavericks](https://www.apple.com/osx/) (as well as [Snow Leopard](http://www.apple.com/support/snowleopard/), [Lion](http://www.apple.com/support/lion/), and [Mountain Lion](http://www.apple.com/support/osx/mountainlion/)) to support [HP LaserJet 1000](http://h20565.www2.hp.com/portal/site/hpsc/template.PAGE/public/psi/swdHome?sp4ts.oid=45675&ac.admitted=1406812827187.876444892.492883150). Here are instructions on how to set it up.

[Foo2zjs](http://foo2zjs.rkkda.com/) is an open source printer driver, and it is recommended not to use precompiled packages, but to compile from the source tarball provided at [foo2zjs](http://foo2zjs.rkkda.com/) home page. Therefore, before you actually compile it, make sure to have [Xcode](https://developer.apple.com/xcode/) installed. [Xcode](https://developer.apple.com/xcode/) is a package provided by [Apple](http://www.apple.com/) containing compilers, libraries and additional tools required to develop and compile applications for [Mac OS X](https://www.apple.com/osx/). The latest version of [Xcode](https://developer.apple.com/xcode/) is available at [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835), but it could be also downloaded from the [Apple developer website](https://developer.apple.com/downloads/). Once [Xcode](https://developer.apple.com/xcode/) is installed, from the [Terminal application](http://en.wikipedia.org/wiki/Terminal_(OS_X)) (```/Applications/Utilities/Terminal.app```) command line, run:

```bash
    $ xcode-select --install
```

and click the __Install__ button to install the required command line developer tools. The same tools could be downloaded from the [Apple developer website](https://developer.apple.com/downloads/) as well.

Beside [Xcode](https://developer.apple.com/xcode/), since [foo2zjs](http://foo2zjs.rkkda.com/) building process is based on [Makefile](http://www.gnu.org/prep/standards/html_node/Makefile-Conventions.html), a few additional command line tools ([autoconf](https://www.gnu.org/software/autoconf/), [automake](https://www.gnu.org/software/automake/), [wget](https://www.gnu.org/software/wget/), and [gsed](https://www.gnu.org/software/gsed/)) have to be installed. Also, since the driver uses [Ghostscript](http://www.ghostscript.com/) (PostScript and PDF interpreter) to perform image processing, this application is required as well. Installation of all these applications could be easily done via [MacPorts](https://www.macports.org/) open-source software installer system. [Mac OS X](https://www.apple.com/osx/) package installer provided at [MacPorts](https://www.macports.org/) home page, automatically installs [MacPorts](https://www.macports.org/), sets the shell environment, and runs a selfupdate operation to update the ports tree and [MacPorts](https://www.macports.org/) base with the latest release. To confirm the installation is working as expected, from the [Terminal application](http://en.wikipedia.org/wiki/Terminal_(OS_X)), run:

```bash
    $ port version
```

Using [MacPorts](https://www.macports.org/) main utility, ```port``` command, [Ghostscript](http://www.ghostscript.com/) and additional command line tools ([autoconf](https://www.gnu.org/software/autoconf/) and [automake](https://www.gnu.org/software/automake/) are provided within [coreutils](https://www.macports.org/ports.php?by=library&substr=coreutils) package) can be installed with the following command:

```bash
    $ sudo port install ghostscript coreutils wget gsed
```

[Foo2zjs](http://foo2zjs.rkkda.com/) uses [Foomatic](http://www.linuxfoundation.org/collaborate/workgroups/openprinting/databasefoomatic) scripts to convert the incoming PostScript data into the printer's native format. Fortunately, [Foomatic](http://www.linuxfoundation.org/collaborate/workgroups/openprinting/databasefoomatic) package installer are provided by the [Linux Foundation](http://www.linuxfoundation.org) and it could be downloaded from [http://www.linuxfoundation.org/collaborate/workgroups/openprinting/macosxfoomatic](http://www.linuxfoundation.org/collaborate/workgroups/openprinting/macosxfoomatic).

Now proceed with [foo2zjs](http://foo2zjs.rkkda.com/) printer driver installation by following these steps:

 - Change home directory:

    ```bash
        $ cd /tmp
    ``` 

 - Download [foo2zjs](http://foo2zjs.rkkda.com/) source tarball :

    ```bash
        $ wget http://foo2zjs.rkkda.com/foo2zjs.tar.gz
    ``` 

 - Extract all files from the tarball:

    ```bash
        $ tar zxvf foo2zjs.tar.gz
    ``` 

 - Go to the extracted directory:

    ```bash
        $ cd foo2zjs
    ``` 

 - Compile [foo2zjs](http://foo2zjs.rkkda.com/) source:

    ```bash
        $ make
    ``` 
 - Download HP LaserJet 1000 firmware file:

    ```bash
        $ ./getweb 1000
    ``` 

 - Download [foo2zjs](http://foo2zjs.rkkda.com/) printer driver:

    ```bash
        $ sudo make install
    ``` 

 - Optionally (but recommended), install hot-plug utility that loads the firmware automatically when the printer is plugged in (or turned on):

    ```bash
        $ sudo make install-hotplug
    ```

    Otherwise, with the following command the firmware file has to be sent manually each time the printer is powered on:

    ```bash
        $ sudo lp -oraw /usr/share/foo2zjs/firmware/sihp1000.dl
    ```

If all steps passed successfully, add the printer (HP LaserJet 1000 Foomatic/foo2zjs) via Printers & Scanners pane in System Preferences. 
