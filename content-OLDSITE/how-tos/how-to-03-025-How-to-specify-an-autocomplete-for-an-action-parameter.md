How to specify an auto-complete for an action parameter [1.3.0+]
-------------------------------------------------------

[//]: # (content copied to _user-guide_xxx)

Using the auto-complete method you can allow the user to search for objects based on a single string.  These will be made available to the user through a device such as a drop-down list.

The syntax is:

    public List<ParameterType> autoCompleteNActionName()

where N indicates the 0-based parameter number.

For example:

    public class Order {
        public Order placeOrder(
                Product product,
                @Named("Quantity") 
                int quantity) {
            ...
        }
        public List<Product> autoComplete0PlaceOrder(String search) {
            return productsRepo.findMatching(search);
        }
        ....
    }

> The [@AutoComplete](../reference/recognized-annotations/AutoComplete.html) also allows autocomplete functionality to be associated with the domain type (eg `Product` in the example above).  If both are present, then the per-parameter autocomplete takes preference.
