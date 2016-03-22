#### 参考文档:
[http://logback.qos.ch/manual/configuration.html#fileInclusion](http://logback.qos.ch/manual/configuration.html#fileInclusion)
#### logback.xml
```xml

<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration>
<configuration debug="true" scan="true" scanPeriod="30 seconds">

    <statusListener class="ch.qos.logback.core.status.OnConsoleStatusListener" />

    <property name="LOG_DIR" value="/home/product/logs/java_logs" />

    <appender name="console" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>[%date{yyyy-MM-dd HH:mm:ss}][%p][%thread][%X{MSG}][%C][%M][%L][%m]%n</pattern>
            <charset>UTF-8</charset>
        </encoder>
    </appender>

    <appender name="rollingFile" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <file>${LOG_DIR}/stdout.log</file>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <fileNamePattern>${LOG_DIR}/stdout.%d{yyyy-MM-dd}.%i.log</fileNamePattern>
            <timeBasedFileNamingAndTriggeringPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedFNATP">
                <maxFileSize>20MB</maxFileSize>
            </timeBasedFileNamingAndTriggeringPolicy>
        </rollingPolicy>
        <encoder>
            <pattern>[%date{yyyy-MM-dd HH:mm:ss}][%p][%thread][%X{MSG}][%C][%M][%L][%m]%n</pattern>
            <charset>UTF-8</charset>
        </encoder>
    </appender>

    <root level="debug">
        <appender-ref ref="console"/>
        <appender-ref ref="rollingFile"/>
    </root>
    <!-- 从classpath import-->
    <include resource="logback-monitor.xml"/>
</configuration>

```

#### logback-monitor.xml
注意：被引入的文件内容是以included标签作为根节点的，并不是标准的logback配置文件,就是说不需要configuration标签

```xml

<included>
    <!-- 日志监控 -->
    <property name="MONITORLOG_DIR" value="/home/product/logs/monitor" />

    <appender name="MONITOR_APPENDER" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <prudent>true</prudent>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <fileNamePattern>${MONITORLOG_DIR}/provider_service.%d{yyyy-MM-dd}.monitor</fileNamePattern>
            <maxHistory>30</maxHistory>
        </rollingPolicy>
        <encoder>
            <Pattern>%msg%n</Pattern>
        </encoder>
    </appender>

    <logger name="MONITOR_LOG" level="info" additivity="false">
        <appender-ref ref="MONITOR_APPENDER" />
    </logger>

</included>

```