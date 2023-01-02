# restapi-springboot-elastic

##  install mysql on windows or on docker container
### install mysql on windows
see file guide on older document/install on window

### install mysql on docker container with docker-compose.yml
see file guide on document/docker

## add dependency elastic
add dependency on pom.xml
--------------------------------- 
         <!--  mysql-->

        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <scope>runtime</scope>
        </dependency>


        <!-- jpa-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>
---------------------------------

## add mysql properties on application.properties
---------------------------------
#mysql config
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=false
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL5InnoDBDialect

spring.datasource.url=jdbc:mysql://localhost:3307/db
spring.datasource.username=user
spring.datasource.password=password
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
---------------------------------


## configuration and implement mysql
- create controller : userController
- create service : userService
- create repo : userRepo extend JPARepository

## Test API user
### create user
- url
  http://localhost:8181/v1/user/save
- req body
  {
  "username":"user",
  "password":"user",
  "roles": "USER",
  "permissions":"READ,WRITE"
  }

### search user by id
- url
  http://localhost:8181/v1/user/1

### search all user
- url
  http://localhost:8181/v1/user/all





