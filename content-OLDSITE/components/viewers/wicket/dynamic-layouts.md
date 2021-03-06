Title: Dynamic Layouts

[//]: # (content copied to _user-guide_wicket-viewer_layout_dynamic-object-layout)

Because Isis implements the [naked objects pattern](http://en.wikipedia.org/wiki/Naked_objects), the domain objects are rendered in the UI based only metadata gleaned from the domain classes themselves.  Traditionally this metadata has been specified [statically](./static-layouts.html), using annotations.  However, it is also possible to specify it using a JSON file.  This brings the advantage that the layout can be refreshed dynamically, without recompiling/redeploying the app.

## <a name="screencast"></a>Screencast

How to layout properties and collections dynamically, in the Wicket viewer.

<iframe width="530" height="354" src="http://www.youtube.com/embed/zmrg49WeEPc" frameborder="0" allowfullscreen></iframe>


## JSON layout file

The JSON layout file for class `Xxx` takes the name `Xxx.layout.json`, and resides in the same package as the class.
The format of the file is:

    {
      "columns": [                                // list of columns
        {
          "span": 6,                              // span of the left-hand property column
          "memberGroups": {                       // ordered map of member (property) groups
            "General": {                          // member group name
              "members": {
                "description": {                  // property, no associated actions, but with UI hint
                  "propertyLayout": {
                    "typicalLength": 50           // UI hint for size of field (no longer used in ISIS 1.8.0)
                  }
                },
                "category": {},
                "complete": {                     // property, with associated actions
                  "propertyLayout": {
                    "describedAs": "Whether this todo item has been completed"
                  },
                  "actions": {
                    "completed": {
                      "actionLayout": {
                        "named": "Done",          // naming UI hint
                        "cssClass": "x-highlight" // CSS UI hint
                      }
                    },
                    "notYetCompleted": {
                      "actionLayout": {
                        "named": "Not done"
                      }
                    }
                  }
                }
              },
              "Misc": {
                "members": {
                  "notes": {
                    "propertyLayout": {
                      "multiLine": 5              // UI hint for text area
                    }
                  },
                  "versionSequence": {}
                }
              }
            }
          }
        },
        {
          "span": 6,                              // span of the middle property column
          "memberGroups": { ... }
        },
        {
          "span": 0                               // span of the right property column (if any)
        },
        {
          "span": 6,
          "collections": {                        // ordered map of collections
            "dependencies": {                     // collection, with associated actions
              "collectionLayout": {
                "paged": 10,                      // pagination UI hint
                "render": "EAGERLY"               // lazy-loading UI hint
              },
              "actions": {
                "add":{},
                "delete": {}
              },
            },
            "similarItems": {}                    // collection, no associated actions
          }
        }
      ],
      "actions": {                                // actions not associated with any member
        "delete": {},
        "duplicate": {
          "actionLayout": {
            "named": {
              "value": "Clone"
            }
          }
        }
      }
    }
 
Although advisable, it is not necessary to list all class members in this file.  Any members not listed with be
ordered according either to annotations (if present) or fallback/default values.

Note also that the layout file may contain entries for
[contributed associations and actions](../../../more-advanced-topics/how-to-01-062-How-to-decouple-dependencies-using-contributions.html);
this allows each contributee classes to define their own layout for their contributions, possibly overriding any
static metadata on the original domain service contributor.

## Downloading an initial layout file

The fastest way to get started is to use the [Developer Utilities Service](../../../reference/services/developer-utilities-service.html) to download the layout file (derived from any existing static metadata defined by annotations).

## Picking up new metadata

When running in [prototype/development mode](../../../reference/deployment-type.html), the Wicket viewer automatically rebuilds the metamodel for each class as it is rendered.

> Conversely, do note that the Wicket viewer will *not* pick up new metadata if running in production/server mode.

## Required updates to the dom project's pom.xml

If using the `.layout.json` files, these must be compiled and available in the CLASSPATH.  When using an IDE such as Eclipse+M2E, any `.layout.json` files in `src/main/java` or `src/main/resources` will be part of the CLASSPATH automatically.  However, unless the `pom.xml` is changed, these will not be part of the compiled WAR.

Therefore, make sure the following is added to the dom project's `pom.xml`:

    <resources>
        <resource>
            <filtering>false</filtering>
            <directory>src/main/resources</directory>
        </resource>
        <resource>
            <filtering>false</filtering>
            <directory>src/main/java</directory>
            <includes>
                <include>**</include>
            </includes>
            <excludes>
                <exclude>**/*.java</exclude>
            </excludes>
        </resource>
    </resources>
 
If using an Isis [archetype](../../../intro/getting-started/simple-archetype.html), then the POM is already correctly configured.

## Static vs Dynamic Layouts

As mentioned above, it is also possible to [specify the layout semantics statically](./static-layouts.html) using annotations.  There's a <a href="static-layouts.html#pros-and-cons">discussion on that page</a> as to the pros and cons of static vs dynamic layouts.
