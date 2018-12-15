# AWS-Elastic-Beanstalk
AWS Elastic Beanstalk

> - 1. Donwload Python3.7 from link https://www.python.org/downloads/release/python-367/
> - 2. Set path in driver C
```
C:\Users\vuongluis\AppData\Roaming\Python\Python37\Scripts
C:\Users\vuongluis\AppData\Local\Programs\Python\Python37-32\Scripts
```
> - 3. Restart Application
> - Type command to check
```
C:\Windows\System32> python --version
C:\Windows\System32> pip --version
C:\Windows\System32> pip install awsebcli --upgrade --user
C:\Windows\System32> eb --version
C:\Windows\System32> pip install awsebcli --upgrade
```

> - 4. Initializing Elastic Beanstalk CLI and Creating an application eb --version
>> - 4.1 Create folder to put your project and prepare it to push Amazon server
>>> - Select a default region: 7 (Singapore)
>>> - You must provide your credentials: https://console.aws.amazon.com/iam/home?#/security_credential (Section 3). You go to Create New Access Key.
>>> - Enter Application Name: Genealogy
>>> - Select a platform: 11 Java
>>> - Java 8
>>> - n (SSH)
>>> - keypair name: genealogy
>>> - Install ssh client in Window 10
>>> - http://www.mls-software.com/opensshd.html and default not need to set name:

>> - 4.2 Configuring the deployment of our Spring Boot application
>>> - We open: .elasticbeanstalk/config.yml
```
branch-defaults:
  default:
    environment: null
    group_suffix: null
## Add the following deploy configuration    
deploy:
  artifact: target/easy-notes-1.0.0.jar
global:
  application_name: Genealogy
  branch: null
  default_ec2_keyname: Genealogy-key
  default_platform: Java 8
  default_region: ap-southeast-1
  include_git_submodules: true
  instance_profile: null
  platform_name: null
  platform_version: null
  profile: eb-cli
  repository: null
  sc: git
  workspace_type: Application

```
>>> - How to create a jar file with IntelliJ IDEA?
>>>> - Go to File/Project Structure/Artifacts/JAR/From modules with dependencies...
>>>> - MainClass is your XXXApllication.java. For example: Here, we have com.api.genealogy.GenealogyApplication
>>>> - Go to Build/Build Artifacts/.../Build
>>>> - Here is location: Genealogy-API\classes\artifacts\genealogy_jar

> - 5. Creating an Elastic Beanstalk Environment with an RDS database
```
eb create --single --database
```
>> - Enter Environment Name: Genealogy-dev
>> - 6. Enter an RDS DB username: boot
>> - 7. boot + pass: Password is not special character mXXX
>> - Please make sure that you have git on it.

> - 6. Configuring Environment properties for RDS database
```
eb status
eb console
eb setenv SPRING_DATASOURCE_URL=jdbc:mysql://aar49hhc1w3ghr.cohablpe3kal.ap-southeast-1.rds.amazonaws.com:3306/ebdb SPRING_DATASOURCE_USERNAME=boot SPRING_DATASOURCE_PASSWORD=mxx
```
## Spring DATASOURCE (DataSourceAutoConfiguration & DataSourceProperties)
spring.datasource.url = jdbc:mysql://localhost:3306/notes_app?autoReconnect=true&useUnicode=true&characterEncoding=UTF-8&allowMultiQueries=true&useSSL=false
spring.datasource.username = root
spring.datasource.password = callicoder


## Hibernate Properties

# The SQL dialect makes Hibernate generate better SQL for the chosen database
spring.jpa.properties.hibernate.dialect = org.hibernate.dialect.MySQL5InnoDBDialect

# Hibernate ddl auto (create, create-drop, validate, update)
spring.jpa.hibernate.ddl-auto = update
```
eb deploy
eb setenv SERVER_PORT=5000
eb open
```
## How to connecting amazon rds mysql using phpmyadmin
> - Go to link: https://ap-southeast-1.console.aws.amazon.com/rds/home?region=ap-southeast-1#launch-dbinstance:
> - Settings:
>> - DB Instance: Webserver
>> - Master username: webserver
>> - Password: keep old
c
> - Database Options:
>> - Database name: genealogy
>> - Port: 3306
>> - Endpoint: webserver.cohablpe3kal.ap-southeast-1.rds.amazonaws.com
>> - mysql -h mysql–instance1.123456789012.us-east-1.rds.amazonaws.com -P 3306 -u mymasteruser -p
>> Go to xampp/mysql to detect **mysql** 
>>> - Path of drive: C:\xampp\htdocs\rsd-phpmyadmin
>>> - Website: http://localhost/rsd-phpmyadmin/setup/
>>>> - New Server: localhost/
>>>> - Link: eb setenv SPRING_DATASOURCE_URL=jdbc:mysql://webserver.cohablpe3kal.ap-southeast-1.rds.amazonaws.com:3306/ebdb SPRING_DATASOURCE_USERNAME=webserver SPRING_DATASOURCE_PASSWORD=m00Lorencedeveloper

## Go to EC2 Management Console
> - Link to: https://ap-southeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-southeast-1#Home:
https://ap-southeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-southeast-1#LoadBalancers:sort=loadBalancerName
> - Create 




