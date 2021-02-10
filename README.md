# F5 Splunk Telemtry Service Setup
The following outlines on how I setup splunk with F5 TS

Prerequistsi: 
- Install F5 TS RPM https://github.com/F5Networks/f5-telemetry-streaming/releases onto your F5
- Install AS3 https://github.com/F5Networks/f5-appsvcs-extension/releases 

Two files here... 
1. ts.json  = Splunk Telemery configuration file
2. as3logging = AS3 declarative configuration to configure the logging profiles


## Edit the ts.json 
Edit the following file to match what you have setup in your lab
- cipherText
- host IP
Note: I Turned off allowselfsignedcert = true because this is for my lab envrionment

## How to post the .json to your F5
- ts.json = POST to the URI https://<BIG-IP>/mgmt/shared/telemetry/declare
- aslogging-all.json = To send a declaration with using cURL, use curl -sku admin:admin -H "Content-Type: application/json" -X POST https://localhost:443/mgmt/shared/appsvcs/declare and then include the declaration.

Or use Postman or Visual Studio Code

Also..for System Logging [If you haven't done this in you DO.JSON ]
Modify the system syslog configuration by adding a destination, using the following TMSH command:

```
modify sys syslog remote-servers replace-all-with { server { host 127.0.0.1 remote-port 6514 } }
```

Modify system logging configuration to update what gets logged:
```
modify sys daemon-log-settings mcpd audit enabled
```
