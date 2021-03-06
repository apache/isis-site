Title: Downloads

[//]: # (content copied to _user-guide_xxx)

Apache Isis&trade; software is a framework for rapidly developing domain-driven apps in Java. Write your business logic in entities, domain services and repositories, and the framework dynamically generates a representation of that domain model as a webapp or RESTful API.  Use for prototyping or production.

## Getting Started

If you just want to get going quickly, we suggest using one of our Maven archetypes.

For example:

<pre>
mvn archetype:generate  \
    -D archetypeGroupId=org.apache.isis.archetype \
    -D archetypeArtifactId=simpleapp-archetype \
    -D archetypeVersion=1.8.0 \
    -D groupId=com.mycompany \
    -D artifactId=myapp \
    -D version=1.0-SNAPSHOT \
    -B
</pre>

For more information, see [here](intro/getting-started/simpleapp-archetype.html).

## Formal Releases

If you want to build Isis from formally released source tarballs, you can download from here:

Core:

* [isis-1.8.0](https://www.apache.org/dyn/closer.cgi/isis/isis-core/isis-1.8.0-source-release.zip) ([asc](http://www.apache.org/dist/isis/isis-core/isis-1.8.0-source-release.zip.asc), [md5](http://www.apache.org/dist/isis/isis-core/isis-1.8.0-source-release.zip.md5)) 

Notes:
* in v1.6.0, core incorporates JDO/DataNucleus ObjectStore, Restful Objects viewer and Shiro Security (previously released as separate components).
* in v1.7.0, modules released (in `org.apache.isis.module` have been moved to be [http://www.isisaddons.org](Isis add-ons) (not ASF).
* in v1.8.0, core incorporates Wicket viewer (previously released as separate components).


Archetypes:

* [simpleapp-archetype-1.8.0](https://www.apache.org/dyn/closer.cgi/isis/archetype/simpleapp-archetype/simpleapp-archetype-1.8.0-source-release.zip) ([asc](http://www.apache.org/dist/isis/archetype/simpleapp-archetype/simpleapp-archetype-1.8.0-source-release.zip.asc), [md5](http://www.apache.org/dist/isis/archetype/simpleapp-archetype/simpleapp-archetype-1.8.0-source-release.zip.md5))


## Verifying Releases

It is essential that you verify the integrity of any downloaded files using
the PGP or MD5 signatures.  For more information on signing artifacts and
why we do it, check out the
[Release Signing FAQ](http://www.apache.org/dev/release-signing.html).

The PGP signatures can be verified using PGP or GPG.  First download the [KEYS](http://www.apache.org/dist/isis/KEYS) as well as the asc signature file for the artifact.  Make sure you get these files from the [main distribution directory](http://www.apache.org/dist/isis/), rather than from a mirror.

Then verify the signatures using a command such as:

<pre>
pgpk -a KEYS
pgpv isis-1.8.0-source-release.zip.asc
</pre>

or
<pre>
pgp -ka KEYS
pgp isis-1.8.0-source-release.zip.asc
</pre>

or
<pre>
gpg --import KEYS
gpg --verify isis-1.8.0-source-release.zip.asc
</pre>

Alternatively, you can verify the MD5 signature on the files. A Unix/Linux
program called `md5` or `md5sum` is included in most distributions.  It is
also available as part of
[GNU Textutils](http://www.gnu.org/software/textutils/textutils.html).
Windows users can get binary md5 programs from these (and likely other) places:

 * <http://www.md5summer.org/>
 * <http://www.fourmilab.ch/md5/>
 * <http://www.pc-tools.net/win32/md5sums/>


## Source Code

You can also download the Isis source code using:

<pre>
git clone git://git.apache.org/isis.git
</pre>

or

<pre>
git clone http://git.apache.org/isis.git
</pre>

The code is also mirrored on [github](http://github.com/apache/isis), where you can browse it or fork it.   And if you're interested in contributing back to Isis, see [here](contributors/contributing.html).
       
### Committers

Committers should use the read/write repo:

<pre>
https://git-wip-us.apache.org/repos/asf/isis.git
</pre>

You can browse the repo [here](https://git-wip-us.apache.org/repos/asf/isis/repo?p=isis.git;a=summary).

