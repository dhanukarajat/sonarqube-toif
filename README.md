# sonarqube-toif
SonarQube Adapter for TOIF  

Contents:
-----------------------------------------------
This directory contains the source code for SonarLint Adapter (com.kdmanalytics.toif.sonarqube) to run with TOIF. It contains the configuration files such as SonarQubeAdapter.java, Activator.java     


Prerequisite:
-----------------------------------------------
Sonarlint.bat file should be present in the classpath of the machine which is using the SonarLint adapter.
Sonarlint-CLI 2.0 was used for the building of the adapter. 
You can download from here: https://bintray.com/sonarsource/Distribution/org.sonarsource.sonarlint-cli/2.0

Note: SonarLint is a standalone version of SonarScanner and is better supported by TOIF framework. As we initially started developing the adapter with SonarQube, there exists a few references to SonarQube throughout the source code.

Supported file(s):
-----------------------------------------------
This version of Sonarlint plugin adapter supports Java files for static analysis.


Working:
-----------------------------------------------
1. Toif facilitates the plugging in of the new adapter by extending the adapter class of AbstractAdaptor class.
2. The adapter class of SonarLint command line utility is SonarQubeAdapter.class which overrides the parse() and runToolCommand() methods of TOIF.
3. The Parse() method parses the output of the SonarLint adapter. The parser extracts the line number and message(rule name) of the exception.
4. This is then passed into the createFinding creator to generate the TOIF finding files.
5. SonarQube supports 58 CWE for Java source code and the same has been mapped in the SonarQubeConfiguration File.
6. The runToolCommand simply maps the Toif arguments with that of the SonarLint arguments and facilitates the triggering of sonarLint command line.
7. Our SonarLint Adapter has been mapped to all 58 CWE findings which are supported by SonarLint Command Utility.

SonarLint commandline argument format used in the plugin:
---------------------------------------------------------
SonarLint --src <File name to be analysed> --html-report <Canonical path along with the file name to the output file>.


Toif execution command:
-------------------------------------------------------------
TOIF --adaptor=<adapter-name> --inputfile=<canonical path to the input java file> --outputdirectory=<canonical path to the output folder location> --housekeeping=<canonical path to the 'housekeeping' configuration file>

Usage:
TOIF --adaptor=sonarqube --inputfile=<canonical path to the input java file> --outputdirectory=<canonical path to the output folder location> --housekeeping=<canonical path to the housekeepingconfiguration file>


Mapping implemented:
Toif Argument      			SonarLint Argument
-------------            ----------------------
inputfile	path				Name of the file extracted from the path

--html-report					outputfolder appended with the name of the input file and extension name as .html


Integration of JSoup Plugin with TOIF
-----------------------------------------------
SonarLint adapter internally uses Jsoup plugin,(https://jsoup.org/) to parse the HTML input of the SonarLint adapter.
The following dependency was included into our .pom files for running JSoup 1.10.1 package

<dependency>
  <!-- jsoup HTML parser library @ http://jsoup.org/ -->
  <groupId>org.jsoup</groupId>
  <artifactId>jsoup</artifactId>
  <version>1.10.1</version>
</dependency>


Debug Output of the SonarLint Parser:
-----------------------------------------------
The SonarLint Parser outputs the Line number and the Issue Description on the console after extracting from the SonarLint HTML Report.  


****************************** END of ReadMe ******************************




 
