## Shared flow: fetchLocation

### Description
This shared flow calls an external target service and returns a part of that response.


### Policies used:
[LC-checkLocation](#LC-checkLocation)
[SC-getLocation](#SC-getLocation)    
[EV-fetchLocation](#EV-fetchLocation)  
[PC-addCountry](#PC-addcountry)

  
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
