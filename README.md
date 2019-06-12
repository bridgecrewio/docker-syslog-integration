# docker-syslog-integration
The integration is collect the data from Fortigate and send it to Bridgecrew

## Fortigate

### Fortigate syslog configuration
```
config log syslogd setting
  set status enable
  set server [IP of the server with the docker]
  set reliable UDP
  set port 9910
  set csv enable
  set facility local7
end
```

### Docker server
###### Port verify
The port 9910 (UDP) must be open outside.   
verify that firewall is configure to allow this port
###### Docker verification
```
docker info
```

###### syslog-integration install
```
docker run -d -p 9910:9910/udp -e BC_CUSTOMER_NAME=[REPLACE_WITH_CUSTOMER_NAME] -e BC_API_TOKEN=[REPLACE_WITH_API_TOKEN] -e BC_URL="https://www.bridgecrew.cloud/api/v1/integrations/logstash" bridgecrew/syslog-integration
```