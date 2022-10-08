Sonarqube
token = 18fadd6c0c6459cd914def053cecf0da12048f5d
mvn sonar:sonar \
  -Dsonar.projectKey=javawebapp \
  -Dsonar.host.url=http://44.203.89.62:9000 \
  -Dsonar.login=18fadd6c0c6459cd914def053cecf0da12048f5d

maven
{0hzLwlWQpt0HFJodMu4sBwu/a90ZLnZS/egufWwHrfw=} 
{5g3Ri2rZO+gHCqZnNMDoy6Q42pznyuK2RNCGidh+8iw=}

<?xml version="1.0" encoding="UTF-8"?>

<settings xmlns="http://maven.apache.org/POM/4.0.0"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">

  <localRepository>/var/lib/jenkins/.m2/repository</localRepository>
######
<servers>
   <server>
        <id>nexus</id>
        <username>admin</username>
        <password>{5g3Ri2rZO+gHCqZnNMDoy6Q42pznyuK2RNCGidh+8iw=}</password>
    </server>
</servers>

<mirrors>
    <mirror>
      <id>nexus</id>
      <name>nexus</name>
      <url>http://44.201.219.119:8081/repository/maven_project/</url>
      <mirrorOf>*</mirrorOf>
    </mirror>
  </mirrors>

</settings>
