# Airship packaging for Dropwizard applications

Allows deployment of dropwizard based java applications into [https://github.com/airlift/airship](Airship).

## Usage

* add launcher dependency in `runtime` scope to the project:

```xml
        <dependency>
            <groupId>de.softwareforge.airship</groupId>
            <artifactId>dropwizard-launcher</artifactId>
            <version> ... current version ... </version>
            <type>tar.gz</type>
            <scope>runtime</scope>
        </dependency>
```

* add maven assembly plugin to build deployable artifact.

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-assembly-plugin</artifactId>
            <version>2.4.1</version>
            <configuration>
                <appendAssemblyId>false</appendAssemblyId>
                <tarLongFileMode>gnu</tarLongFileMode>
                <attach>true</attach>
                <descriptorRefs>
                    <descriptorRef>distribution</descriptorRef>
                </descriptorRefs>
            </configuration>
            <dependencies>
                <dependency>
                    <groupId>de.softwareforge.airship</groupId>
                    <artifactId>dropwizard-packaging</artifactId>
                    <version> ... current version ... </version>
                </dependency>
            </dependencies>
            <executions>
                <execution>
                    <id>package</id>
                    <phase>package</phase>
                    <goals>
                        <goal>single</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

When building the project, a tarball with the service in airship deployable format is created.

## Deployment

Any deployment into airship also requires a configuration artifact. This must contain

* `etc/server.yml` - dropwizard configuration file
* `etc/jvm.config` - JVM configuration

