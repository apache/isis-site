Title: Joda Dates

[//]: # (content copied to _user-guide_how-tos_class-structure_properties)

Isis' JDO objectstore bundles DataNucleus' [built-in support](http://www.datanucleus.org/documentation/products/plugins.html) for Joda `LocalDate` and `LocalDateTime` datatypes, meaning that entity properties of these types will be persisted as appropriate data types in the database tables.

It is, however, necessary to annotate your properties with `@javax.jdo.annotations.Persistent`, otherwise the data won't actually be persisted.  (See the [JDO docs](http://db.apache.org/jdo/field_types.html) for more details on this).

Moreover, these datatypes are *not* in the default fetch group, meaning that JDO/DataNucleus will perform an additional `SELECT` query for each attribute.  To avoid this extra query, the annotation should indicate that the property is in the default fetch group.

For example, the `ToDoItem` (in the [todoapp example app](https://github.com/isisaddons/isis-app-todoapp) (not ASF)) defines the `dueBy` property as follows:

<pre>
    @javax.jdo.annotations.Persistent(defaultFetchGroup="true")
    private LocalDate dueBy;

    @javax.jdo.annotations.Column(allowsNull="true")
    public LocalDate getDueBy() {
        return dueBy;
    }
</pre>


