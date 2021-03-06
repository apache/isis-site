Title: Honor UI Hints 

[//]: # (content copied to _user-guide_restful-objects-viewer)

{note
These configuration settings should be considered beta, and are likely to change in the future in response to emerging requirements.
}

By default the representations generated by Restful Objects ignore any Isis metamodel hints referring to the UI.  
In particular, if a collection is annotated then `Render(EAGERLY)` then the contents of the collection are *not*
eagerly embedded in the object representation.

However, this behaviour can be overridden.

## Global Configuration

Configuring the Restful Objects viewer to honor UI hints globally is done using the
following property (typically added to `WEB-INF/viewer_restfulobjects.properties`):

    isis.viewer.restfulobjects.honorUiHints=true

## Per request

This is not currently supported (though may be in the future).
