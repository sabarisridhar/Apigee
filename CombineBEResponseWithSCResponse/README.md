## Proxy: getLocation

### Description 
This proxy is demonstrate on how to fetch a response from a target using service callout policy and combine that response with the response fetched from the backend target server.

### Policies Used:  
[AM-remove-ifNoneMatch](#AM-remove-ifNoneMatch:)   
[FC-callFetchLocation](#FC-callFetchLocation:)  
[AM-SetResponse](#AM-SetResponse:)  

## Shared flow: fetchLocation

### Description
This shared flow calls an external target service and returns a part of that response.


### Policies used:
[SC-getLocation](#SC-getLocation:)    
[EV-fetchLocation](#EV-fetchLocation:)  



#### AM-remove-ifNoneMatch:  
This AssignMessage policy removes the header "ifNoneMatch" to make sure that   
-> the browser does not return cached response to the client and   
-> the request reaches the target 
 
#### FC-callFetchLocation: 
This FlowCallout policy calls the shared flow "fetchLocation"  

#### SC-getLocation: 
This ServiceCallout policy is used to call an external target which returns the client's geographical data in JSON format using the client IP as input.   
The target URL refers to "proxy.client.ip" flow variable to get the client IP.  

#### EV-fetchLocation:  
This ExtractVariable policy is used to get a particular field ("country name" in this case) from the callout response and sets the value to the variable "locationResponse.country".


#### AM-setResponse:  
This AssignMessage policy combines the variable "country" returned by the service callout with the backend response and returns the response in JSON format.   
