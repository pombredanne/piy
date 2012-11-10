# piy


"POM in YAML" is a simple tool to write [Maven](http://maven.apache.org) POM files using [YAML](http://www.yaml.org/).

## Usage

First you would need to install it in your system:

    python setup.py install

## How does it work

The tools preprocess th file pom.yaml of the current directory, and generates a proper pom.xml. Then you can use Maven as usual.

Althougt with the same goal, the approach is completelly different to [Maven3 polyglot](http://polyglot.sonatype.org/), which adds to Maven3 the ability to work with pom files written in non-XML notations. 

## Status

**The tools is still in alpha!**

Currently it has a strong issue for its usage:

 * It is not completelly functionall without applying [this patch](http://www.yaml.org/) to one of its dependencies

## Syntax

Basically it's a translation of the current XML tree to YAML.

    project:

        modelVersion: 4.0.0
        groupId: com.foo
        artifactId: bar
        version: 1.0-SNAPSHOT
        packaging: jar

        build:
            plugins:
                plugin:
                    groupId: org.apache.maven.plugins
                    artifactId: maven-compiler-plugin
                    version: 2.5.1                
                    configuration:
                        source: 1.6
                        target: 1.6

        dependencies:
            dependency:
                groupId: com.bar
                artifactId: foo
                version: 1.0-SNAPSHOT

This will be transformed to a normal pom.xml file.

Although not very common in POMs, sometimes attributes are necessary. Since YAML doesn't support attributes, attributes start with underline.

See for instance the following example to configure the port with the Jetty plugin:

    project:
        build:
            plugins:
                plugin:
                    groupId: org.mortbay.jetty
                    artifactId: maven-jetty-plugin
                    version: 6.1.10
                    configuration:
                        connectors:
                            connector:
                                _implementation: org.mortbay.jetty.nio.SelectChannelConnector
                                port: 8080

