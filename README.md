# Creating RPM Packages for Fedora 16+ / Centos 6+
You might be able to get these specs working on ancient versions of <= Centos 5 / <= RHEL 5/ <= Fedora 15, but it is a royal pain, and requires some crazy patching to do so. It is practical to use a more current distribution release. Please don't send me patches or requests for those older OS. They won't get accepted.

These are written and tested against couchdb-1.2.0

## Requirements

Fedora:
* [Instructions](https://fedoraproject.org/wiki/How_to_create_an_RPM_package) for setting up rpmbuild on Fedora
* sudo yum install autoconf automake libtool curl-devel erlang-erts erlang-etap erlang-ibrowse erlang-mochiweb erlang-oauth erlang-os_mon help2man js-devel libicu-devel perl-Test-Harness erlang-crypto erlang-erts erlang-inets erlang-kernel erlang-sasl erlang-stdlib erlang-tools

Centos:
* [Instructions](http://wiki.centos.org/HowTos/SetupRpmBuildEnvironment) for setting up rpmbuild on Centos NOTE: Do not install redhat-rpm-config
* Build and install working js-devel-1.8.5 (See README_JS_DEVEL.md)
* sudo yum install autoconf automake libtool curl-devel erlang-erts erlang-etap erlang-ibrowse erlang-mochiweb erlang-oauth erlang-os_mon help2man libicu-devel perl-Test-Harness erlang-crypto erlang-erts erlang-inets erlang-kernel erlang-sasl erlang-stdlib erlang-tools

## Build RPM (Fedora and Centos)
* Download release archive from https://couchdb.apache.org/downloads.html
Or:
* Checkout couchdb from https://git-wip-us.apache.org/repos/asf/couchdb.git
* Alternatively, create an archive from a release tag or repo revision: git archive --format=tar --prefix=apache-couchdb-1.2.0/ fb72251bc | gzip >apache-couchdb-1.2.0.tar.gz
Then:
* mv downloaded archive to ~/rpmbuild/SOURCES
* cd This project dir
* cp .spec ~/rpmbuild/SPECS
* cp *.patch ~/rpmbuild/SOURCES
* cp couchdb.init ~/rpmbuild/SOURCES
* cd ~/rpmbuild/SPECS
* If building a version other than 1.2.0, update the spec file to reflect your version change.
* rpmbuild -ba couchdb.spec
* Installable rpms will reside in ~/rpmbuild/RPMS

## Other
* Please take a look at https://github.com/iriscouch/build-couchdb for ability to build against specific erlang and spidermonkey versions.
* Drop by irc.freenode.net #couchdb if you have any questions.
