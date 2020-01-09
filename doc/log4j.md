# Attributes
- url
    _required_. HEC URL
- token
    _required_. HEC token
- channel
    HEC channel
- type
    "Raw" if '/services/collector/raw' endpoint is to be used
- name
  _required_. The name of the appender being configured.
- source
    Splunk source field to use
- sourcetype
    Splunk sourcetype field to use
- host
    Splunk host field to use
- index
    Splunk index to use
- messageFormat
    "text" or "json". Default is "text"
- ignoreExceptions
    _boolean_, default 'true'
- batch_size_bytes
    Default is Long.MAX_VALUE if batch_size_count is set, 0 otherwise
- batch_size_count
    Default is Long.MAX_VALUE if batch_size_bytes is set, 0 otherwise
- batch_interval
    Time in milliseconds to batch data in order to send a single transmission
    to Splunk.
- retries_on_error
    integer.
- send_mode
    "sequential" or "parallel". If sequential, only one thread is assigned to 
    the HTTP client thread pool.
- middleware
    class name.
- disableCertificateValidation
    Allow self-signed SSL certificates from Splunk
- eventBodySerializer
    class name
- includeLoggerName
    _boolean_, default 'true'
- includeThreadName
    _boolean_, default 'true'
- includeMDC
    _boolean_, default 'true'
- includeException
    _boolean_, default 'true'
- includeMarker
    _boolean_, default 'true'
# Elements
The following are standard Log4J elements that are used to format and filter
log entries before transmission to Splunk. Refer to the Log4J documentation for
details.

- Layout
    default:   Uses the pattern "%m" witha UTF-8 charset, writes
     exceptions, and           layout = PatternLayout.newBuilder()
    
                                 .withPattern("%m")
                                 .withCharset(StandardCharsets.UTF_8)
                                 .withAlwaysWriteExceptions(true)
                                 .withNoConsoleNoAnsi(false)
                                 .build();
- Filter

# Example

```xml

<Configuration status="info" name="example" packages="com.splunk.logging">
    <Appenders>
        <SplunkHttp name="http-input"
              url="http://localhost:5555"
              token="11111111-2222-3333-4444-555555555555"
              index="application_logs"
              source="splunktest"
              sourcetype="java_log4j"
              messageFormat="text"
              batch_interval="250"
              disableCertificateValidation="true">
            <PatternLayout pattern="%m"/>
        </SplunkHttp>
    </Appenders>

    <Loggers>
        <Root level="INFO">
            <AppenderRef ref="http-input"/>
        </Root>
    </Loggers>

</Configuration>
```
