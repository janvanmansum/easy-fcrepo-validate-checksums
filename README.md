*Note: this project is in pre-alpha state, so below instructions may not work completely yet*

easy-fcrepo-fixity-checker
==========================

Check the fixity of a Fedora Commons Repository's datastreams.

SYNOPSIS
--------

    easy-fcrepo-fixity-checker \
       [-f <fcrepo-server>] \
       [-u <fcrepo-user> \
        -p <fcrepo-password> ] \
       [-l][-s] \
       [-t <time-between-calls>] \

DESCRIPTION
-----------

Service that checks the fixity of datastreams in a Fedora Commons 3.x repository. It does this by continuously retrieving
the metadata for the datastreams to be checked with the Fedora [getDatastream] method, specifying ``validateChecksum = true``,
so that Fedora recalculates the datastream's checksum and compares it to the one stored in the digital object. This action
can optionally be logged in the digital object's audit log.

ARGUMENTS
---------

* ``--fcrepo-server``, ``-f`` -- URL of the Fedora Commons Repository Server
* ``--fcrepo-user``, ``-u`` -- Fedora user to connect with
* ``--fcrepo-password``, ``-p`` -- Fedora user's password
* ``--log-results``, ``-l`` -- whether to log the result of the validation in the digital object's audit log
* ``--skip-external-datastreams``, ``-s`` -- whether to skip datastreams with control group ``R`` and ``E``.
* ``--time-between-calls``, ``-t`` -- time in milliseconds to wait before doing the next call to Fedora


INSTALLATION AND CONFIGURATION
------------------------------

### Installation steps:

1. Unzip the tarball to a directory of your choice, e.g. /opt/
2. A new directory called easy-fcrepo-fixity-checker-<version> will be created
3. Create an environment variabele ``EASY_FCREPO_FIXITY_CHECKER_HOME`` with the directory from step 2 as its value


### Configuration

General configuration settings can be set in ``$EASY_FCREPO_FIXITY_CHECKER_HOME/cfg/application.properties`` 
and logging can be configured in ``$EASY_FCREPO_FIXITY_CHEKCER_HOME/cfg/logback.xml``. The available settings are 
explained in comments in aforementioned files.

The datastreams that must be validated must be configured in the ``$EASY_FCREPO_FIXITY_CHECKER_HOME/cfg/validation.properties``.
The format of this file is as follows:

      <namespace-id>=<datastream-id-list>
      
in which ``<namespace-id>`` is the namespace to validate and ``datastream-id-list`` is a comma separated list of datastreams
to check in that namespace.




BUILDING FROM SOURCE
--------------------

Prerequisites:

* Java 7 or higher
* Maven 3.3.3 or higher
 
Steps:

1. Clone and build the [dans-parent] project (*can be skipped if you have access to the DANS maven repository*)
      
        git clone https://github.com/DANS-KNAW/dans-parent.git
        cd dans-parent
        mvn install
2. Clone and build this project

        git clone https://github.com/DANS-KNAW/easy-fcrepo-fixity-checker.git
        cd easy-fcrepo-fixity-checker
        mvn install
        
[getDatastream]: https://wiki.duraspace.org/display/FEDORA38/REST+API#RESTAPI-getDatastream
