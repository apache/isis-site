Title: Deployment Types and Component Defaults

One important configuration setting is the `deploymentType`, which, in turn, specifies the `deploymentCategory`.  If a component implementation is not specified explicitly, then the default is based on the deployment category (see the [InstallerLookupDefault](https://raw.github.com/apache/isis/master/core/runtime/src/main/java/org/apache/isis/core/runtime/installers/InstallerLookupDefault.java) class). Certain other features are based on the category also.

<table>
<tr>
<th>Deployment category</th>
<th>Deployment types</th>
<th>Authentication<br/>(if not specified)</th>
<th>Authorization<br/>(if not specified)</th>
<th>Object store<br/>(if not specified)</th>
<th>Profile store<br/>(if not specified)</th>
<th>@Exploration actions</th>
<th>@Prototype actions</th>
</tr>
<tr>
    <td>EXPLORING</td>
    <td>SERVER_EXPLORATION<br/>
EXPLORATION<br/>
UTILITY</td>
    <td><a href="bypass-security.html">Bypass</a></td>
    <td><a href="bypass-security.html">Bypass</a></td>
    <td><a href="inmemory-objectstore.html">In-memory</a></td>
    <td><a href="inmemory-profilestore.html">In-memory</a></td>
    <td>Visible</td>
    <td>Not visible</td>
    </tr>
<tr>
    <td>PROTOTYPING</td>
    <td>SERVER_PROTOTYPE<br/>
PROTOTYPE</td>
    <td><a href="../components/security/file/about.html">File-based</a></td>
    <td><a href="bypass-security.html">Bypass</a></td>
    <td><a href="inmemory-objectstore.html">In-memory</a></td>
    <td><a href="inmemory-profilestore.html">In-memory</a></td>
    <td>Not visible</td>
    <td>Visible</td>
</tr>
<tr>
    <td>PRODUCTION</td>
    <td>SERVER<br/>
UNIT_TESTING<br/>
SINGLE_USER</td>
    <td><a href="../components/security/file/about.html">File-based</a></td>
    <td><a href="../components/security/file/about.html">File-based</a></td>
    <td><a href="../components/objectstores/xml/about.html">XML</a></td>
    <td><a href="../components/profilestores/xml/about.html">XML</a></td>
    <td>Not visible</td>
    <td>Not visible</td>
</tr>
</table>

## Specifying the deploymentType explicitly

### Scimpi, HTML, Restful Objects

For the [scimpi](../components/viewers/scimpi/about.html) and [restfulobjects](../components/viewers/restfulobjects/about.html) viewers, the `deploymentType` is specified in the `<web.xml>` file:

<pre>
&lt;context-param&gt;
    &lt;param-name&gt;deploymentType&lt;/param-name&gt;
    &lt;param-value&gt;SERVER&lt;/param-value&gt;
&lt;/context-param&gt;
</pre>


If running these viewers using the [WebServer](https://raw.github.com/apache/isis/master/core/webserver/src/main/java/org/apache/isis/core/webserver/WebServer.java), then the `deploymentType` can be overridden at the command line:

    -t server_prototype

or using the long form:

    --type server_exploration

Only `server_*`-style `deploymentType`s should be specified (it has a bearing on the way that Isis does its session management).

The default if not specified is `SERVER`.

### Wicket

For the [wicket](../components/viewers/wicket/about.html) viewer, the Isis `deploymentType` is inferred from [Apache Wicket](http://wicket.apache.org)'s own [deployment mode](http://ci.apache.org/projects/wicket/apidocs/6.x/org/apache/wicket/Application.html#getConfigurationType()):

* Wicket's `DEVELOPMENT` mode corresponds to Isis' `PROTOTYPING` mode
* Wicket's `DEPLOYMENT` mode corresponds to Isis' `PRODUCTION` mode

The Wicket mode is set in the usual way for a Wicket application:

<pre>
&lt;init-param&gt;
    &lt;param-name&gt;configuration&lt;/param-name&gt;
    &lt;param-value&gt;deployment&lt;/param-value&gt;
&lt;/init-param&gt;
</pre>

### DnD

For the [dnd](../components/viewers/dnd/about.html) viewer, the `deploymentType` is specified at the command-line, for example:

    -t prototype

or using the long form:

    --type exploration

The default if not specified is `PROTOTYPE`.
