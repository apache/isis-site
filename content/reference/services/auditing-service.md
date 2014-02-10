Title: Auditing Service

The auditing service provides a simple mechanism to capture changes to data.  It is called for each property that has changed on any domain object, as a set of pre- and post-values.

### API [1.4.0-SNAPSHOT]

The API for the service is:

    public interface AuditingService3 {
    
        @Programmatic
        public void audit(
                final UUID transactionId, String targetClassName, final Bookmark target, 
                String memberIdentifier, final String propertyName, 
                final String preValue, final String postValue, 
                final String user, final java.sql.Timestamp timestamp);
      }

> **BREAKING CHANGE!!!** The previous APIs for this service (`AuditingService` and `AuditingService2`) have been removed.  The new API is a superset of these previous APIs.  The change was made so that the auditing service would be consistent with the related [Publishing](./publishing-service.html) and the [Command Context](./command-context.html) services.

### API [1.3.0]

The API for the service is:

    public interface AuditingService2 {
    
        @Hidden
        public void audit(
           String user, long currentTimestampEpoch, 
           String objectType, String identifier, 
           String propertyId, 
           String preValue, String postValue);
      }

> Note that the original API for this service was called `AuditingService`.  This original API has been deprecated because it accidentally omitted the `propertyId` parameter.

### Implementations

A simple implementation of the service that writes to stderr, is available, useful for debugging:

* `org.apache.isis.applib.services.audit.AuditingService3$Stderr` [1.4.0-SNAPSHOT]
* `org.apache.isis.applib.services.audit.AuditingService2$Stderr` [1.3.0]

An alternative implementation, that persists audit records to a database, is the [JDO Publishing Service](../../components/objectstores/jdo/publishing-service-jdo.html).   This implementation is only supported when the the [JDO objectstore](../../components/objectstores/jdo/about.html) is configured.


### Register the Service

Register like any other service in `isis.properties`.  For example, if using the [JDO auditing implementation](../../components/objectstores/jdo/auditing-service.html) then it would be:

    isis.services=...,\
                  org.apache.isis.objectstore.jdo.applib.service.audit.AuditingServiceJdo,\
                  ...


### Related Services

A similar service that you may want to use alongside or instead of the auditing service is the [Publishing Service](publishing-service.html).