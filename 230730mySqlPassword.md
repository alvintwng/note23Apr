## MySQL password
I has struggled whole day to recover the mySql root password but no avail.
At the end mashed up and need to uninstalled and removed all MySql related files.
On my Windows:
- Remove MySQL Files:  `C:\Program Files\MySQL\MySQL Server 8.0\`
- Remove MySQL Service (Optional): 
- Remove MySQL Configuration Files:  `C:\ProgramData\`
- Search all MySQL residual vua `C:\>dir \*mysql* /s`
- Disk Cleanup

### Installed
Installed only MySQL 8.0 Command Line Client. Copy down new password.

Did download `mysql-connector-j-8.1.0`, and set to Class path in Windows.
But after able to connect to sql, I removed back.   
Because realised that Maven has this driver setup too.   
https://dev.mysql.com/doc/connector-j/8.1/en/connector-j-installing-maven.html

pom.xml, after added version, error resolved. 
``` xml
    <dependency>
        <groupId>com.mysql</groupId>
        <artifactId>mysql-connector-j</artifactId>
        <version>8.0.33</version>
        <!-- <scope>runtime</scope> -->
    </dependency>
```
application.properties
```
spring.jpa.hibernate.ddl-auto=update
spring.datasource.url=jdbc:mysql://localhost:3306/accounts
spring.datasource.username=root
spring.datasource.password=Zero@1
```
Ref from: https://github.com/alvintwng/steps/tree/ver01/AuthEmp/src/main
### MySQL Tutorial
- `\c` to cancel
- `SELECT USER();`
- `SHOW DATABASES;`
- `USE mysql`
- `SHOW TABLES;`
- `DESCRIBE user;`
- `SELECT COUNT(*) FROM user;`
- `SELECT User, Grant_priv FROM user;`

Create and grant database:
``` mysql
mysql> CREATE DATABASE accounts;
mysql> USE accounts
mysql> GRANT ALL ON accounts.* TO 'root'@'localhost';
```
---
