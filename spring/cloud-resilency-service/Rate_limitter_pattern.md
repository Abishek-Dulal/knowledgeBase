
## Rate Limiter pattern
 Resilence4j provides two types of pattern:-
 1) AtomicRateLimiter
 2) SemaphoreRateLimiter

### Semphore Rate Limiter
The SemaphoreBasedRateLimiter is the simplest. This implementation is based on
having one java.util.concurrent.Semaphore store the current permissions. In this scenario, 
all the user threads will call the method semaphore.tryAcquire to trigger a call to an additional internal thread by executing semaphore.release when a new limitRefreshPeriod starts.

### Atomic RateLimiter
The AtomicRateLimiter splits all nanoseconds from the start into cycles, and each
cycle duration is the refresh period (in nanoseconds). Then at the beginning of each
cycle, we should set the active permissions to limit the period. To better understand
this approach, let’s look at the following settings:
1) ActiveCycle —The cycle number used by the last call
2) ActivePermissions —The count of available permissions after the last call
3) NanosToWait —The count of nanoseconds to wait for permission for the last call

This implementation contains some tricky logic. To better understand it, we can con-
sider the following Resilience4j statements for this pattern:
1) Cycles are equal time pieces.
2) If the available permissions are not enough, we can perform a permission reservation by decreasing the current permissions and calculating the time we need to wait for the permission to appear. Resilience4j allows this by defining the number of calls that are allowed during a time period ( limitForPeriod ); how often permissions are refreshed ( limitRefreshPeriod ); and how long a threadcan wait to acquire permissions ( timeoutDuration ).

![[rate_limit.png]]

``` yml

resilience4j:
  ratelimiter:
    instances:
      licenseserver:
        limitForPeriod: 5
        timeoutDuration: 1000ms
        limitRefreshPeriod: 5000

```

```java

    @RateLimiter(name = "licenseService",
            fallbackMethod = "buildFallbackLicenseList")
    public List<License> getLicenseByOrganisation(String organisationId){
        return licenseRepository.findByOrganisationId(organisationId);
    }

```
