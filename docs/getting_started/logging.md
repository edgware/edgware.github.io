---
layout: default
title: Edgware log files
---   

Edgware logging is a useful source of diagnostic information for use in problem determination. Logging information is written to the console, and saved in a file in the following directory:

**Windows:**

	%FABRIC_HOME%\log

**Linux and OS X:**

	$FABRIC_HOME/log

### Configuring logging

The level of detail included in log output can be controlled via the configuration file `fabricConfig_default.properties` in the directory:

**Windows:**

	%FABRIC_HOME%\osgi\configuration

**Linux and OS X:**

	$FABRIC_HOME/osgi\configuration

The following configuration values are available:

| Configuration Property                   | Default Value | Description |
| ---------------------------------------- | ------------- | ----------- |
| `java.util.logging.FileHandler.level`    | `FINE`        | The logging level for log file output.
| `java.util.logging.ConsoleHandler.level` | `INFO`        | The logging level for console output.
| `org.eclipse.paho.client.mqttv3.level`   | `WARNING`     | The logging level for the MQTT API.
| `logging.messages.long`                  | `false`       | `true` for long log messages containing additional detail information, `false` for short log messages.

A description of the valid logging level values can be found [on-line](http://docs.oracle.com/javase/7/docs/api/java/util/logging/Level.html). Note that low level logging will generate copious output and will slow the system down appreciably.