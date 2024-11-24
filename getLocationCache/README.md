## Overview:-
This proxy demostrate the functions of cache policies.

## Proxy: getLocation

### Description 
This proxy is demonstrate on how to fetch a response from a target using service callout policy and combine that response with the response fetched from the backend target server.

### Policies Used:  
[FC-callFetchLocation](#FC-callFetchLocation)  
[RC-response](#RC-response)
[AM-SetResponse](#AM-SetResponse)  

## Shared flow: fetchLocation

### Description
This shared flow calls an external target service and returns a part of that response.


### Policies used:
[LC-checkLocation](#LC-checkLocation)
[SC-getLocation](#SC-getLocation)    
[EV-fetchLocation](#EV-fetchLocation)  
[PC-addCountry](#PC-addcountry)

#### FC-callFetchLocation 
1) This FlowCallout policy calls the shared flow "fetchLocation"  
  
#### LC-checkLocation
1) The LookupCache policy checks a response has been cached for the "proxy.client.ip"    
2) The policy has been configured such that:-
- If the policy finds the cached response, it assigns the cached value to the "locationResponse.country" variable and skips the rest of the policies in the shared flow.  
- If the policy does not find the cached response it proceeds to the service callout policy [SC-getLocation](#SC-getLocation) 

#### SC-getLocation 
1) This ServiceCallout policy is used to call an external target which returns the client's geographical data in JSON format using the client IP as input.   
2) The target URL refers to "proxy.client.ip" flow variable to get the client IP.  
  
  
#### EV-fetchLocation  
1) This ExtractVariable policy is used to get a particular field ("country name" in this case) from the callout response and sets the value to the variable "locationResponse.country".

#### PC-addCountry
1) The PoplateCache policy is configured to create a cache containing the value of "locationResponse.country" variable. 
2) The cache is stored with reference to the "proxy.client.ip" value.


#### RC-response
1) The response cache policy is configured to execute based on the query parameter "user".   
2) If the policy creates a cache of response with reference to the "user" value passed.  
3) If the same "user" value is passed on the subsequent request, the reponse will be fetched from the cache till the cache is expried.


#### AM-setResponse  
1) This AssignMessage policy combines the variable "country" returned by the service callout with the backend response and returns the response in JSON format.   
