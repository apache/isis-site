Title: Eagerly Registering Entity Types

[//]: # (content copied to _user-guide_runtime_configuring-datanucleus_eagerly-registering-entities)

*in 1.6.0 and 1.7.0, this feature may be (partly?) broken; see [ISIS-847](https://issues.apache.org/jira/browse/ISIS-847)*

Both Apache Isis and DataNucleus have their own metamodels of the domain entities.  Isis builds its metamodel by walking the graph of types from the services registered using
`@DomainService` or explicitly registered in `isis.properties`.  The JDO objectstore then takes these types and registers them with DataNucleus.

In some cases, though, not every entity type is discoverable from the API of the service actions.  This is especially the case if you have lots of subtypes (where the action method specifies only the supertype).  In such cases the Isis and JDO metamodels is built lazily, when an instance of that (sub)type is first encountered.

Isis is quite happy for the metamodel to be lazily created, and - to be fair - DataNucleus also works well in most cases.  In some cases, though, we have found that the JDBC driver (eg HSQLDB) will deadlock if DataNucleus tries to submit some DDL (for a lazily discovered type) intermingled with DML (for updating).

In any case, it's probably not good practice to have DataNucleus work this way.  The `RegisterEntities` service can therefore be registered in order to do the eager registration.  It searches for all `@PersistenceCapable` entities under specified package(s), and registers them all.

> in 1.3.x, it is not mandatory to eagerly register entity types; however we strongly recommend it.
> in 1.4.0 and later, it *is* mandatory to eager register entity types.

### Specify the Package Prefix(es)

In the `persistor_datanucleus.properties`, specify the package prefix(es) of your application, to provide a hint for finding the `@PersistenceCapable` classes.  

<pre>
isis.persistor.datanucleus.RegisterEntities.packagePrefix=com.mycompany.dom
</pre>

The value of this property can be a comma-separated list (if there is more than one package or Maven module that holds persistable entities).


### Register the Service (1.3.x only)

> In 1.4.0 and later this step is no longer required.

(If using 1.3.x), register like any other service in `isis.properties`:

<pre>
isis.services=<i>...other services...</i>,\
              org.apache.isis.objectstore.jdo.service.RegisterEntities,\
              ...
</pre>
