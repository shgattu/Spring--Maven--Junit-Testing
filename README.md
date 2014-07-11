Spring--Maven--Junit-Testing
============================

Common problems faced when building junit tests with Spring

Maven pom.xml changes:

1) Add dependency of junit and its version. 

<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
			<version>4.9</version>
			<scope>test</scope>
		</dependency>
		
		Scope test specifies to load dependencies during test phase 
		mvn test
		
2) We can load some of the resource files under resources directory to target/test-classes folder if need be
		
		
		src                                                                       target
		|                                                                           |
		|----main                                                                   |--------test-classes
		      |                copying files from resources to test-classesfolder                                                   
		      |--- resources          -------------------->            
		      
		      
3) You can specify test-resources in pom.xml for achieving step 2

<testResources>
			<testResource>
				<directory>src/main/resources/xyz/</directory>
				<filtering>true</filtering>
			</testResource>
			<testResource>
				<directory>src/test/resources</directory>
				<filtering>true</filtering>
			</testResource>
		</testResources>
		
4) Use maven-surefire-plugin to generate reports of tests

5) We can also exclude some classes or folders during compile time for testing. Something like specified below

<plugin>
				<artifactId>maven-compiler-plugin</artifactId>
				<version>2.0.2</version>
				<configuration>
					<source>1.7</source>
					<target>1.7</target>
					<debug>true</debug>
					<debuglevel>lines,vars,source</debuglevel>
				</configuration>
				<executions>
					<execution>
						<id>default-testCompile</id>
						<phase>test-compile</phase>
						<configuration>
							<excludes>
								<exclude>xyz/**</exclude>
							</excludes>
						</configuration>
						<goals>

							<goal>testCompile</goal>
						</goals>
					</execution>
				</executions>
			</plugin>
