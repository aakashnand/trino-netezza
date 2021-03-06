# Trino Netezza Connector

## Prerequisite to build
- Java 11
- Netezza JDBC jar 
  - Ref: https://www.ibm.com/support/knowledgecenter/SSULQD_7.2.1/com.ibm.nz.datacon.doc/c_datacon_jdbc_driver_installation_unix_linux_sup.html
  - Download nzjdbc-3.jar and place it under the directory `resources/repo/org/netezza/nzjdbc/3/`
  
## Usage

### Build connector

```
$ cd trino-netezza
$ ./mvnw clean install
```

This will create taregt folder in the current directory. It should create folder `trino-netezza-351`

```
$ cd target/trino-netezza-351/
$ $ ls target/trino-netezza-351/
HdrHistogram-2.1.9.jar             failsafe-2.4.0.jar                 jackson-datatype-joda-2.11.1.jar           jsr305-3.0.2.jar             stats-202.jar
aopalliance-1.0.jar                failureaccess-1.0.1.jar            jackson-datatype-jsr310-2.11.1.jar         log-202.jar                  trino-base-jdbc-351.jar
bootstrap-202.jar                  guava-29.0-jre.jar                 jackson-module-parameter-names-2.11.1.jar  log-manager-202.jar          trino-matching-351.jar
bval-jsr-2.0.0.jar                 guice-4.2.3.jar                    javax.annotation-api-1.3.2.jar             log4j-over-slf4j-1.7.30.jar  trino-netezza-351-services.jar
cglib-nodep-3.3.0.jar              j2objc-annotations-1.3.jar         javax.inject-1.jar                         logback-core-1.2.3.jar       trino-netezza-351.jar
checker-qual-2.11.1.jar            jackson-core-2.11.1.jar            jcl-over-slf4j-1.7.30.jar                  nzjdbc-3.jar                 trino-plugin-toolkit-351.jar
concurrent-202.jar                 jackson-databind-2.11.1.jar        jmxutils-1.21.jar                          parameternames-1.4.jar       units-1.6.jar
configuration-202.jar              jackson-datatype-guava-2.11.1.jar  joda-time-2.10.6.jar                       slf4j-api-1.7.30.jar         validation-api-2.0.1.Final.jar
error_prone_annotations-2.4.0.jar  jackson-datatype-jdk8-2.11.1.jar   json-202.jar
```

### Setup netezza connector on trino-server
- rename trino-netezza-351 directory to netezza
```
$ mv trino-netezza-351 netezza
```

- Copy target/netezza to trino installation directory 

Example:
```
scp -r target/netezza user@trino-server:/usr/lib/trino/plugins
```

### Create catalog config
- Create catalog file under presto installation directory /etc

```
$vi /usr/lib/trino/etc/catalog/netezza.properties
```

Configure following properties to `netezza.proprties`

```
connector.name=netezza
connection-url=jdbc:netezza://X.X.X.X:5480/db_name
connection-user=username
connection-password=password
```

- Restart the presto server

```
$/usr/lib/trino/bin/launcher restart
```

- Confirm the data
```
trino:default> show catalogs;
 Catalog 
---------
 hive    
 netezza 
 system  
(3 rows)

```

## Limitations
- Currently this connector does not support `DELETE` and `UPDATE` queries.

## Contribution
Please read [CONTRUBUTIONS.md](CONTRIBUTING.md) and feel free to send PR or create issue to improve this connector. 


