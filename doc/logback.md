# Settings
- url
- token
- channel
- type
- layout
- includeLoggerName (bool)
- includeThreadName (bool)
- includeMDC
- includeException
- source
- sourcetype
- messageFormat
- host
- index
- eventBodySerializer
- disableCertificateValidation
- batch_size_count
- batch_size_bytes
- batch_interval
- retries_on_error
- send_mode
- middleware

# Example

Logback is configured via an XML config file located in the JVM classpath. For
details on how Logback manages loggers and configuration refer to the Logback
documentation.

```xml
<configuration>
    <appender name="splunk" class="com.splunk.logging
.HttpEventCollectorLogbackAppender">
        <url>http://localhost:5555</url>
        <token>11111111-2222-3333-4444-555555555555</token>
        <source>splunktest</source>
        <sourcetype>java_logging</sourcetype>
        <messageFormat>text</messageFormat>
        <batch_interval>250</batch_interval>
        <layout class="ch.qos.logback.classic.PatternLayout">
            <pattern>%msg</pattern>
        </layout>
    </appender>

    <root level="INFO">
        <appender-ref ref="splunk"/>
    </root>
</configuration>
```
