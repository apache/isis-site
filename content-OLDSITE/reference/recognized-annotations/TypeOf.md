Title: @TypeOf

[//]: # (content copied to _user-guide_xxx)

> Deprecated, use instead [@Collection#typeOf](./Collection.html) or [@Action#typeOf](./Action.html).

The `@TypeOf` annotation is used to specify the type of elements in a
collection, when for whatever reason it is not possible to use generics.

> **Note**
>
> Given that Apache Isis only supports Java 1.6 and later, it's not that
> obvious what such a reason might be...

For example:

    public void AccountService {
        @TypeOf(Customer.class)
        public List errantAccounts() {
            return CustomerDatabase.allNewCustomers();
        }
        ...
    }
