# Etendo
This is the development repository of Etendo. <br>
Etendo is a platform to manage the business flows, adaptable to the needs of the companies. Our mission is creating an adaptable, flexible, composable and scalable software, able to grow without restrictions from the start and offers an intuitive, customizable and complete solution for the companies.
We are developing an international ERP and a platform that supports business development and scalable growth for our partners and their customers.

To more information visit [etendo.software](https://etendo.software)

### Requirements
You can read about the system requirements in the [System Requirements](https://docs.etendo.software/en/technical-documentation/etendo-environment/requirements-and-tools/requirements) section of the Etendo Documentation.

### Etendo Instalation
Etendo includes the Classic ERP functionalities and Etendo RX, a reactive platform to execute microservices, able to interact with the database and perform asynchronous actions.

1. Clone the repository
```
git clone git@github.com:etendosoftware/etendo.git
```
2. 
3. To compile and deploy an Etendo instance you have to setup the configuration variables, to do that you have to create a copy of `gradle.properties.template` file in root and src-rx folders.
```bash
cp gradle.properties.template gradle.properties
cp src-rx/gradle.properties.template src-rx/gradle.properties
```
3. You can either edit both `gradle.properties` files updating the variables, or use their default values.

### gradle.properties

>The Nexus and GitHub credentials are required. <br>
>To configure GitHub credentials read [Using repositories on Etendo](https://docs.etendo.software/en/technical-documentation/etendo-environment/requirements-and-tools/developer-tools/use-of-repositories-in-etendo)

| Variable                       | Description                                                     | Default value |
|--------------------------------|-----------------------------------------------------------------|---------------|
| githubUser <br> githubPassword | GitHub repository credentials, for access to commercial modules |               |
| nexusUser <br> nexusPassword   | Nexus repository credentials, for access to commercial modules  |               |
| context.name                   | Environment name                                                | etendo        |
| bbdd.sid                       | Database name                                                   | etendo        |
| bbdd.port                      | Database port                                                   | 5432          | 
| bbdd.systemUser                | Database system user                                            | postgres      |
| bbdd.systemPassword            | Database system password                                        | syspass       |
| bbdd.user                      | Database user                                                   | tad           |
| bbdd.password                  | Database password                                               | tad           |

### src-rx/gradle.properties

| Variable                     | Description                                                               | Default value                          |
|------------------------------|---------------------------------------------------------------------------|----------------------------------------|
| bbdd.rdbms                   | Database manager system                                                   | POSTGRE                                |
| bbdd.driver                  | Database driver                                                           | org.postgresql.Driver                  |
| bbdd.url                     | Database url connection                                                   | jdbc:postgresql://localhost\:5432      |
| bbdd.sid                     | Database name                                                             | etendo                                 |
| bbdd.systemUser              | Database system user                                                      | postgres                               |
| bbdd.systemPassword          | Database system password                                                  | syspass                                |
| bbdd.user                    | Database user                                                             | tad                                    |
| bbdd.password                | Database password                                                         | tad                                    |
| bbdd.sessionConfig           | Database session preferences                                              | select update_dateFormat('DD-MM-YYYY') |

> **Note** <br>
> Variables appearing in both files must have the same value.  
> Run the gradle tasks with the `--info` or `--debug` flag to see more information.

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
> **Warning** <br>
> If you change the default **bbdd.url** and/or **bbdd.sid**, you must edit the `src-rx/rxconfig/das.yaml` file using the new values.

6. Execute install task to create the initial database and compile the sources
```
./gradlew install
```
5. Deploy Etendo ERP to Tomcat:
```
./gradlew smartbuild
```
This task deploys the webContent folder into the tomcat/webapps directory, for that you must set up $CATALINA_HOME pointing to the aforementioned path.

6. Execute the rx:generate.entities task

```
./gradlew rx:generate.entities 
```

7. Run Tomcat and access to [https://localhost:8080/etendo](https://localhost:8080/etendo) to get into Etendo ERP
8. To execute RX services run:
```
./gradlew rx:rx 
```
By default the following services must be up:
- Config
- Auth
- Edge
- Das
- Async


### Documentation
For  more information you can read documentation in [Etendo Docs](https://docs.etendo.software) .
