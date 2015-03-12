*This is forked from https://code.google.com/p/onejar-maven-plugin/ to fix issues with included AWS jars.*


# Lets you build an executable jar with Maven2, containing all dependencies.

You can do that with the assembly plugin too, but that will just unpack all dependencies together with your classes in one directory and then repack that directory into a new jar. Doing it that way means files will overwrite each other if they have the same names in the same path, which is quite common with resources such as log4.properties and even other more important files.

**With onejar-maven-plugin, you'll instead get a nice clean super jar with the dependency jars inside.**

Get started by following the Usage [instructions](http://onejar-maven-plugin.googlecode.com/svn/mavensite/usage.html)!

## Changes from the original

The fork packages a patched one-jar 0.97 from [iceberg901](https://github.com/iceberg901/sbt-onejar/commit/0fb0f829941aac4074be47cec4899b8b5a86d961) and uses that version  by default. The original 0.97 is still intact and can be used by specifying the onejarVersion configuration option in the maven pom.xml.

### Example pom.xml build plugin configuration

	...
	<build>
		<plugins>
			<plugin>
				<groupId>com.github.sampov2</groupId>
				<artifactId>onejar-maven-plugin</artifactId>
				<version>1.4.6</version>
				<executions>
					<execution>
						<configuration>
							<mainClass>my.package.Foo</mainClass>
							<attachToBuild>true</attachToBuild>
						</configuration>
						<goals>
							<goal>one-jar</goal>
						</goals>
					</execution>
				</executions>
			</plugin>
		</plugins>
	</build>
	
	<pluginRepositories>
		<pluginRepository>
			<id>com.github.sampov2.onejar-maven-plugin</id>
			<url>http://maven.codeforcode.com/repository</url>
		</pluginRepository>
	</pluginRepositories>
	...

