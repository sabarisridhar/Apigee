## Proxy: getLocation

### Description 
This proxy is demonstrate on how to fetch a response from a target using service callout policy and combine that response with the response fetched from the backend target server.

### Policies Used:  
[FC-callFetchLocation](#FC-callFetchLocation)  
[RC-response](#RC-response)
[AM-SetResponse](#AM-SetResponse)  



#### FC-callFetchLocation 
1) This FlowCallout policy calls the shared flow "fetchLocation"  
  

#### RC-response
1) The response cache policy is configured to execute based on the query parameter "user".   
2) If the policy creates a cache of response with reference to the "user" value passed.  
3) If the same "user" value is passed on the subsequent request, the reponse will be fetched from the cache till the cache is expried.


#### AM-setResponse  
1) This AssignMessage policy combines the variable "country" returned by the service callout with the backend response and returns the response in JSON format.   
