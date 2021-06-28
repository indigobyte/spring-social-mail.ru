# spring-social-mailru

Spring social plugin for Mail.Ru

## Introduction

### How to create new version of plugin

Maven repository is located in folder repository. To produce new version:
- Change version in `pom.xml` file.
- Run command:


    mvn clean deploy
- It will fail with message


    Failed to execute goal com.github.github:site-maven-plugin:0.12:site (default) on project spring-social-mailru: Error creating blob: Not Found (404) -> [Help 1]
- . It's OK. Now go to `target\mvn-repo` folder and delete it.
- Create new empty folder `target\mvn-repo`.
- Clone repository into `target\mvn-repo` folder.
- Go to that folder and checkout `mvn-repo` branch.
- Now go back to repository root and run `mvn deploy` (without `clean`!). It will fail with the same message again. It's OK. 
- Go to `target\mvn-repo` folder, add, commit, and push changes into `mvn-repo` branch.

You might need to change maven settings: `.m2/settings.xml`:

    <?xml version="1.0" encoding="UTF-8"?>
    <settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
              xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
              xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">
        <servers>
            <server>
                <id>github</id>
                <username>username</username>
                <password>password</password>
            </server>
        </servers>
    </settings>

To create local installation run command:

    mvn clean compile package install:install-file
    -DgroupId=org.springframework.social
    -DartifactId=spring-social-mailru
    -Dversion=1.1.2
    -Dfile=target/spring-social-mailru-1.1.2.jar
    -Dsources=target/spring-social-mailru-1.1.2-sources.jar
    -Dpackaging=jar
    -DgeneratePom=true
    -DlocalRepositoryPath=mvn-repo/spring-social-mailru
    -DcreateChecksum=true

### Maven: how to build and install locally, without uploading to remote repository

    mvn clean install
