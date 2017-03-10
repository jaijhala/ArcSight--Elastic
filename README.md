# ArcSight--Elastic
How to integrate ArcSight with Elastic

This document demonstrates how to integrate ArcSight with Elastic using Apache Syslog Smartconnector. 
We'll be monitoring Apache Logs using Apache Syslog connector. 3 steps -> 

1). Things to be done on Apache Server side:

Edit the file /etc/httpd/conf/httpd.conf and add the entries:
  ErrorLog "| /usr/bin/logger -t 'apache_error_log' " 
  CustomLog "| /usr/bin/logger -t 'apache_access_log' " combined
  
This will send all access and error logs to syslog on the localhost. If you are forwarding events to a remote log host, the /etc/syslog.conf file should be modified.
Restart syslog and httpd after making those changes. 




