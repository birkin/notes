+++
title = "installing wireshark"
date = 2008-03-08
description = "network-analyzer"
authors = []

[taxonomies]
tags=[ "installs", "tools" ]
+++

_[2023 update -- all this is ancient history. As of today, the standard Mac package-installer is [Homebrew](https://brew.sh/)]_

*[2008 note: This was like being back in school, where we did a bunch of 'compiling' and 'make'ing, and often took steps backwards, sometimes for a while, in order to go forward.]*

*[2008 update: tried the macport install again after a required library was back online; all proceeded smoothly.]*

---

Wanted to run [wireshark](http://en.wikipedia.org/wiki/Wireshark) (formerly ethereal) to check on something. Looks like Leopard install has moved it and other stuff around. Looking into getting it back up...

I've used Fink in the past to install linux packages that don't have mac binary versions, but have heard good things about [MacPorts](http://www.macports.org/) and am trying this (I did check and they do have a wireshark port.)

* Downloaded the universal installer for Leopard.

* Ran install. Though the documentation indicated that macports would automatically edit my .profile file; it didn't, so I added two paths to my .profile file:

        export PATH=$PATH:/opt/local/bin        
        export PATH=$PATH:/opt/local/var/macports/

* Looked good:

        birkinbox:~ birkin$         
        birkinbox:~ birkin$ which port        
        /opt/local/bin/port        
        birkinbox:~ birkin$         
        birkinbox:~ birkin$ sudo port selfupdate        
            
        MacPorts base version 1.600 installed        

        Downloaded MacPorts base version 1.600        
                
        The MacPorts installation is not outdated and so was not updated        
        selfupdate done!        
        birkinbox:~ birkin$ \r\n  \r\n  * wireshark found:\r\n          
        birkinbox:~ birkin$         
        birkinbox:~ birkin$ port search 'wireshark'        
        wireshark                      net/wireshark  0.99.8       Graphical network analyzer and capture tool        
        birkinbox:~ birkin$ \r\n    \r\n  * but install unsuccessful:\r\n          
        birkinbox:~ birkin$         
        birkinbox:~ birkin$ sudo port install 'wireshark'        
        Password:        
        --->  Fetching expat        
        --->  Attempting to fetch expat-2.0.1.tar.gz from http://downloads.sourceforge.net/expat        
        --->  Verifying checksum(s) for expat        
        --->  Extracting expat        
        --->  Configuring expat        
        Error: Target org.macports.configure returned: configure failure: shell command \" cd \"/opt/local/var/macports/build/_opt_local_var_macports_sources_rsync.macports.org_release_ports_textproc_expat/work/expat-2.0.1\" && ./configure --prefix=/opt/local --mandir=/opt/local/share/man \" returned error 77        
        Command output: checking build system type... i386-apple-darwin9.2.0        
        checking host system type... i386-apple-darwin9.2.0        
        checking for gcc... /usr/bin/gcc-4.0        
        checking for C compiler default output file name... configure: error: C compiler cannot create executables        
        See `config.log' for more details.        
                
        Error: The following dependencies failed to build: glib2 gettext expat libiconv gperf ncurses ncursesw pkgconfig gtk2 atk cairo fontconfig freetype zlib libpng render xrender gtk-doc docbook-xml-4.1.2 xmlcatmgr docbook-xsl libxml2 perl5.8 scrollkeeper docbook-xml docbook-xml-4.2 docbook-xml-4.3 docbook-xml-4.4 docbook-xml-4.5 libxslt p5-xml-parser jpeg pango Xft2 xorg-xproto xorg-util-macros shared-mime-info tiff libpcap openssl        
        Error: Status 1 encountered during processing.        
        birkinbox:~ birkin$ 

* Another step back to try and figure this out.

* 'Amer from Boston' _(link `http://www.anders.com/cms/241/Wireshark/MacPorts` no longer active)_, has some steps he said worked for him; I'll try them.

        sudo port -v install gtk2 +x11

        birkinbox:~ birkin$         
        birkinbox:~ birkin$ sudo port -v install gtk2 +x11        
        Password:        
        --->  Configuring expat        
        checking build system type... i386-apple-darwin9.2.0        
        checking host system type... i386-apple-darwin9.2.0        
        checking for gcc... /usr/bin/gcc-4.0        
        checking for C compiler default output file name... configure: error: C compiler cannot create executables        
        See `config.log' for more details.        
        Error: Target org.macports.configure returned: configure failure: shell command \" cd \"/opt/local/var/macports/build/_opt_local_var_macports_sources_rsync.macports.org_release_ports_textproc_expat/work/expat-2.0.1\" && ./configure --prefix=/opt/local --mandir=/opt/local/share/man \" returned error 77        
        Command output: checking build system type... i386-apple-darwin9.2.0        
        checking host system type... i386-apple-darwin9.2.0        
        checking for gcc... /usr/bin/gcc-4.0        
        checking for C compiler default output file name... configure: error: C compiler cannot create executables        
        See `config.log' for more details.        
                
        Warning: the following items did not execute (for expat): org.macports.activate org.macports.configure org.macports.build org.macports.destroot org.macports.install        
        Error: The following dependencies failed to build: atk gettext expat libiconv gperf ncurses ncursesw glib2 pkgconfig cairo fontconfig freetype zlib libpng render xrender gtk-doc docbook-xml-4.1.2 xmlcatmgr docbook-xsl libxml2 perl5.8 scrollkeeper docbook-xml docbook-xml-4.2 docbook-xml-4.3 docbook-xml-4.4 docbook-xml-4.5 libxslt p5-xml-parser jpeg pango Xft2 xorg-xproto xorg-util-macros shared-mime-info tiff        
        Error: Status 1 encountered during processing.        
        birkinbox:~ birkin$ 

* Consulting installation documentation _(bad link: http://trac.macports.org/projects/macports/wiki/InstallingMacPorts)_ from main documentation page _(bad link: http://trac.macports.org/projects/macports)_. Reading through the docs I see there's a lot I didn't do that I need to, but pretty basic stuff. This is good; it's always nice to have ideas about why something's not working.
  
* xcode 3.0 is required; I thought I had installed that when I installed Leopard, but there's no /Developer directory in the new installation (only one is in the 'Previous Systems' directory) so I must not have. Downloading the (big) intaller.
  
* The modified date on the Utilities/X11.app is 2008-02-29, which is when I installed Leopard. So I suspect that the selection I remember on the install was for the X11 install, not the whole xcode package.
  
* Hmmn... the macports xcode-installation docs say _"Click Customize, expand the Applications category and click the checkbox beside X11 SDK to add it to the default items."_ ...but the xcode installer didn't have an Applications category; proceeding with install.
  
* Looks like it went ok.  
  
* Looks like a good source of Leopard X11 info _(bad link: http://homepage.mac.com/sao1/X11/index.html)_.  
  
* Based on intall docs, revised `~/.profile` to:

        # for macport install (2008-03-21)        
        export PATH=/opt/local/bin:/opt/local/sbin:$PATH        
        export DISPLAY=:0.0

* The 'Verify the shell environment' section instructs to run 'env' to confirm that the initial paths are the MacPort paths, like:

        PATH=/opt/local/bin:/opt/local/sbin:/bin:/sbin:/usr/bin:/usr/sbin  

* My path has the old '/sw/' paths previously installed via Fink:

        birkinbox:~ birkin$         
        birkinbox:~ birkin$ env        
        ...        
        PATH=/sw/bin:/sw/sbin::/usr/lib/php/:/opt/local/bin:/opt/local/sbin:/usr/bin:/bin:/usr/sbin:...        
        ...        
        birkinbox:~ birkin$ 

* Ok, disabled the fink stuff; the php lib still comes before the macport directories, but I'm thinking that's ok. Onward...

* Trying the wireshark install again... OMG, I'm over an hour into the install command and stuff's still being downloaded and installed. Is this a natural series of dependencies? Or is an entire 'base' environment being installed? I now seem to remember something similar with Fink. It's not at all necessary to list all this output, but I'm going to, for the strange geeky factor, and because over the years I've been occasionlly been surprised at the benefits of having this bizarre documentation.   

        birkinbox:~ birkin$         
        birkinbox:~ birkin$ sudo port install 'wireshark'        
        Password:        
        --->  Configuring expat        
        --->  Building expat with target all        
        --->  Staging expat into destroot        
        --->  Installing expat 2.0.1_0        
        --->  Activating expat 2.0.1_0        
        --->  Cleaning expat        
        --->  Fetching libiconv        
        --->  Attempting to fetch libiconv-1.12.tar.gz from http://ftp.gnu.org/gnu/libiconv        
        --->  Verifying checksum(s) for libiconv        
        --->  Extracting libiconv        
        --->  Applying patches to libiconv        
        --->  Configuring libiconv        
        --->  Building libiconv with target all        
        --->  Staging libiconv into destroot        
        --->  Installing libiconv 1.12_0        
        --->  Activating libiconv 1.12_0        
        --->  Cleaning libiconv        
        --->  Fetching ncursesw        
        --->  Attempting to fetch ncurses-5.6.tar.gz from http://ftp.gnu.org/gnu/ncurses        
        --->  Verifying checksum(s) for ncursesw        
        --->  Extracting ncursesw        
        --->  Applying patches to ncursesw        
        --->  Configuring ncursesw        
        --->  Building ncursesw with target all        
        --->  Staging ncursesw into destroot        
        --->  Installing ncursesw 5.6_1        
        --->  Activating ncursesw 5.6_1        
        --->  Cleaning ncursesw        
        --->  Fetching ncurses        
        --->  Verifying checksum(s) for ncurses        
        --->  Extracting ncurses        
        --->  Applying patches to ncurses        
        --->  Configuring ncurses        
        --->  Building ncurses with target all        
        --->  Staging ncurses into destroot        
        --->  Installing ncurses 5.6_0        
        --->  Activating ncurses 5.6_0        
        --->  Cleaning ncurses        
        --->  Fetching gettext        
        --->  Attempting to fetch gettext-0.17.tar.gz from http://ftp.gnu.org/gnu/gettext        
        --->  Verifying checksum(s) for gettext        
        --->  Extracting gettext        
        --->  Applying patches to gettext        
        --->  Configuring gettext        
        --->  Building gettext with target all        
        --->  Staging gettext into destroot        
        --->  Installing gettext 0.17_3        
        --->  Activating gettext 0.17_3        
        --->  Cleaning gettext        
        --->  Fetching pkgconfig        
        --->  Attempting to fetch pkg-config-0.23.tar.gz from http://pkg-config.freedesktop.org/releases/        
        --->  Verifying checksum(s) for pkgconfig        
        --->  Extracting pkgconfig        
        --->  Configuring pkgconfig        
        --->  Building pkgconfig with target all        
        --->  Staging pkgconfig into destroot        
        --->  Installing pkgconfig 0.23_0        
        --->  Activating pkgconfig 0.23_0        
        --->  Cleaning pkgconfig        
        --->  Fetching glib2        
        --->  Attempting to fetch glib-2.16.1.tar.bz2 from ftp://ftp.gtk.org/pub/glib/2.16/        
        --->  Attempting to fetch glib-2.16.1.tar.bz2 from http://mandril.creatis.insa-lyon.fr/linux/gnome.org/sources/glib/2.16/        
        --->  Verifying checksum(s) for glib2        
        --->  Extracting glib2        
        --->  Applying patches to glib2        
        --->  Configuring glib2        
        --->  Building glib2 with target all        
        --->  Staging glib2 into destroot        
        --->  Installing glib2 2.16.1_0+darwin_9        
        --->  Activating glib2 2.16.1_0+darwin_9        
        --->  Cleaning glib2        
        --->  Fetching atk        
        --->  Attempting to fetch atk-1.22.0.tar.bz2 from http://mandril.creatis.insa-lyon.fr/linux/gnome.org/sources/atk/1.22/        
        --->  Verifying checksum(s) for atk        
        --->  Extracting atk        
        --->  Configuring atk        
        --->  Building atk with target all        
        --->  Staging atk into destroot        
        --->  Installing atk 1.22.0_1        
        --->  Activating atk 1.22.0_1        
        --->  Cleaning atk        
        --->  Fetching zlib        
        --->  Attempting to fetch zlib-1.2.3.tar.bz2 from http://www.zlib.net/        
        --->  Verifying checksum(s) for zlib        
        --->  Extracting zlib        
        --->  Applying patches to zlib        
        --->  Configuring zlib        
        --->  Building zlib with target all        
        --->  Staging zlib into destroot        
        --->  Installing zlib 1.2.3_1        
        --->  Activating zlib 1.2.3_1        
        --->  Cleaning zlib        
        --->  Fetching freetype        
        --->  Attempting to fetch freetype-2.3.5.tar.bz2 from http://download.savannah.gnu.org/releases/freetype/        
        --->  Verifying checksum(s) for freetype        
        --->  Extracting freetype        
        --->  Applying patches to freetype        
        --->  Configuring freetype        
        --->  Building freetype with target all        
        --->  Staging freetype into destroot        
        --->  Installing freetype 2.3.5_1        
        --->  Activating freetype 2.3.5_1        
        --->  Cleaning freetype        
        --->  Fetching fontconfig        
        --->  Attempting to fetch fontconfig-2.5.0.tar.gz from http://fontconfig.org/release/        
        --->  Verifying checksum(s) for fontconfig        
        --->  Extracting fontconfig        
        --->  Configuring fontconfig        
        --->  Building fontconfig with target all        
        --->  Staging fontconfig into destroot        
        --->  Installing fontconfig 2.5.0_0+macosx        
        --->  Activating fontconfig 2.5.0_0+macosx        
        --->  Cleaning fontconfig        
        --->  Fetching libpng        
        --->  Attempting to fetch libpng-1.2.25.tar.bz2 from http://downloads.sourceforge.net/libpng        
        --->  Verifying checksum(s) for libpng        
        --->  Extracting libpng        
        --->  Configuring libpng        
        --->  Building libpng with target all        
        --->  Staging libpng into destroot        
        --->  Installing libpng 1.2.25_0        
        --->  Activating libpng 1.2.25_0        
        --->  Cleaning libpng        
        --->  Fetching render        
        --->  Attempting to fetch renderext-0.9.tar.bz2 from http://xlibs.freedesktop.org/release/        
        --->  Verifying checksum(s) for render        
        --->  Extracting render        
        --->  Configuring render        
        --->  Building render with target all        
        --->  Staging render into destroot        
        --->  Installing render 0.9_1        
        --->  Activating render 0.9_1        
        --->  Cleaning render        
        --->  Fetching xrender        
        --->  Attempting to fetch libXrender-0.9.0.tar.bz2 from http://xlibs.freedesktop.org/release/        
        --->  Verifying checksum(s) for xrender        
        --->  Extracting xrender        
        --->  Configuring xrender        
        --->  Building xrender with target all        
        --->  Staging xrender into destroot        
        --->  Installing xrender 0.9.0_2        
        --->  Activating xrender 0.9.0_2        
        --->  Cleaning xrender        
        --->  Fetching cairo        
        --->  Attempting to fetch cairo-1.4.14.tar.gz from http://cairographics.org/releases/        
        --->  Verifying checksum(s) for cairo        
        --->  Extracting cairo        
        --->  Configuring cairo        
        --->  Building cairo with target all        
        --->  Staging cairo into destroot        
        --->  Installing cairo 1.4.14_0        
        --->  Activating cairo 1.4.14_0        
        --->  Cleaning cairo        
        --->  Fetching xmlcatmgr        
        --->  Attempting to fetch xmlcatmgr-2.2.tar.gz from ftp://ftp.FreeBSD.org/pub/FreeBSD/ports/distfiles/        
        --->  Verifying checksum(s) for xmlcatmgr        
        --->  Extracting xmlcatmgr        
        --->  Configuring xmlcatmgr        
        --->  Building xmlcatmgr with target all        
        --->  Staging xmlcatmgr into destroot        
        --->  Installing xmlcatmgr 2.2_1        
        --->  Activating xmlcatmgr 2.2_1        
        --->  Cleaning xmlcatmgr        
        --->  Fetching docbook-xml-4.1.2        
        --->  Attempting to fetch docbkx412.zip from http://www.oasis-open.org/docbook/xml/4.1.2/        
        --->  Verifying checksum(s) for docbook-xml-4.1.2        
        --->  Extracting docbook-xml-4.1.2        
        --->  Configuring docbook-xml-4.1.2        
        --->  Building docbook-xml-4.1.2 with target all        
        --->  Staging docbook-xml-4.1.2 into destroot        
        --->  Installing docbook-xml-4.1.2 4.1.2_1        
        --->  Activating docbook-xml-4.1.2 4.1.2_1        
        ######################################################################        
        # As MacPorts does not currently have a post-deactivate hook,         
        # you will need to ensure that you manually remove the catalog         
        # entry for this port when you uninstall it.  To do so, run         
        # \"xmlcatmgr remove nextCatalog /opt/local/share/xml/docbook/4.1.2/catalog.xml\".        
        ######################################################################        
        --->  Cleaning docbook-xml-4.1.2        
        --->  Fetching docbook-xsl        
        --->  Attempting to fetch docbook-xsl-1.72.0.tar.bz2 from http://downloads.sourceforge.net/docbook        
        --->  Verifying checksum(s) for docbook-xsl        
        --->  Extracting docbook-xsl        
        --->  Configuring docbook-xsl        
        --->  Building docbook-xsl with target all        
        --->  Staging docbook-xsl into destroot        
        --->  Installing docbook-xsl 1.72.0_0        
        --->  Activating docbook-xsl 1.72.0_0        
        ######################################################################        
        # As MacPorts does not currently have a post-deactivate hook,         
        # you will need to ensure that you manually remove the catalog         
        # entry for this port when you uninstall it.  To do so, run         
        # \"xmlcatmgr remove nextCatalog /opt/local/share/xsl/docbook-xsl/catalog.xml\".        
        ######################################################################        
        --->  Cleaning docbook-xsl        
        --->  Fetching libxml2        
        --->  Attempting to fetch libxml2-2.6.31.tar.gz from http://xmlsoft.org/sources/        
        --->  Verifying checksum(s) for libxml2        
        --->  Extracting libxml2        
        --->  Configuring libxml2        
        --->  Building libxml2 with target all        
        --->  Staging libxml2 into destroot        
        --->  Installing libxml2 2.6.31_0        
        --->  Activating libxml2 2.6.31_0        
        --->  Cleaning libxml2        
        --->  Fetching perl5.8        
        --->  Attempting to fetch perl-5.8.8.tar.bz2 from http://www.cpan.org/src/5.0/        
        --->  Verifying checksum(s) for perl5.8        
        --->  Extracting perl5.8        
        --->  Applying patches to perl5.8        
        --->  Configuring perl5.8        
        --->  Building perl5.8 with target all        
        --->  Staging perl5.8 into destroot        
        --->  Installing perl5.8 5.8.8_2        
        --->  Activating perl5.8 5.8.8_2        
        --->  Cleaning perl5.8        
        --->  Fetching docbook-xml-4.2        
        --->  Attempting to fetch docbook-xml-4.2.zip from http://www.oasis-open.org/docbook/xml/4.2/        
        --->  Verifying checksum(s) for docbook-xml-4.2        
        --->  Extracting docbook-xml-4.2        
        --->  Configuring docbook-xml-4.2        
        --->  Building docbook-xml-4.2 with target all        
        --->  Staging docbook-xml-4.2 into destroot        
        --->  Installing docbook-xml-4.2 4.2_0        
        --->  Activating docbook-xml-4.2 4.2_0        
        ######################################################################        
        # As MacPorts does not currently have a post-deactivate hook,         
        # you will need to ensure that you manually remove the catalog         
        # entry for this port when you uninstall it.  To do so, run         
        # \"xmlcatmgr remove nextCatalog /opt/local/share/xml/docbook/4.2/catalog.xml\".        
        ######################################################################        
        --->  Cleaning docbook-xml-4.2        
        --->  Fetching docbook-xml-4.3        
        --->  Attempting to fetch docbook-xml-4.3.zip from http://www.oasis-open.org/docbook/xml/4.3/        
        --->  Verifying checksum(s) for docbook-xml-4.3        
        --->  Extracting docbook-xml-4.3        
        --->  Configuring docbook-xml-4.3        
        --->  Building docbook-xml-4.3 with target all        
        --->  Staging docbook-xml-4.3 into destroot        
        --->  Installing docbook-xml-4.3 4.3_0        
        --->  Activating docbook-xml-4.3 4.3_0        
        ######################################################################        
        # As MacPorts does not currently have a post-deactivate hook,         
        # you will need to ensure that you manually remove the catalog         
        # entry for this port when you uninstall it.  To do so, run         
        # \"xmlcatmgr remove nextCatalog /opt/local/share/xml/docbook/4.3/catalog.xml\".        
        ######################################################################        
        --->  Cleaning docbook-xml-4.3        
        --->  Fetching docbook-xml-4.4        
        --->  Attempting to fetch docbook-xml-4.4.zip from http://www.oasis-open.org/docbook/xml/4.4/        
        --->  Verifying checksum(s) for docbook-xml-4.4        
        --->  Extracting docbook-xml-4.4        
        --->  Configuring docbook-xml-4.4        
        --->  Building docbook-xml-4.4 with target all        
        --->  Staging docbook-xml-4.4 into destroot        
        --->  Installing docbook-xml-4.4 4.4_0        
        --->  Activating docbook-xml-4.4 4.4_0        
        ######################################################################        
        # As MacPorts does not currently have a post-deactivate hook,         
        # you will need to ensure that you manually remove the catalog         
        # entry for this port when you uninstall it.  To do so, run         
        # \"xmlcatmgr remove nextCatalog /opt/local/share/xml/docbook/4.4/catalog.xml\".        
        ######################################################################        
        --->  Cleaning docbook-xml-4.4        
        --->  Fetching docbook-xml-4.5        
        --->  Attempting to fetch docbook-xml-4.5.zip from http://www.oasis-open.org/docbook/xml/4.5/        
        --->  Verifying checksum(s) for docbook-xml-4.5        
        --->  Extracting docbook-xml-4.5        
        --->  Configuring docbook-xml-4.5        
        --->  Building docbook-xml-4.5 with target all        
        --->  Staging docbook-xml-4.5 into destroot        
        --->  Installing docbook-xml-4.5 4.5_0        
        --->  Activating docbook-xml-4.5 4.5_0        
        ######################################################################        
        # As MacPorts does not currently have a post-deactivate hook,         
        # you will need to ensure that you manually remove the catalog         
        # entry for this port when you uninstall it.  To do so, run         
        # \"xmlcatmgr remove nextCatalog /opt/local/share/xml/docbook/4.5/catalog.xml\".        
        ######################################################################        
        --->  Cleaning docbook-xml-4.5        
        --->  Fetching docbook-xml        
        --->  Verifying checksum(s) for docbook-xml        
        --->  Extracting docbook-xml        
        --->  Configuring docbook-xml        
        --->  Building docbook-xml with target all        
        --->  Staging docbook-xml into destroot        
        --->  Installing docbook-xml 4.5_1        
        --->  Activating docbook-xml 4.5_1        
        --->  Cleaning docbook-xml        
        --->  Fetching libxslt        
        --->  Attempting to fetch libxslt-1.1.22.tar.gz from ftp://xmlsoft.org/libxslt/        
        --->  Verifying checksum(s) for libxslt        
        --->  Extracting libxslt        
        --->  Configuring libxslt        
        --->  Building libxslt with target all        
        --->  Staging libxslt into destroot        
        --->  Installing libxslt 1.1.22_0        
        --->  Activating libxslt 1.1.22_0        
        --->  Cleaning libxslt        
        --->  Fetching p5-xml-parser        
        --->  Attempting to fetch XML-Parser-2.36.tar.gz from http://ftp.ucr.ac.cr/Unix/CPAN/modules/by-module/XML        
        --->  Verifying checksum(s) for p5-xml-parser        
        --->  Extracting p5-xml-parser        
        --->  Configuring p5-xml-parser        
        --->  Building p5-xml-parser with target all        
        --->  Staging p5-xml-parser into destroot        
        --->  Installing p5-xml-parser 2.36_0        
        --->  Activating p5-xml-parser 2.36_0        
        --->  Cleaning p5-xml-parser        
        --->  Fetching scrollkeeper        
        --->  Attempting to fetch scrollkeeper-0.3.14.tar.gz from http://downloads.sourceforge.net/scrollkeeper        
        --->  Verifying checksum(s) for scrollkeeper        
        --->  Extracting scrollkeeper        
        --->  Applying patches to scrollkeeper        
        --->  Configuring scrollkeeper        
        --->  Building scrollkeeper with target all        
        --->  Staging scrollkeeper into destroot        
        --->  Installing scrollkeeper 0.3.14_6        
        --->  Activating scrollkeeper 0.3.14_6        
        --->  Cleaning scrollkeeper        
        --->  Fetching gtk-doc        
        --->  Attempting to fetch gtk-doc-1.9.tar.bz2 from http://mandril.creatis.insa-lyon.fr/linux/gnome.org/sources/gtk-doc/1.9/        
        --->  Verifying checksum(s) for gtk-doc        
        --->  Extracting gtk-doc        
        --->  Configuring gtk-doc        
        --->  Building gtk-doc with target all        
        --->  Staging gtk-doc into destroot        
        --->  Installing gtk-doc 1.9_1        
        --->  Activating gtk-doc 1.9_1        
        --->  Cleaning gtk-doc        
        --->  Fetching jpeg        
        --->  Attempting to fetch jpegsrc.v6b.tar.gz from http://www.ijg.org/files        
        --->  Attempting to fetch droppatch.tar.gz from http://sylvana.net/jpegcrop/        
        --->  Verifying checksum(s) for jpeg        
        --->  Extracting jpeg        
        --->  Applying patches to jpeg        
        --->  Configuring jpeg        
        --->  Building jpeg with target all        
        --->  Staging jpeg into destroot        
        --->  Installing jpeg 6b_2        
        --->  Activating jpeg 6b_2        
        --->  Cleaning jpeg        
        --->  Fetching xorg-util-macros        
        --->  Attempting to fetch util-macros-1.1.5.tar.bz2 from http://www.x.org/pub/individual/util/        
        --->  Verifying checksum(s) for xorg-util-macros        
        --->  Extracting xorg-util-macros        
        --->  Configuring xorg-util-macros        
        --->  Building xorg-util-macros with target all        
        --->  Staging xorg-util-macros into destroot        
        --->  Installing xorg-util-macros 1.1.5_0        
        --->  Activating xorg-util-macros 1.1.5_0        
        --->  Cleaning xorg-util-macros        
        --->  Fetching xorg-xproto        
        --->  Attempting to fetch xproto-7.0.11.tar.bz2 from http://www.x.org/pub/individual/proto/        
        --->  Verifying checksum(s) for xorg-xproto        
        --->  Extracting xorg-xproto        
        --->  Applying patches to xorg-xproto        
        --->  Configuring xorg-xproto        
        --->  Building xorg-xproto with target all        
        --->  Staging xorg-xproto into destroot        
        --->  Installing xorg-xproto 7.0.11_1        
        --->  Activating xorg-xproto 7.0.11_1        
        --->  Cleaning xorg-xproto        
        --->  Fetching Xft2        
        --->  Attempting to fetch libXft-2.1.12.tar.bz2 from http://xorg.freedesktop.org/releases/individual/lib/        
        --->  Verifying checksum(s) for Xft2        
        --->  Extracting Xft2        
        --->  Configuring Xft2        
        --->  Building Xft2 with target all        
        --->  Staging Xft2 into destroot        
        --->  Installing Xft2 2.1.12_0        
        --->  Activating Xft2 2.1.12_0        
        --->  Cleaning Xft2        
        --->  Fetching pango        
        --->  Attempting to fetch pango-1.20.0.tar.bz2 from http://mandril.creatis.insa-lyon.fr/linux/gnome.org/sources/pango/1.20        
        --->  Verifying checksum(s) for pango        
        --->  Extracting pango        
        --->  Applying patches to pango        
        --->  Configuring pango        
        --->  Building pango with target all        
        --->  Staging pango into destroot        
        --->  Installing pango 1.20.0_0        
        --->  Activating pango 1.20.0_0        
        --->  Cleaning pango        
        --->  Fetching shared-mime-info        
        --->  Attempting to fetch shared-mime-info-0.23.tar.bz2 from http://people.freedesktop.org/~hadess/        
        --->  Verifying checksum(s) for shared-mime-info        
        --->  Extracting shared-mime-info        
        --->  Configuring shared-mime-info        
        --->  Building shared-mime-info with target all        
        --->  Staging shared-mime-info into destroot        
        --->  Installing shared-mime-info 0.23_1        
        --->  Activating shared-mime-info 0.23_1        
        --->  Cleaning shared-mime-info        
        --->  Fetching tiff        
        --->  Attempting to fetch tiff-3.8.2.tar.gz from ftp://ftp.remotesensing.org/pub/libtiff/        
        --->  Verifying checksum(s) for tiff        
        --->  Extracting tiff        
        --->  Configuring tiff        
        --->  Building tiff with target all        
        --->  Staging tiff into destroot        
        --->  Installing tiff 3.8.2_1+macosx        
        --->  Activating tiff 3.8.2_1+macosx        
        --->  Cleaning tiff        
        --->  Fetching gtk2        
        --->  Attempting to fetch gtk+-2.12.9.tar.bz2 from http://mandril.creatis.insa-lyon.fr/linux/gnome.org/sources/gtk+/2.12/        
        --->  Verifying checksum(s) for gtk2        
        --->  Extracting gtk2        
        --->  Applying patches to gtk2        
        --->  Configuring gtk2        
        --->  Building gtk2 with target all        
        --->  Staging gtk2 into destroot        
        --->  Installing gtk2 2.12.9_0+x11        
        --->  Activating gtk2 2.12.9_0+x11        
        --->  Cleaning gtk2        
        --->  Fetching libpcap        
        --->  Attempting to fetch libpcap-0.9.8.tar.gz from http://www.tcpdump.org/release/        
        --->  Attempting to fetch libpcap-0.9.8.tar.gz from http://svn.macports.org/repository/macports/distfiles/libpcap        
        --->  Attempting to fetch libpcap-0.9.8.tar.gz from http://svn.macports.org/repository/macports/distfiles/general/        
        --->  Attempting to fetch libpcap-0.9.8.tar.gz from http://svn.macports.org/repository/macports/downloads/libpcap        
        --->  Attempting to fetch libpcap-0.9.8.tar.gz from http://svn.macports.org/repository/macports/distfiles/libpcap        
        --->  Attempting to fetch libpcap-0.9.8.tar.gz from http://svn.macports.org/repository/macports/distfiles/general/        
        --->  Attempting to fetch libpcap-0.9.8.tar.gz from http://svn.macports.org/repository/macports/downloads/libpcap        
        Error: Target org.macports.fetch returned: fetch failed        
        Error: The following dependencies failed to build: libpcap openssl        
        Error: Status 1 encountered during processing.        
        birkinbox:~ birkin$ 

* Tried an install of libpcap directly and it failed the same way.

* Posted a message to the MacPorts listserve _(bad link: http://lists.macosforge.org/mailman/listinfo.cgi/macports-users)_  , and got back a helpful suggestion to get libpcap from SfR-fresh _(bad link: http://www.sfr-fresh.com/unix/misc/libpcap-0.9.8.tar.gz/)_, and put it at:

        /opt/local/var/macports/distfiles/libpcap/

* Whew. Will do, but first: going to bed again.    :)

* *Two weeks later...*

* Figured I'd just try the standard way again...

        birkinbox:~ birkin$   

        birkinbox:~ birkin$ sudo port install wireshark        
        Portfile changed since last build; discarding previous state.        
        --->  Fetching libpcap        
        --->  Attempting to fetch libpcap-0.9.8.tar.gz from http://www.tcpdump.org/release/        
        --->  Verifying checksum(s) for libpcap        
        --->  Extracting libpcap        
        --->  Applying patches to libpcap        
        --->  Configuring libpcap        
        --->  Building libpcap with target all        
        --->  Staging libpcap into destroot        
        --->  Installing libpcap 0.9.8_0        
        --->  Activating libpcap 0.9.8_0        
        --->  Cleaning libpcap        
        --->  Fetching wireshark        
        --->  Attempting to fetch wireshark-1.0.0.tar.bz2 from http://www.wireshark.org/download/src/        
        --->  Verifying checksum(s) for wireshark        
        --->  Extracting wireshark        
        --->  Configuring wireshark        
        --->  Building wireshark with target all        
        --->  Staging wireshark into destroot        
        --->  Installing wireshark 1.0.0_0+darwin_9        
        --->  Activating wireshark 1.0.0_0+darwin_9        
        --->  Cleaning wireshark        
        birkinbox:~ birkin$

* Life is good!