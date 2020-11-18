# Presto Netezza Connector

## Prerequisite
- Latest Netezza JDBC jar
- Java 11
- maven 3.6.3 or 3.6.3+

## Usage
### Copy nzjdbc.jar to resources
- Copy your nzjdbc.jar under `presto-netezza/resources/repo/org/netezza/nzjdbc/3`

### Build connector
```
$ cd presto-netezza
$ mvn clean install
```
This will create taregt folder in the current directory. It should create folder `presto-netezza-347-SNAPSHOT`
```
$ cd target/presto-netezza-347-SNAPSHOT/
$ ls target/presto-netezza-347-SNAPSHOT/
HdrHistogram-2.1.9.jar             guava-29.0-jre.jar                         javax.inject-1.jar           parameternames-1.4.jar
aopalliance-1.0.jar                guice-4.2.3.jar                            jcl-over-slf4j-1.7.30.jar    presto-base-jdbc-347-SNAPSHOT.jar
bootstrap-201.jar                  j2objc-annotations-1.3.jar                 jmxutils-1.21.jar            presto-matching-347-SNAPSHOT.jar
bval-jsr-2.0.0.jar                 jackson-core-2.10.5.jar                    joda-time-2.10.6.jar         presto-netezza-347-SNAPSHOT-services.jar
cglib-nodep-3.3.0.jar              jackson-databind-2.10.5.jar                json-201.jar                 presto-netezza-347-SNAPSHOT.jar
checker-qual-2.11.1.jar            jackson-datatype-guava-2.10.5.jar          jsr305-3.0.2.jar             presto-plugin-toolkit-347-SNAPSHOT.jar
concurrent-201.jar                 jackson-datatype-jdk8-2.10.5.jar           log-201.jar                  slf4j-api-1.7.30.jar
configuration-201.jar              jackson-datatype-joda-2.10.5.jar           log-manager-201.jar          slf4j-jdk14-1.7.30.jar
error_prone_annotations-2.4.0.jar  jackson-datatype-jsr310-2.10.5.jar         log4j-over-slf4j-1.7.30.jar  stats-201.jar
failsafe-2.4.0.jar                 jackson-module-parameter-names-2.10.5.jar  logback-core-1.2.3.jar       units-1.6.jar
failureaccess-1.0.1.jar            javax.annotation-api-1.3.2.jar             nzjdbc-3.jar                 validation-api-2.0.1.Final.jar
```

### Setup netezza connector on presto-server
- rename presto-netezza-347-SNAPSHOT directory to netezza
```
$ mv presto-netezza-347-SNAPSHOT netezza
```

- Copy target/netezza to presto installation directory 
Example:

```
scp -r target/netezza user@presto-server:/usr/lib/presto/plugins
```

### Create catalog config
- Create catalog file under presto installation directory /etc
```
$vi /usr/lib/presto/etc/catalog/netezza.properties
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
$/usr/lib/presto/bin/launcher restart
```

- Confirm the data
```
presto:default> show catalogs;
 Catalog 
---------
 hive    
 netezza 
 system  
(3 rows)

```






