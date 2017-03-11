# ArcSight--Elastic

This document demonstrates how to integrate ArcSight with Elastic using Apache Syslog Smartconnector. 
We'll be monitoring Apache Logs with the following architecture  -> 

Apache Server -> Syslog Connector -> Logstash (via CEF codec Plugin) -> Elasticsearch -> Kibana

1). In this case we are sending events to Logstash TCP Port 5100, refer to attach Logstash.conf file. 
Start Elastisearch
Start Kibana
Start Logstash using the Logstash.conf file => bin/logstash -f logstash.conf

2). Things to be done on Apache Server side:

Edit the file /etc/httpd/conf/httpd.conf and add the entries:
  ErrorLog "| /usr/bin/logger -t 'apache_error_log' " 
  CustomLog "| /usr/bin/logger -t 'apache_access_log' " combined
  
This will send all access and error logs to syslog on the localhost. If you are forwarding events to a remote log host, the /etc/rsyslog.conf file should be modified with the appropriate hostname/IP with Port number. 
For instance: #*.* @@remote-host:Port number
Double @@ for TCP and single for UDP

Restart syslog and httpd after making those changes. 

3). Install Syslog Daemon, File or Pipe connector.
    Syslog Daemon : It will listen on the specified port for syslog events. 
    Syslog File: Enter the full path name for the file from which this connector will read events.
    Syslog Pipe: Specify the absolute path to the pipe. 
When setting up the destination enter the hostname and port where Logstash is installed and listening on that port. Make sure that you already have Logstash up and running on that port otherwise the connector will give 'Destination unreachable error' since that TCP port is not listening currently. 
Start the connector => bin/arcsight agents

Check the attached Dashboard as a sample output on Kibana. 
