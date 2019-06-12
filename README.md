# docker-syslog-integration
The integration is collecting data from Fortigate and sending it to Bridgecrew.

## Fortigate

The installation includes 2 steps,   
1. Fortigate syslog configuration   
2. Install the syslog integration docker 

### 1. Fortigate syslog configuration
connect to fortigate console and run the following command:
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

### 2. Install the syslog integration docker 
###### Port verify
The port 9910 (UDP) must be open outside.   
verify that firewall is configure to allow this port

#### Installation

1. Open ssh to server
2. Install docker
3. Verify docker by running the following command: ``` docker info ```
4. Run syslog-integration:
```
docker run -d -p 9910:9910/udp -e BC_CUSTOMER_NAME=[REPLACE_WITH_CUSTOMER_NAME] -e BC_API_TOKEN=[REPLACE_WITH_API_TOKEN] -e BC_URL="https://www.bridgecrew.cloud/api/v1/integrations/logstash" bridgecrew/syslog-integration
```