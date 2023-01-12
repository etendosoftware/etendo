# Etendo
This is the development repository of Etendo. <br>
Etendo is a platform to manage the business flows, adaptable to the needs of the companies. Our mission is creating an adaptable, flexible, composable and scalable software, able to grows without restrictions from the start and offers an intuitive, customizable and complete solution for the companies.
We are developing an international ERP and a platform that supports business development and scalable growth for our partners and their customers.

To more information visit [etendo.software](https://etendo.software)

### Requirements
In this section you can read the [System Requirements](https://docs.etendo.software/en/technical-documentation/etendo-environment/requirements-and-tools/requirements).

### Etendo Instalation
Etendo includes the Classic ERP functionalities and Etendo RX, a reactive platform to execute microservices able to interact with the database and perform asynchronous actions.

1. Clone the repository and move to develop branch
```
git clone  -b develop git@github.com:etendosoftware/etendo.git
```
2. To compile and deploy an Etendo instance you have to setup the configuration variables, to do that you have to create a copy of `gradle.properties.template` file in root and src-rx folders.
```bash
cp gradle.properties.template gradle.properties
cp src-rx/gradle.properties.template src-rx/gradle.properties
```
2. You can edit `gradle.properties` files updating the variables or use the default values

>The Nexus user and Password is required

| Variable                     | Description                                                               | Default value |
|------------------------------|---------------------------------------------------------------------------|---------------|
| nexusUser <br> nexusPassword | Nexus repository credentials, for access to commercial modules            |               |
| context.name                 | Environment name                                                          | etendo        |
| bbdd.sid                     | Database name                                                             | etendo        |
| bbdd.port                    | Database port                                                             | 5432          | 
| bbdd.systemUser              | Database system user                                                      | postgres      |
| bbdd.systemPassword          | Database system password                                                  | syspass       |
| bbdd.user                    | Database user                                                             | tad           |
| bbdd.password                | Database password                                                         | tad           |

> Run the gradle tasks with the `--info` or `--debug` flag to log more information.

Change the repositoryURL to etendo-snapshot-jars
```
...
org.gradle.jvmargs=-Xmx2g -XX:+HeapDumpOnOutOfMemoryError -Dfile.encoding=UTF-8
repositoryUrl=https://repo.futit.cloud/repository/etendo-snapshot-jars
repositoryUser=
repositoryPassword=
...
```

4. Run setup tasks to create the configurations files
```
./gradlew setup
```
4. Change the port to 5432 in the `src-rx/rxconfig/das.yaml` file
```
...
spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/etendo
    username: tad
    password: tad
...
```

6. Execute install task to create the initial database and compile the sources
```
./gradlew install
```
5. Deploy Etendo ERP to Tomcat:
```
./gradlew smartbuild
```
This task deploying the webContent folder into the tomcat/webapps directory, for that you must set up $CATALINA_HOME environment variable.

6. Execute the rx:genearateEntities task

```
./gradlew rx:generate.entities --info 
```

7. Run the tomcat and access to [https://localhost:8080/etendo](https://localhost:8080/etendo) to ingress into Etendo ERP
8. To execute RX services run:
```
./gradlew rx:rx --info
```
By default the following services must be up:
- Config
- auth
- edge
- das
- async


### Documentation
For  more information you can read documentation in [Etendo Docs](https://docs.etendo.software) .