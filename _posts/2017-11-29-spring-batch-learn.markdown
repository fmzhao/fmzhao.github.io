---
title: Spring Batchѧϰ
layout: post
category: spring java
tags: framework springbatch
---

**Spring Batch**��һ����������*������*��ҵ���������������ܡ�

> ������һϵ��û���û������Զ���ɵĸ��������ִ�й��̡�

### Ŀ¼

- [1. Spring Batch��ʲô?](#1)
- [2. Spring Batch��Ŀ](#2)
    - [2.1 Spring Batch��������Java��Ŀ](#2.1)
    - [2.2 Spring Batch XML-To-MysqlJava��Ŀ](#2.2)

---

<h3 id="1">1. Spring Batch��ʲ?</h3>

Spring Batch��ܳ����ṩ*������*�����⣬��ܻ��ṩ��

- ��־�͸���
- �������
- Job����ͳ��
- Job����
- ����(Skip)����Դ����

Spring Batch������

- �����
    - �޸�xml�ļ����Ըı�������Ӧ�õ�ִ��˳��
- ��ά����
    - ������Job��ÿһ��Step�ǽ���ģ����Զ������ԣ�����
- ����չ��
    - ����ִ��������Job�еĶ��Step
    - ����ִ��һ�������߳�
- ֧�ֶ��ļ���ʽ
    - XML, Flat files, CSV, MYSQL, Hibernate, JDBC, Mongo, Neo4j, ect 
- �෽������������Job
    - Java����, Web����, �����е�

---

<h3 id="2">2. Spring Batch��Ŀ</h3>

<h4 id="2.1">2.1 Spring Batch��������Java��Ŀ</h4>

**1. **����һ��maven��Ŀ

**2. **�޸�pom�ļ�

    <project xmlns = "http://maven.apache.org/POM/4.0.0" 
       xmlns:xsi = "http://www.w3.org/2001/XMLSchema-instance" 
       xsi:schemaLocation = "http://maven.apache.org/POM/4.0.0 
       http://maven.apache.org/maven-v4_0_0.xsd"> 
       <modelVersion>4.0.0</modelVersion> 
       <groupId>com.fmz.springbatch</groupId> 
       <artifactId>SpringBatchSample</artifactId> 
       <packaging>jar</packaging> 
       <version>1.0-SNAPSHOT</version> 
       <name>SpringBatchSample</name>
       <url>http://maven.apache.org</url>  
     
       <properties> 
          <jdk.version>1.7</jdk.version> 
          <spring.version>4.3.8.RELEASE</spring.version> 
          <spring.batch.version>3.0.7.RELEASE</spring.batch.version> 
          <mysql.driver.version>5.1.25</mysql.driver.version> 
          <junit.version>4.11</junit.version> 
       </properties>  
       
       <dependencies> 
          <!-- Spring Core --> 
          <dependency> 
             <groupId>org.springframework</groupId> 
             <artifactId>spring-core</artifactId> 
             <version>${spring.version}</version> 
          </dependency>  
          
          <!-- Spring jdbc, for database --> 
          <dependency> 
             <groupId>org.springframework</groupId> 
             <artifactId>spring-jdbc</artifactId> 
             <version>${spring.version}</version> 
          </dependency>  
          
          <!-- Spring XML to/back object --> 
          <dependency> 
             <groupId>org.springframework</groupId> 
             <artifactId>spring-oxm</artifactId> 
             <version>${spring.version}</version> 
          </dependency>  
      
          <!-- Spring Batch dependencies --> 
          <dependency> 
             <groupId>org.springframework.batch</groupId> 
             <artifactId>spring-batch-core</artifactId> 
             <version>${spring.batch.version}</version> 
          </dependency> 
      
          <dependency> 
             <groupId>org.springframework.batch</groupId> 
             <artifactId>spring-batch-infrastructure</artifactId> 
             <version>${spring.batch.version}</version> 
          </dependency>  
      
          <!-- Spring Batch unit test --> 
          <dependency> 
             <groupId>org.springframework.batch</groupId> 
             <artifactId>spring-batch-test</artifactId> 
             <version>${spring.batch.version}</version> 
          </dependency>  
      
          <!-- Junit --> 
          <dependency> 
             <groupId>junit</groupId> 
             <artifactId>junit</artifactId> 
             <version>${junit.version}</version> 
             <scope>test</scope> 
          </dependency> 
       </dependencies> 
     
       <build> 
          <finalName>spring-batch</finalName> 
          <plugins> 
             <plugin> 
                <groupId>org.apache.maven.plugins</groupId> 
                <artifactId>maven-eclipse-plugin</artifactId>
                <version>2.9</version> 
                <configuration> 
                   <downloadSources>true</downloadSources> 
                   <downloadJavadocs>false</downloadJavadocs> 
                </configuration> 
             </plugin> 
          
             <plugin> 
                <groupId>org.apache.maven.plugins</groupId> 
                <artifactId>maven-compiler-plugin</artifactId> 
                <version>2.3.2</version> 
                <configuration> 
                   <source>${jdk.version}</source> 
                   <target>${jdk.version}</target> 
                </configuration> 
             </plugin> 
          </plugins> 
       </build> 
    </project>     

**3. **��������ļ�

    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns = "http://www.springframework.org/schema/beans" 
       xmlns:batch = "http://www.springframework.org/schema/batch" 
       xmlns:xsi = "http://www.w3.org/2001/XMLSchema-instance" 
       xsi:schemaLocation = "http://www.springframework.org/schema/batch 
          http://www.springframework.org/schema/batch/spring-batch-2.2.xsd
          http://www.springframework.org/schema/beans
          http://www.springframework.org/schema/beans/spring-beans-3.2.xsd "> 
        <import resource="context.xml" />
        <bean id = "tasklet" class = "com.fmz.springbatch.springbatchsample.MyTasklet" /> 
        <!-- Defining a job--> 
        <batch:job id = "helloWorldJob">  
           <!-- Defining a Step --> 
           <batch:step id = "step1"> 
              <tasklet ref = "tasklet"/>   
           </batch:step>    
        </batch:job>  
    </beans> 

> �������ļ���jobConfig.xml������Job��steps of Job(readers or writers)

    <beans xmlns = "http://www.springframework.org/schema/beans" 
       xmlns:xsi = "http://www.w3.org/2001/XMLSchema-instance" 
       xsi:schemaLocation = "http://www.springframework.org/schema/beans 
          http://www.springframework.org/schema/beans/spring-beans-3.2.xsd">  
       
       <bean id = "jobRepository"   
          class="org.springframework.batch.core.repository.support.MapJobRepositoryFactoryBean"> 
          <property name = "transactionManager" ref = "transactionManager" /> 
       </bean>     
         
       <bean id = "transactionManager" 
          class = "org.springframework.batch.support.transaction.ResourcelessTransactionManager" /> 
          
       <bean id = "jobLauncher" 
          class = "org.springframework.batch.core.launch.support.SimpleJobLauncher"> 
          <property name = "jobRepository" ref = "jobRepository" /> 
       </bean> 
    </beans>

> context.xml�����ã�job repository, job launcher, transaction manager

**4. **����tasklet

    package com.fmz.springbatch.springbatchsample;

    import org.springframework.batch.core.StepContribution; 
    import org.springframework.batch.core.scope.context.ChunkContext;
    import org.springframework.batch.core.step.tasklet.Tasklet;
    import org.springframework.batch.repeat.RepeatStatus;  

    public class MyTasklet implements Tasklet { 
       
       @Override 
       public RepeatStatus execute(StepContribution arg0, ChunkContext arg1) throws Exception {  
          System.out.println("Hello This is a sample example of spring batch"); 
          return RepeatStatus.FINISHED; 
       } 
    } 

**5. **����������

    package com.fmz.springbatch.springbatchsample;

    import org.springframework.batch.core.Job; 
    import org.springframework.batch.core.JobExecution; 
    import org.springframework.batch.core.JobParameters; 
    import org.springframework.batch.core.launch.JobLauncher; 
    import org.springframework.context.ApplicationContext; 
    import org.springframework.context.support.ClassPathXmlApplicationContext;

    public class App { 
       public static void main(String[] args)throws Exception { 
      
          // System.out.println("hello"); 
          //String[] springConfig  =  {"jobConfig.xml"};  
          
          // Creating the application context object  
          ApplicationContext context = new ClassPathXmlApplicationContext("jobConfig.xml"); 
          
          // Creating the job launcher 
          JobLauncher jobLauncher = (JobLauncher) context.getBean("jobLauncher"); 
      
          // Creating the job 
          Job job = (Job) context.getBean("helloWorldJob"); 
      
          // Executing the JOB 
          JobExecution execution = jobLauncher.run(job, new JobParameters()); 
          System.out.println("Exit Status : " + execution.getStatus()); 
       }    
    }

---

<h4 id="2.2">2.2 Spring Batch XML-To-Mysql Java��Ŀ</h4>

> ��xml�ļ����ݱ��浽MySQL���ݿ⣬ͬʱд��PDF�ļ���

**1. **����2.1������������Java��Ŀ

    <project xmlns = "http://maven.apache.org/POM/4.0.0" 
       xmlns:xsi = "http://www.w3.org/2001/XMLSchema-instance" 
       xsi:schemaLocation = "http://maven.apache.org/POM/4.0.0 
       http://maven.apache.org/maven-v4_0_0.xsd"> 
       <modelVersion>4.0.0</modelVersion> 
       <groupId>com.fmz.springbatch</groupId> 
       <artifactId>SpringBatchXmlToMysqlDemo</artifactId> 
       <packaging>jar</packaging> 
       <version>1.0-SNAPSHOT</version> 
       <name>SpringBatchXmlToMysqlDemo</name>
       <url>http://maven.apache.org</url>  
     
       <properties> 
          <jdk.version>1.7</jdk.version> 
          <spring.version>4.3.8.RELEASE</spring.version> 
          <spring.batch.version>3.0.7.RELEASE</spring.batch.version> 
          <mysql.driver.version>5.1.25</mysql.driver.version> 
          <junit.version>4.11</junit.version> 
       </properties>  
       
       <dependencies> 
          <!-- Spring Core --> 
          <dependency> 
             <groupId>org.springframework</groupId> 
             <artifactId>spring-core</artifactId> 
             <version>${spring.version}</version> 
          </dependency>  
          
          <!-- Spring jdbc, for database --> 
          <dependency> 
             <groupId>org.springframework</groupId> 
             <artifactId>spring-jdbc</artifactId> 
             <version>${spring.version}</version> 
          </dependency>  
          
          <!-- Spring XML to/back object --> 
          <dependency> 
             <groupId>org.springframework</groupId> 
             <artifactId>spring-oxm</artifactId> 
             <version>${spring.version}</version> 
          </dependency>  
       
          <!-- MySQL database driver --> 
          <dependency> 
             <groupId>mysql</groupId> 
             <artifactId>mysql-connector-java</artifactId>
             <version>${mysql.driver.version}</version> 
          </dependency>  
      
          <!-- Spring Batch dependencies --> 
          <dependency> 
             <groupId>org.springframework.batch</groupId> 
             <artifactId>spring-batch-core</artifactId> 
             <version>${spring.batch.version}</version> 
          </dependency> 
      
          <dependency> 
             <groupId>org.springframework.batch</groupId> 
             <artifactId>spring-batch-infrastructure</artifactId> 
             <version>${spring.batch.version}</version> 
          </dependency>  
      
          <!-- Spring Batch unit test --> 
          <dependency> 
             <groupId>org.springframework.batch</groupId> 
             <artifactId>spring-batch-test</artifactId> 
             <version>${spring.batch.version}</version> 
          </dependency>  
      
          <!-- Junit --> 
          <dependency> 
             <groupId>junit</groupId> 
             <artifactId>junit</artifactId> 
             <version>${junit.version}</version> 
             <scope>test</scope> 
          </dependency> 
          
          <dependency>
            <groupId>org.apache.pdfbox</groupId>
            <artifactId>pdfbox</artifactId>
            <version>2.0.8</version>
          </dependency>
       </dependencies> 
     
       <build> 
          <finalName>spring-batch</finalName> 
          <plugins> 
             <plugin> 
                <groupId>org.apache.maven.plugins</groupId> 
                <artifactId>maven-eclipse-plugin</artifactId>
                <version>2.9</version> 
                <configuration> 
                   <downloadSources>true</downloadSources> 
                   <downloadJavadocs>false</downloadJavadocs> 
                </configuration> 
             </plugin> 
          
             <plugin> 
                <groupId>org.apache.maven.plugins</groupId> 
                <artifactId>maven-compiler-plugin</artifactId> 
                <version>2.3.2</version> 
                <configuration> 
                   <source>${jdk.version}</source> 
                   <target>${jdk.version}</target> 
                </configuration> 
             </plugin> 
          </plugins> 
       </build> 
    </project>     

> pom.xml

**2. **��������ļ�

    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns = "http://www.springframework.org/schema/beans" 
       xmlns:batch = "http://www.springframework.org/schema/batch" 
       xmlns:xsi = "http://www.w3.org/2001/XMLSchema-instance" 
       xmlns:util = "http://www.springframework.org/schema/util" 
       xsi:schemaLocation = "http://www.springframework.org/schema/batch 
        
          http://www.springframework.org/schema/batch/spring-batch-2.2.xsd 
          http://www.springframework.org/schema/beans 
          http://www.springframework.org/schema/beans/spring-beans-3.2.xsd 
          http://www.springframework.org/schema/util     
          http://www.springframework.org/schema/util/spring-util-3.0.xsd ">  
      
       <import resource = "context.xml" /> 
      
       <bean id = "itemProcessor" class = "com.fmz.springbatch.step.CustomItemProcessor" /> 
       <batch:job id = "helloWorldJob"> 
          <batch:step id = "step1"> 
             <batch:tasklet>           
                <batch:chunk reader = "xmlItemReader" writer = "mysqlItemWriter" processor = "itemProcessor" commit-interval="10">
                </batch:chunk> 
             </batch:tasklet> 
          </batch:step> 
       </batch:job> 
                    
       <bean id = "xmlItemReader" 
          class = "org.springframework.batch.item.xml.StaxEventItemReader"> 
          <property name = "fragmentRootElementName" value = "tutorial" /> 
          <property name = "resource" value = "classpath:resources/tutorial.xml" /> 
          <property name = "unmarshaller" ref = "customUnMarshaller" /> 
       </bean> 
          
       <bean id = "customUnMarshaller" class = "org.springframework.oxm.xstream.XStreamMarshaller">
          <property name = "aliases"> 
             <util:map id = "aliases"> 
                <entry key = "tutorial" value = "com.fmz.springbatch.bean.Tutorial" />            
             </util:map> 
          </property> 
       </bean>  
       <bean id = "mysqlItemWriter" class = "org.springframework.batch.item.database.JdbcBatchItemWriter"> 
          <property name = "dataSource" ref = "dataSource" /> 
          <property name = "sql"> 
             <value> 
                <![CDATA[insert into test.tutorials (tutorial_id, tutorial_author, tutorial_title, 
                   submission_date, tutorial_icon, tutorial_description) 
                   values (:tutorial_id, :tutorial_author, :tutorial_title, :submission_date, 
                   :tutorial_icon, :tutorial_description);]]>
             </value> 
          </property>   
          
          <property name = "itemSqlParameterSourceProvider"> 
             <bean class = "org.springframework.batch.item.database.BeanPropertyItemSqlParameterSourceProvider" /> 
          </property> 
       </bean> 
    </beans>   

> jobConfig.xml

    <beans xmlns = "http://www.springframework.org/schema/beans" 
       xmlns:jdbc = "http://www.springframework.org/schema/jdbc" 
       xmlns:xsi = "http://www.w3.org/2001/XMLSchema-instance" 
       xsi:schemaLocation = "http://www.springframework.org/schema/beans 
          http://www.springframework.org/schema/beans/spring-beans-3.2.xsd 
          http://www.springframework.org/schema/jdbc 
          http://www.springframework.org/schema/jdbc/spring-jdbc-3.2.xsd"> 
       
       <!-- stored job-meta in database -->
       <bean id = "jobRepository" 
          class = "org.springframework.batch.core.repository.support.JobRepositoryFactoryBean"> 
          <property name = "dataSource" ref = "dataSource" /> 
          <property name = "transactionManager" ref = "transactionManager" /> 
          <property name = "databaseType" value = "mysql" /> 
       </bean>  
     
       <bean id = "transactionManager" 
       class = "org.springframework.batch.support.transaction.ResourcelessTransactionManager" />  
       <bean id = "jobLauncher" 
          class = "org.springframework.batch.core.launch.support.SimpleJobLauncher"> 
          <property name = "jobRepository" ref = "jobRepository" /> 
       </bean> 
      
       <!-- connect to MySQL database --> 
       <bean id = "dataSource" 
          class = "org.springframework.jdbc.datasource.DriverManagerDataSource"> 
          <property name = "driverClassName" value = "com.mysql.jdbc.Driver" /> 
          <property name = "url" value = "jdbc:mysql://localhost:3306/test" /> 
          <property name = "username" value = "fmz" /> 
          <property name = "password" value = "147258" /> 
       </bean>  
     
       <!-- create job-meta tables automatically --> 
       <jdbc:initialize-database data-source = "dataSource">   
          <jdbc:script location = "org/springframework/batch/core/schema-drop-mysql.sql"/>   
          <jdbc:script location = "org/springframework/batch/core/schema-mysql.sql"/> 
       </jdbc:initialize-database> 
    </beans>   

> context.xml

**3. **�����Դ�ļ�

    <?xml version="1.0" encoding="UTF-8"?> 
    <tutorials> 
       <tutorial>      
          <tutorial_id>1001</tutorial_id> 
          <tutorial_author>Sanjay</tutorial_author> 
          <tutorial_title>Learn Java</tutorial_title> 
          <submission_date>06-05-2007</submission_date> 
          <tutorial_icon>https://www.tutorialspoint.com/java/images/java-minilogo.jpg</tutorial_icon> 
          <tutorial_description>Java is a high-level programming language originally 
             developed by Sun Microsystems and released in 1995. 
             Java runs on a variety of platforms. 
             This tutorial gives a complete understanding of Java.');</tutorial_description> 
       </tutorial> 
        
       <tutorial>      
          <tutorial_id>1002</tutorial_id> 
          <tutorial_author>Abdul S</tutorial_author> 
          <tutorial_title>Learn MySQL</tutorial_title> 
          <submission_date>19-04-2007</submission_date> 
          <tutorial_icon>https://www.tutorialspoint.com/mysql/images/mysql-minilogo.jpg</tutorial_icon> 
          <tutorial_description>MySQL is the most popular 
             Open Source Relational SQL database management system. 
             MySQL is one of the best RDBMS being used for developing web-based software applications. 
             This tutorial will give you quick start with MySQL 
             and make you comfortable with MySQL programming.</tutorial_description> 
       </tutorial> 
        
       <tutorial>
          <tutorial_id>1003</tutorial_id> 
          <tutorial_author>Krishna Kasyap</tutorial_author> 
          <tutorial_title>Learn JavaFX</tutorial_title> 
          <submission_date>06-07-2017</submission_date> 
          <tutorial_icon>https://www.tutorialspoint.com/javafx/images/javafx-minilogo.jpg</tutorial_icon> 
          <tutorial_description>JavaFX is a Java library used to build Rich Internet Applications. 
             The applications developed using JavaFX can run on various devices 
             such as Desktop Computers, Mobile Phones, TVs, Tablets, etc. 
             This tutorial, discusses all the necessary elements of JavaFX that are required
             to develop effective Rich Internet Applications</tutorial_description> 
       </tutorial> 
    </tutorials>

> tutorial.xml���ļ�·����`CLASSPATH:resources/tutorial.xml`

**4. **Bean�ļ�

    package com.fmz.springbatch.bean;

    public class Tutorial { 
           private int tutorial_id; 
           private String tutorial_author; 
           private String tutorial_title; 
           private String submission_date; 
           private String tutorial_icon; 
           private String tutorial_description;   
           
           @Override 
           public String toString() { 
              return " [id=" + tutorial_id + ", author=" + tutorial_author  
                 + ", title=" + tutorial_title + ", date=" + submission_date + ", icon =" 
                 +tutorial_icon +", description = "+tutorial_description+"]"; 
           }  
           
           public int getTutorial_id() { 
              return tutorial_id; 
           }  
           
           public void setTutorial_id(int tutorial_id) { 
              this.tutorial_id = tutorial_id; 
           }  
           
           public String getTutorial_author() { 
              return tutorial_author; 
           }  
           
           public void setTutorial_author(String tutorial_author) { 
              this.tutorial_author = tutorial_author; 
           }  
           
           public String getTutorial_title() { 
              return tutorial_title; 
           } 
           
           public void setTutorial_title(String tutorial_title) { 
              this.tutorial_title = tutorial_title; 
           }  
           
           public String getSubmission_date() { 
              return submission_date; 
           }  
           
           public void setSubmission_date(String submission_date) { 
              this.submission_date = submission_date; 
           }  
           
           public String getTutorial_icon() { 
              return tutorial_icon; 
           }  
           
           public void setTutorial_icon(String tutorial_icon) { 
              this.tutorial_icon = tutorial_icon; 
           }  
           
           public String getTutorial_description() { 
              return tutorial_description; 
           }  
           
           public void setTutorial_description(String tutorial_description) { 
              this.tutorial_description = tutorial_description; 
           } 
        }

**5. **Mapper�ļ�

    package com.fmz.springbatch.mapper;

    import org.springframework.batch.item.file.mapping.FieldSetMapper; 
    import org.springframework.batch.item.file.transform.FieldSet; 
    import org.springframework.validation.BindException;  

    import com.fmz.springbatch.bean.Tutorial;

    public class TutorialFieldSetMapper implements FieldSetMapper<Tutorial> { 
       
       @Override 
       public Tutorial mapFieldSet(FieldSet fieldSet) throws BindException {   
          // instantiating the Tutorial class 
          Tutorial tutorial = new Tutorial(); 
       
          // Setting the fields from XML 
          tutorial.setTutorial_id(fieldSet.readInt(0));   
          tutorial.setTutorial_title(fieldSet.readString(1)); 
          tutorial.setTutorial_author(fieldSet.readString(2)); 
          tutorial.setTutorial_icon(fieldSet.readString(3)); 
          tutorial.setTutorial_description(fieldSet.readString(4));   
          return tutorial;  
       }  
    } 

**6. **Job�����ļ�

    package com.fmz.springbatch.step;

    import java.io.File; 
    import java.io.IOException;  

    import org.apache.pdfbox.pdmodel.PDDocument; 
    import org.apache.pdfbox.pdmodel.PDPage; 
    import org.apache.pdfbox.pdmodel.PDPageContentStream; 
    import org.apache.pdfbox.pdmodel.font.PDType1Font; 
    import org.springframework.batch.item.ItemProcessor;  

    import com.fmz.springbatch.bean.Tutorial;

    public class CustomItemProcessor implements ItemProcessor<Tutorial, Tutorial> {  
       
       public static void drawTable(PDPage page, PDPageContentStream contentStream, 
          float y, float margin, String[][] content) throws IOException { 
          final int rows = content.length; 
          final int cols = content[0].length; 
          final float rowHeight = 50; 
          final float tableWidth = page.getMediaBox().getWidth()-(2*margin); 
          final float tableHeight = rowHeight * rows; 
          final float colWidth = tableWidth/(float)cols; 
          final float cellMargin=5f;  
          
          // draw the rows 
          float nexty = y ; 
          for (int i = 0; i <= rows; i++) {   
             contentStream.drawLine(margin,nexty,margin+tableWidth,nexty);
             nexty-= rowHeight; 
          }  
          
          //draw the columns 
          float nextx = margin; 
          for (int i = 0; i <= cols; i++) {
             contentStream.drawLine(nextx,y,nextx,y-tableHeight); 
             nextx += colWidth; 
          }  
          
          // now add the text    
          contentStream.setFont(PDType1Font.HELVETICA_BOLD,12);  
          
          float textx = margin+cellMargin; 
          float texty = y-15; 
          for(int i = 0; i < content.length; i++){ 
             for(int j = 0 ; j < content[i].length; j++){ 
                String text = content[i][j]; 
                contentStream.beginText(); 
                contentStream.moveTextPositionByAmount(textx,texty); 
                contentStream.drawString(text); 
                contentStream.endText(); 
                textx += colWidth; 
             } 
            
             texty-=rowHeight; 
             textx = margin+cellMargin; 
          } 
       }  
       
       @Override 
       public Tutorial process(Tutorial item) throws Exception { 
          System.out.println("Processing..." + item); 
       
          // Creating PDF document object 
          PDDocument doc = PDDocument.load(new File("E:/test.pdf"));     
          
          // Creating a blank page 
          PDPage page = new PDPage(); 
          doc.addPage( page ); 
          PDPageContentStream contentStream =  new PDPageContentStream(doc, page);  
          
          String[][] content = {{"Id",""+item.getTutorial_id()},
          {"Title", item.getTutorial_title()}, 
          {"Authour", item.getTutorial_author()}, 
          {"Submission Date", item.getSubmission_date()}} ;  
          drawTable(page, contentStream, 700, 100, content);       
          
          contentStream.close(); 
          doc.save("E:/test.pdf" ); 
          System.out.println("Hello"); 
          return item; 
       }    
    }  

**7. **�������

    package com.fmz.springbatch;

    import org.springframework.batch.core.Job;
    import org.springframework.batch.core.JobParameters;
    import org.springframework.batch.core.launch.JobLauncher;
    import org.springframework.context.ApplicationContext;
    import org.springframework.context.support.ClassPathXmlApplicationContext;

    public class App {
        public static void main(String[] args) throws Exception {
            String[] springConfig = { "jobConfig.xml" };

            // Creating the application context object
            ApplicationContext context = new ClassPathXmlApplicationContext(
                    springConfig);

            // Creating the job launcher
            JobLauncher jobLauncher = (JobLauncher) context.getBean("jobLauncher");

            // Creating the job
            Job job = (Job) context.getBean("helloWorldJob");

            // Executing the JOB
            org.springframework.batch.core.JobExecution execution = jobLauncher
                    .run(job, new JobParameters());
            System.out.println("Exit Status : " + execution.getStatus());
        }
    }

---
