+++
title = "ssh tunneling notes"
date = 2006-02-02
description = "useful for local development"
authors = []

[taxonomies]
tags=[ "ssh_tunneling", "presentations", "techniques" ]
+++

---

_This was first posted in 2006, to a no-longer-accessible wiki, to accompany a "Brown Internet Programming Group" talk I gave._

---

### The problem

The situation: My preferred way of working is to program, on my laptop, code that often must communicate with a database running on a remote server. What are good ways of handling this?
In the past I used two different approaches.

* Run a parallel database.
    * Pros: good when lots of database development/reconfiguration is required. No separate connection file is needed.
    * Cons: testing may lead to need to spend effort keeping database structures and sometimes data in sync.
* Access the remote database by programming the connection-code to determine which host its running on. If running on my laptop, the connection-code would locate the database at an internet address; if running on the same server as the database, the connection-code would locate the database at the localhost address.
    * Pros: Only need to deal with one database.
    * Cons: Non-localhost connectivity may be disabled for security reasons. If others work on the same code, the differing connection-code to detect multiple hosts can be a hassle and can reveal internet passwords. Care must be taken since the password may be transmitted over a non-secure connection.

*Solution:* Another programmer showed me how he solves this issue via ssh-tunneling. It's a wonderful solution.

### Overview

Background info to keep in mind: Common client-server internet connections generally generally do not require specification of originating ports (the computers can pick a port), but do require specification of destination ports.

Example: my browser wants to access a web-page. My browser may send out the http request from any of a range of ports, but will specifically access the server's IP address at port 80, where the web-server is listening.

In ssh-tunneling, the client computer is set up to 'listen' for incoming data on a specified port at the 127.0.0.1 localhost IP address -- and to 'forward' that data, via a pre-established ssh connection, to a specific port at the server's IP address. This terminology may be a bit confusing, because the 'client' -- say, the local development laptop -- is 'listening', which a 'server' normally does. In this case, think of the server as a remote database-server.

What this means for my database situation is that I set up my laptop to listen for incoming data at '127.0.0.1:3306' and to forward that data to 'somehost.services.brown.edu:3306'. All I have to do in my connection code is specify that it attempt to connect to the database at '127.0.0.1:3306'.

The beauty of this is two-fold...

First, the same connection code can run on my laptop and on the server with no modification at all. Example of php connection code...

```php
<?php
    mysql_connect(\"127.0.0.1:3306\", \"username\", \"password\") or die (\"Sorry, cannot connect to server\");
    mysql_select_db(\"databasename\") or die (\"Sorry, cannnot connect to database\");
?>
```

Second, because the 'set up' is using SSH as the fowarding mechanism, all data is transferred securely.

Note that there are many different ways of tunneling; this page focuses on one: 'local client' to 'remote service' (in this case, a remote database server).

### Setting up the tunnel

#### Unices

On Linux, Unix, and the Mac, setting up a tunnel is as easy as issuing one command in a terminal window:

    ssh -N -L 3306:somehost.services.brown.edu:3306 myaccount@somehost.services.brown.edu

Even if you're going to use a GUI client to set up the tunnel, examine the details of this command to get an understanding of what's going on:

* The ssh part is the normal secure-shell command.
* The -N flag specifies that commands flowing over this connection won't be executed on the remote computer, just forwarded.
* The -L flag specifies the details of the 'localPort:remoteHost:remotePort' section that follows this flag. It means that the local computer should listen for incoming connections on the specified localPort, and forward them over the ssh connection to the remote computer at the remotePort.
* The 'myaccount@somehost.services.brown.edu' sets up the ssh connection. This prompts me to enter my account-password on the remote computer 'somehost'.

#### Mac: Fugu

Fugu is an open-source ssh client that supports ssh tunneling.

To set up a tunnel in fugu:

* Select 'SSH' -> 'New SSH Tunnel'
* Enter 'somehost.services.brown.edu' in the 'Create Tunnel to' textbox'.
* Enter '3306' in the 'Service or Port' textbox (think of this as the 'Remote Port').
* Enter '3306' in the 'Local Port' textbox.
* Enter 'somehost.services.brown.edu' in the 'Remote Host' textbox.
    * I'm not sure of the distinction between the two 'host' textboxes, but entering info this way works.
* Enter your username in the 'Username' textbox.
* Enter '22' in the 'Port' textbox (think of this as the 'SSH Port').

#### Windows: Putty

[Putty](http://software.brown.edu/dist/w-putty.html) is a free Brown-offered ssh client that supports tunneling.

* Open 'putty.exe' file. The 'PuTTy Configuration' window appears.
* Click once on 'Category' -> 'Session'.
* On the right-side of the window enter 'somehost.services.brown.edu' in the 'Host Name (or IP address)' textbox.
* Enter '22' in the 'Port' textbox.
* Select 'SSH' for the 'Protocol'.
* Click once on 'Category' -> 'SSH' -> 'Tunnels'.
* Enter '3306' in the 'Source port' textbox.
* Enter 'somehost.services.brown.edu:3306' in the 'Destination' textbox.
* Select the 'Remote' radio-button under the 'Destination' textbox.
* Click the 'Add' button.
* Click the 'Open' button. The putty terminal window opens.
* When prompted by 'login as', enter your username and hit return.
* When prompted by for your password, enter it and hit return.
* That's it; the tunnel is established.

### More tunnel fun

#### Web

The idea...

    ssh -N -L 5005:123.123.123.123:80 myaccount@123.123.123.123

To implement this in Fugu or Putty, just switch the IP address, use '5005' for the 'Local Port' (Fugu) or 'Source Port' (Putty), and use '80' for the 'Service or Port' (Fugu) or the port following the host+colon in the 'Category' -> 'SSH' -> 'Tunnels' 'Destination' textbox (Putty).

You can then access a web page on the 123.123.123.123 server using an http://127.0.0.1:5005 address instead of the normal http://123.123.123.123 address.

Note that the 5005 'localPort' can really be any unused port above 1000. The only reason I keep the 'localPort' and 'remoteHostPort' the same in the database example is so my database connection code is the same and works the same on my development laptop and the actual database server.

#### Other

Note that these techniques can be applied in a wide variety of situations. 
 * I've switched over to tunneled connections from Eclipse, my programming IDE, to my Subversion repositories. 
 * Brown email is encrypted over the network, but if you have a home account that's not, you can check it from a coffee-shop unencrypted wireless network using ssh-tunneling.
