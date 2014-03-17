Title: Suggested JVM args

The default JVM configuration will most likely not be appropriate for running Isis as a webapp.  Some args that you will 

<table class="table table-striped table-bordered table-condensed">
<tr>
    <th>Flag</th>
    <th>Description</th>
</tr>
<tr>
    <td>-server</td>
    <td>Run the JVM in server mode, meaning that the JVM should spend more time on the optimization of the fragments of codes that are most often used (hotspots). This leads to better performance at the price of a higher overhead at startup</td>
</tr>
<tr>
    <td>-Xms128m</td>
    <td></td>
</tr>
<tr>
    <td>-Xmx768m</td>
    <td></td>
</tr>
<tr>
    <td>-XX:PermSize=64m</td>
    <td></td>
</tr>
<tr>
    <td>-XX:MaxPermSize=256m</td>
    <td></td>
</tr>
<tr>
    <td>-XX:+DisableExplicitGC</td>
    <td>Causes any explicit calls to <tt>System.gc()</tt> to be ignored.  See <a href="http://stackoverflow.com/questions/12847151/setting-xxdisableexplicitgc-in-production-what-could-go-wrong">this stackoverflow</a> question.</td>
</tr>
</table>
   
There are also a whole bunch of GC-related flags, that you might want to explore; see this detailed [Hotspot JVM](http://www.oracle.com/technetwork/java/javase/tech/vmoptions-jsp-140102.html) documentation and also this [blog post](http://blog.ragozin.info/2011/09/hotspot-jvm-garbage-collection-options.html).

   
## Configuring in Tomcat

If using Tomcat, update the `CATALINA_OPTS` variable.

> This variable is also updated if [configuring logging to run externally](./externalized-configuration.html#log4j).
