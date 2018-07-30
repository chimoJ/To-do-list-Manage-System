/first-webapplication/src/main/resources/log4j.properties
---
    log4j.rootLogger=TRACE, Appender1
 
    log4j.appender.Appender1=org.apache.log4j.ConsoleAppender
    log4j.appender.Appender1.layout=org.apache.log4j.PatternLayout
    log4j.appender.Appender1.layout.ConversionPattern=%-7p %d [%t] %c %x - %m%n
    #TRACE
    #DEBUG
    #INFO
    #WARN
    #ERROR
/first-webapplication/src/main/resources/messages_en.properties
---
    welcome.message=Welcome in English
    todo.caption= Todo Caption in English
/first-webapplication/src/main/resources/messages_fr.properties
---
    welcome.message=Welcome in French
    todo.caption= Todo Caption in French
