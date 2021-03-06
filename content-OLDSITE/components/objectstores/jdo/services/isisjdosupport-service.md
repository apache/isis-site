Title: Using the IsisJdoSupport service

[//]: # (content copied to user-guide_reference_domain-services_isis-jdo-support)

The `IsisJdoSupport` service  provides a number of general purpose methods for working with DataNucleus.

## Executing arbitrary SQL

The `executeSql(...)` method allows arbitrary queries to be submitted:

    List<Map<String, Object>> executeSql(String sql);

while `executeUpdate(...)` allows arbitrary updates to be performed. 

    Integer executeUpdate(String sql);

A common use of these is to setup fixture data for integration tests.

## Fixture support

The `deleteAll(...)` method is provided pretty much exclusively for tearing down fixture data: 

    void deleteAll(Class<?>... pcClasses);



## Reloading entities

A [known limitation](http://www.datanucleus.org/products/datanucleus/jdo/orm/relationships.html) of DataNucleus' implementation of JDO is that persisting a child entity (in a 1:n bidirectional relationship) does not cause the parent's collection to be updated.

The `refresh(T domainObject)` method can be used to reload the parent object (or indeed any object).

For example:

    public Order newOrder(final Customer customer) {
        Order order = newTransientInstance(Order.class);
        order.setCustomer(customer);
        persist(customer);
        getContainer().flush(); // to database
        isisJdoSupport.refresh(customer); // reload parent from database
        return order;
    }


## Accessing the JDO `PersistenceManager`

Apache Isis provides a simplified API on top of only supports JDO, and so does not support all of JDO's features.  For example, Isis (currently) only supports named queries.  If you require more flexibility than this, eg for dynamically constructed queries, then the service provides access to the underlying JDO `PersistenceManager` API.


For example:

    public List<Order> findOrders(...) {
        javax.jdo.PersistenceManager pm = isisJdoSupport.getPersistenceManager();
        
        // knock yourself out...
        
        return someListOfOrders;
    }

    
## Registering the Service

The implementation is `IsisJdoSupportImpl`.  It is registered in `isis.properties` as per usual:

    isis.services = ...\
                org.apache.isis.objectstore.jdo.datanucleus.service.support.IsisJdoSupportImpl,\
                    ...

In the domain entity or service, add:

    private IsisJdoSupport isisJdoSupport;
    public void injectIsisJdoSupport(IsisJdoSupport isisJdoSupport) {
        this.isisJdoSupport = isisJdoSupport;
    }

or simply:

    @javax.inject.Inject
    private IsisJdoSupport isisJdoSupport;

The service will then be automatically injected as normal.
                    