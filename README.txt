 for testing Maven Training Suite (Two Modules)
================================

This zip is a training project to demo:
- mvn -v, validate, compile, test, package, install
- test reports (Surefire)
- coverage report (JaCoCo) [jar-demo]
- WAR build + Tomcat deployment [war-demo]
- JFrog/Artifactory deploy using mvn deploy (placeholders)

Modules
-------
1) jar-demo
   - Packaging: JAR (runnable)
   - Tests: JUnit5
   - Reports:
     * target/surefire-reports  (unit test reports)
     * target/site/jacoco       (HTML coverage report)

2) war-demo
   - Packaging: WAR (Tomcat deploy)
   - URL after deploy:
     http://<HOST>:8080/war-demo/hello

Quick Demo Commands
-------------------
From project root:

1) Show Maven version
   mvn -v

2) Validate
   mvn validate

3) Compile
   mvn compile

4) Test + reports
   mvn test

5) Package (builds jar and war)
   mvn package

6) Install into local repo (~/.m2)
   mvn install

Build only one module
---------------------
mvn -pl jar-demo clean test
mvn -pl war-demo clean package

Run JAR Demo
------------
java -jar jar-demo/target/jar-demo.jar

Tomcat Deploy (WAR Demo)
------------------------
1) Ensure Tomcat is running (port 8080)
2) Copy WAR:
   cp war-demo/target/war-demo.war $CATALINA_HOME/webapps/

3) Open:
   http://<EC2_PUBLIC_IP>:8080/war-demo/hello

JFrog / Artifactory Deploy
--------------------------
Parent pom has distributionManagement with placeholders:
- jfrog-releases
- jfrog-snapshots

1) Update URLs in parent pom.xml:
   <jfrog.release.repo.url>...</jfrog.release.repo.url>
   <jfrog.snapshot.repo.url>...</jfrog.snapshot.repo.url>

2) Add credentials to ~/.m2/settings.xml (example below)

3) Deploy:
   mvn clean deploy

Example ~/.m2/settings.xml
--------------------------
<settings>
  <servers>
    <server>
      <id>jfrog-releases</id>
      <username>YOUR_USER</username>
      <password>YOUR_API_KEY</password>
    </server>
    <server>
      <id>jfrog-snapshots</id>
      <username>YOUR_USER</username>
      <password>YOUR_API_KEY</password>
    </server>
  </servers>
</settings>
