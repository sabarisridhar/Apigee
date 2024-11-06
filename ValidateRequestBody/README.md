## Proxy: ValidateRequestBody  

### Description:   
This proxy illustrates the of OASValidation Policy.

### Policies Used:  
[JTP-userData](#JTP-userData)  
[OAS-validateUserBody](#OAS-validateUserBody)  
[RF-JTP](#RF-JTP) 
[RF-requestBodyRequired](#RF-requestBodyRequired)  
[AM-returnResponse](#AM-returnResponse)   


 
### JTP-userData  
The JSONThreatProtection policy prevents user from adding addition fields in the request payload.

### OAS-validateUserBody  
The OASValidation policy validates the request payload against the swagger file (which consists the specification of the request body).

### RF-JTP  
This RaiseFault policy is configured to return custom error message in XML format when the "JTP-userData" policy fails.

### RF-requestBodyRequired  
This RaiseFault policy is configured to return custom error message in JSON format when the "OAS-validateUserBody" policy fails.

### AM-returnResponse   
The AssignMessage policy is configured to copy and return the request payload. 

