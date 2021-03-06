title: Tweaking the UI using CSS classes

[//]: # (content copied to _user-guide_wicket-viewer_customisation)

The Wicket viewer allows you to customize the GUI in several (progressively more sophisticated) ways:

* through CSS (described below)
* through Javascript snippets (eg JQuery) (see [here](./how-to-tweak-the-ui-using-javascript.html))
* by replacing elements of the page using the `ComponentFactory` interface (see [here](./customizing-the-viewer.html))
* by providing new pages (see [here](./custom-pages.html))

The most straight-forward way to customize the Wicket viewer's UI is to use CSS, and is described here.

## Customizing the CSS

The HTML generated by the Wicket viewer include plenty of CSS classes so that you can easily target the required elements as required.  For example, you could use CSS to suppress the entity's icon alongside its title.  This would be done using:

    .entityIconAndTitlePanel a img {
    	display: none;
    }

These customizations should generally be added to `src/main/webapp/css/application.css`; this file is included by default in every webpage served up by the Wicket viewer.

## Targetting individual members

For example, the `ToDoItem` object of the Isis addons example [todoapp](https://github.com/isisaddons/isis-app-todoapp/) (not ASF) has a `notes` property.  The HTML for this will be something like:

    <div>
        <div class="property ToDoItem-notes">
            <div class="multiLineStringPanel scalarNameAndValueComponentType">
                <label for="id83" title="">
                    <span class="scalarName">Notes</span>
                    <span class="scalarValue">
                        <textarea
                            name="middleColumn:memberGroup:1:properties:4:property:scalarIfRegular:scalarValue" 
                            disabled="disabled" 
                            id="id83" rows="5" maxlength="400" size="125" 
                            title="">
                        </textarea>
                        <span>
                        </span>
                    </span>
                </label>
           </div>
        </div>
    </div>
    

The `src/main/webapp/css/application.css` file is the place to add application-specific styles.  By way of an example, if (for some reason) we wanted to completely hide the notes value, we could do so using:

    div.ToDoItem-notes span.scalarValue {
        display: none;
    }

You can use a similar approach for collections and actions.


### Targetting members through a custom CSS style

The above technique works well if you know the class member to target, but you might instead want to apply a custom style to a set of members.  For this, you can use the `@CssClass`.

For example, in the `ToDoItem` class the following annotation (indicating that this is a key, important, property) :

    @CssClass("x-key")
    public LocalDate getDueBy() {
        return dueBy;
    }

would generate the HTML:

    <div>
        <div class="property ToDoItem-dueBy x-key">
            ...
        </div>
    </div>

This can then be targeted, for example using:

    div.x-key span.scalarName {
    	color: red;
    }


Note also that instead of using `@CssClass` annotation, you can also specify the CSS style using a [dynamic layout](./dynamic-layouts.html) JSON file:

    ...
    "dueBy": {
        "propertyLayout": {
            "cssClass": "x-key"
        }
    },
    ...


### Application-specific 'theme' class

The application name (as defined in the `IsisWicketApplication` subclass) is also used (in sanitized form) as the CSS class in a `<div>` that wraps all the rendered content of every page.

For example, if the application name is "ToDo App", then the `<div>` generated is:

    <div class="todo-app">
        ...
    </div>

You can therefore use this CSS class as a way of building your own theme for the various elements of the wicket viewer pages.

## Using a different CSS file

If for some reason you wanted to name the CSS file differently (eg `stylesheets/myapp.css`), then adjust the Guice bindings (part of Isis' bootstrapping) in your custom subclass of `IsisWicketApplication`:

    public class MyAppApplication extends IsisWicketApplication {
        @Override
        protected Module newIsisWicketModule() {
            final Module isisDefaults = super.newIsisWicketModule();
            final Module myAppOverrides = new AbstractModule() {
                @Override
                protected void configure() {
                    ...
                    bind(String.class)
                        .annotatedWith(Names.named("applicationCss"))
                        .toInstance("stylesheets/myapp.css");
                    ...
                }
            };
    
            return Modules.override(isisDefaults).with(myAppOverrides);
        }
    }

As indicated above, this file is resolved relative to `src/main/webapp`.

