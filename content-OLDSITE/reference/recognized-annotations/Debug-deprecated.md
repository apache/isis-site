Title: @Debug

[//]: # (content copied to _user-guide_xxx)

> Deprecated, use instead [@Action#restrictTo()](./Action.html).

The `@Debug` annotation marks an action method as available in debug mode
only, and so will not normally be displayed by the user interface.

For example:

    public class Customer {
        public Order placeNewOrder() { ... }
        @Debug
        public List<Order> listRecentOrders() { ... }
        ...
    }

The exact means to access `@Debug` actions depends on the viewer.
