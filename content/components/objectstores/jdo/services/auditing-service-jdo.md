Title: Auditing Service using JDO

The JDO objectstore provides a simple implementation of the applib [AuditingService](../../../../reference/services/auditing-service.html) that simply persists the event data into a `AuditEntry` entity.

> Rather than using an `AuditingService`, you may prefer to use the [Publishing Service](../../../../reference/services/publishing-service.html), since it is considerably more flexible.  A JDO [implementation](./publishing-service-jdo.html) is available.

### Register the Service

Register like any other service in `isis.properties`:

    isis.services=...,\
                  org.apache.isis.objectstore.jdo.applib.service.audit.AuditingServiceJdo,\
                  ...

Assuming that you've also configured Isis to use the JDO objectstore, you should be good to go...