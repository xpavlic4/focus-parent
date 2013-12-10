Focusmr Parent POM
=================
The parent Maven POM for Focusmr community projects.

What is it?
-----------
The Focusmr parent POM provides default configuration for Maven builds.
 
* Recommended/Default versions for the most commonly used Maven plugins
* Manifest configuration for the jar and assembly plugins
* Profiles for generating source jars, and enforcing a minimum versions of 
  Java and Maven
* Distribution Management and other configuration for deploying to the 
  Focusmr Maven repositories

How to use it?
--------------
Start out by adding the parent configuration to your pom.

    <parent>
      <groupId>com.focusmr</groupId>
      <artifactId>focusmr-parent</artifactId>
      <version>0.0.8-SNAPSHOT</version>
    </parent>

The pom includes properties which allow various build configuration to be 
customized.  For example, to override the default version of the
maven-compiler-plugin, just set a property.

    <properties>
      <version.compiler.plugin>2.3</version.compiler.plugin>
    </properties>

Or override the default Java compiler source and target level used in the build.  
Note the default level is 1.6.

    <properties>
      <maven.compiler.target>1.5</maven.compiler.target>
      <maven.compiler.source>1.5</maven.compiler.source>
    </properties>

The minimum version of Java or Maven required to run a build can also be set via
properties.

    <properties>
      <maven.min.version>3.0.3</maven.min.version>
      <jdk.min.version>1.7</jdk.min.version>
    </properties>

For the full list of properties, refer to the POM itself.


The Focusmr Release Profile
--------------------
The parent POM includes a Maven profile called "focusmr-release".  This profile contains 
settings for generating a full project source archive, javadoc jar files, and
release deployment metadata.  If using the Maven release plugin, this profile
will automatically be activate during the release:perform step.

If the Maven release plugin is not used during the release process, the profile
can be manually activated from the command line during a release build.

    mvn -Pfocusmr-release deploy


The GPG Sign Profile
--------------------
This POM includes a Maven profile called "gpg-sign" which provides default 
configuration to generate GPG signatures for the build artifacts.  

    mvn -Pgpg-sign deploy

In order for the gpg plugin to properly create a signature for each artifact,
the properties "gpg.keyname" and "gpg.passphrase" must be available to 
the current build.  These properties can either be set in a
build profile, or on the command line.

    <profile>
      <id>gpg-config</id>
      <properties>
        <gpg.keyname>me@home.com</gpg.keyname>
        <!-- Don't keep passphrase in plain text! -->
        <gpg.passphrase>secret</gpg.passphrase>
      </properties>
    </profile>