Title: Event Bus Service for JDO

To use the [EventBusService](../../../../reference/services/event-bus-service.html) with the JDO Object Store, the JDO-specific implementation should be registered.

The JDO implementation does not provide any additional functionality, but is aware of the lifecycle of domain entities and so ensures that objects are not interacted with while they are being rehydrated by the object store.


## Register the Service

Register this service like any other service, in `isis.properties`:

    isis.services=...,\
                  org.apache.isis.objectstore.jdo.datanucleus.service.eventbus.EventBusServiceJdo,\
                  ...
