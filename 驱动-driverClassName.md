## 数据库几种常见的连接方式

### ***配置***

***driverClassName:xxx***

***url:xxx***

***username:xxx***

***password:xxx***

### MySQL5

driverClassName: com.mysql.jdbc.Driver

url:jdbc:mysql://<host>:<port>/<database_name>

#### example

url:jdbc:mysql://localhost:3306/example

### MySQL6

driverClassName: com.mysql.cj.jdbc.Driver

url:jdbc:mysql://<host>:<port>/<database_name>

#### example

url:jdbc:mysql://localhost:3306/example

### oracle

driverClassName: oracle.jdbc.driver.OracleDriver

url:jdbc:oracle:thin:@<host>:<port>:<database_name>

#### example

url:jdbc:oracle:thin:@localhost:1521:orcl

### Sql Server

driverClassName:com.microsoft.sqlserver.jdbc.SQLServerDriver

url:jdbc:sqlserver://<host>:<port>; DatabaseName=<database_name>

#### example

url:jdbc:sqlserver://localhost:1433; DatabaseName=example

### DB2

driverClassName:  com.ibm.db2.jcc.DB2Driver

url:  jdbc:db2://<host>:<port>/<database_name>

#### example 

url:jdbc:db2://localhost:50000/example

### HSQLDB

driverClassName:org.hsqldb.jdbcDriver

url:jdbc:hsqldb:hsql://<host>:<port>/<database_name>

#### example

url:jdbc:hsqldb:hsql://localhost:9001/example

### ODBC

driverClassName:sun.jdbc.odbc.JdbcOdbcDriver

url:jdbc:odbc:<database_name>

#### example

url:jdbc:odbc:example



