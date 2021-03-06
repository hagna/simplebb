========
simplebb
========


simplebb manages running builds with a distributed network of builders.
Simple setup is the goal.  I wrote this because I couldn't get
Buildbot to do what I wanted.


Quick Start
===========

1. Get the code::

    $ git clone git@github.com:iffy/simplebb.git simplebb.git
    
2. Install dependencies::

    $ easy_install Twisted

3. Start a sample ``simplebb`` server::
    
    $ cd simplebb.git
    $ PYTHONPATH=. python example/server.py

4. See the build script that will take what ever version you want to build
   and append that version to ``example/project/_echo``::

    $ cat example/project/echo

5. Telnet to the server::

    $ telnet 127.0.0.1 9223

6. Request some builds of the ``echo`` project::

    > build echo "Hello, world!"
    Build requested (failures not reported here)
    > build echo "another"
    Build requested (failures not reported here)
    > quit

7. See that the build script was run::

    $ cat example/projects/_echo 
    Hello, world!
    another


What makes simplebb cool?
=========================

Everything is a builder
-----------------------

The server is a builder, the client is a builder, the build-step executer is a
builder.  Some builders simply pass on build requests to other builders.  Others
execute scripts.  You can write your own builders.


It's distributed
----------------

If you connect a builder to a receive build requests from a remote builder,
the local builder is responsible for acquiring code and defining build steps.
You can report the results to the remote builder but you don't have to. If 
you're in QA, you could make a builder that fails every build.



