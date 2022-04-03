

## Retry pattern
![[retry_yml.png]]

```yml

resilience4j:
   retry:
    instances:
      retryLicensesService:
        maxRetryAttempts: 5
        waitDuration: 10000
        retryExceptions:
          - java.util.concurrent.TimeoutException




```

```java
@Retry(name = "retryLicenseService", fallbackMethod=  
                "buildFallbackLicenseList")  
public List<License> getLicenseByOrganisation(String organisationId){  
    return licenseRepository.findByOrganisationId(organisationId);  
}
```



#spring  #spring_resilency 