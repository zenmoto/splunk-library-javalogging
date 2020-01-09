# Settings
- host
- index
- source
- sourcetype
- messageformat
- url
- token
- channel
- type
- batch_interval
- batch_size_count
- batch_size_bytes
- retries_on_error
- send_mode
  Default: "sequential"
- middleware
- eventBodySerializer
- include_logger_name
    Boolean, default: true
- include_thread_name
    Boolean, default: true
- include_exception
    Boolean, default: true
    
# Example

To configure `java.util.logging`, pass define the `java.util.logging.config.file`
property when executing the JVM. Note that the Splunk Java logging library will
need to be on the classpath.

```shell script
java -Djava.util.logging.config.file=splunk-logger.properties com.example.MainClass
```

```properties
# Splunk http event collector handler
handlers=com.splunk.logging.HttpEventCollectorHandler

# Http event collector application token
com.splunk.logging.HttpEventCollectorLoggingHandler.token=81029a58-63db-4bef-9c6f-f6b7e500f098

# Splunk logging input url.
com.splunk.logging.HttpEventCollectorLoggingHandler.url=https://localhost:8089

# Logging events metadata.
com.splunk.logging.HttpEventCollectorLoggingHandler.index=main
com.splunk.logging.HttpEventCollectorLoggingHandler.source=myprogram
com.splunk.logging.HttpEventCollectorLoggingHandler.sourcetype=java_logging

# Events batching parameters:

# Accumulate events for up to a quarter second and send them all at once.
# Higher values improve throughput and efficiency at the expense of latency
com.splunk.logging.HttpEventCollectorLoggingHandler.batch_interval=250

# Max number of events in a batch. Default is 0, meaning that events are sent
# immediately. If batch_interval is set and this value is unset, the number 
# of events in a batch are unbounded. If both are set, then the batch will be
# sent when either limit is satisfied.
com.splunk.logging.HttpEventCollectorLoggingHandler.batch_size_count=50

# Adds a constraint on the overall size of the serialized batch. A value of
# 0 (the default) disables the constraint.
com.splunk.logging.HttpEventCollectorLoggingHandler.batch_size_bytes=0

```
