This describes the BrowserID "Native Client Facilitation Server", 
something that requires a better name.

# Overview

BrowserID requires a non-trivial amount of client side logic to 
function properly.  Namely, the generation of keypairs, and a specific
UI.  Because the most complex place to implement said logic is in 
web browsers, that was the primary focus of the BrowserID Project.

This focus is problematic when it is desired to integrate browserid
into native applications or plugins for mobile or desktop applications.

The NCFS server leverages existing code to provide a simplified API for
native applications, to enable rapid prototyping of said applications.
Using this server, it's possible to build client applications that 
use BrowserID in the short term, and then eventually move more
implementation into the client.

A design goal of the server is to leave the core implementation of
BrowserID unchanged, specifically by having the server bridge the 
existing BrowserID protocol to native devices.  The combination of 
a native app using the server, and the server itself should appear
to BrowserID as an existing web client

# Server API

The api exposed by NCFS exposes only a subset of the features
available with BrowserID.  It is thus:

## `https://browserid_ncfs.<some_domain>/auth`

  * method `post`
  * arguments 
    * `email`
    * `password`
  * response
    * `secret` (in some sort of object that handles errors as well)

## `https://browserid_ncfs.<some_domain>/list_emails`

  * method `post`
  * arguments 
    * `secret`
  * response
    * list of emails (in some sort of object that handles errors as well)

## `https://browserid_ncfs.<some_domain>/get_assertion`

  * method `post`
  * arguments 
    * `secret`
    * `audience`
    * `email`
  * response
    * `assertion` (in some sort of object that handles errors as well)

## `https://browserid_ncfs.<some_domain>/logout`

  * method `post`
  * arguments 
    * `secret`
  * response
    * `status` (in some sort of object that handles errors as well)
