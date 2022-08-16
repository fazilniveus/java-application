Maven Project Code Analysis With Sonarqube:
==========================================
Sonarqube is an invaluable tool for static code analysis and monitoring test coverage. 
This example demonstrates how to analyze a simple Java Maven project.

Prerequisites
=============
* [SonarQube](http://www.sonarsource.org/downloads/) 2.12 or higher
* Maven 3.3.1 or higher

Installation:
=============
* Create an empty schema called sonar and a sonarqube user, with db_owner (CRUD) permission on this db (MS SQL is so nice on this)

* Edit conf/sonar.properties, and set the following:

    VARIABLE                 | ROLE                                                     | EXAMPLE VALUES 
    -------------------------|----------------------------------------------------------|----------------
    sonar.jdbc.username      |The sonar database username                               |sonar
    sonar.jdbc.password      |The sonar database password                               |s3cr3t1234
    sonar.jdbc.url           |The sonar database url                                    |jdbc:jtds:sqlserver://localhost/sonar;SelectMethod=Cursor
    sonar.web.context        |Web context. When set, it must start with forward slash (for example /sonarqube).|/sonar
    sonar.web.port           |TCP port for incoming HTTP connections.                   |9000

* Run StartSonar.bat on the cmd to test

* Go to localhost:9000/sonar

* If everything is ok, run InstallNTService.bat to install sonarqube as a service


Running analysis on a maven project:
====================================
* Copy the settings.xml file to your .m2 folder(see [link](http://docs.sonarqube.org/display/SONAR/Installing+and+Configuring+Maven) for details)

* Copy the sonar-specific details on the pom file to your pom file

* Each time you make a change to your maven project, run:

	mvn clean org.jacoco:jacoco-maven-plugin:0.7.4.201502262128:prepare-agent install
		
	This cleans, builds, tests, downloads jacoco, and runs the "prepare-agent" goal, packages then installs
	PS: 0.7.4.201502262128 is the jacoco version number
	
* Run: mvn sonar:sonar [This updates the sonar db]

* Refresh localhost:9000/sonar
