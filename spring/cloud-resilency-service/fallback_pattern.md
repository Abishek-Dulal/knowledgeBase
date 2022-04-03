
## Fallback pattern

```java

    @CircuitBreaker(name="licenseService",
            fallbackMethod = "buildFallbackLicesenList"
    )
    public List<License> getLicenseByOrganisation(String organisationId){
        return licenseRepository.findByOrganisationId(organisationId);
    }


    public List<License> buildFallbackLicesenList(String organistionId){
        List<License> fallbackList = new ArrayList<>();
        License license = new License();
        license.setLicenseId("0000000-00-00000");
        license.setOrganisationId(organistionId);
        license.setProductName(
                "Sorry no licensing information currently available");
        fallbackList.add(license);
        return fallbackList;
    }



```


#spring  #spring_resilency 