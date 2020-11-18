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