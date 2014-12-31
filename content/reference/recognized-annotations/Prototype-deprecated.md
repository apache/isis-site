Title: @Prototype

> Deprecated in 1.8.0-SNAPSHOT, see instead [@ActionLayout](./ActionLayout.html)

The `@Prototype` annotation marks an action method as available in
prototype mode only, and therefore not intended for use in the
production system.

For example:

    public class Customer {
        public Order placeNewOrder() { ... }
        @Prototype
        public List<Order> listRecentOrders() { ... }
        ...
    }

    
#### See also

See also the [@Exploration](./exploration.html) annotation.
