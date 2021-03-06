Title: Release Branch and Tag Names

[//]: # (content copied to _user-guide_xxx)

As described in the [release process](release-process.html) documentation, each release of core or a component is prepared in a separate branch, and ultimately results in a tag in the central repo.

In Isis the version numbers of core and each component can vary independently 
(they are not synchronized); therefore the branches and the tag names must 
distinguish the releasable module that they refer to.

The table below shows the tag name to use when running the `release:prepare` command itself, as well as the local branch name to use while preparing the release:

* We've chosen to base the tag name on the `artifactId` of the pom of the parent module being released, as this also happens to be the default provided by the `maven-release-plugin`.  

* The branch name to use is not actually that important, because it would not usually be pushed to the origin (unless you were preparing the release with some other committer).  However, we recommend that is similar (though not identical to) the tag name. 

<table>
<tr>
<th>Releasable module</th>
    <th>Branch name to use while <br/>readying the release locally</th>
    <th>Tag name for <tt>release:prepare</tt></th>
    <th>Tag name manually pushed.</th>
</tr>
<tr>
    <td>core</td>
    <td>prepare/isis-x.y.z</td>
    <td>isis-x.y.z</td>
    <td>isis-x.y.z-RCn</td>
</tr>
<tr>
    <td>viewer/xxx</td>
    <td>prepare/isis-x.y.z<br/>(reuse same branch as core)</td>
    <td>isis-viewer-xxx-x.y.z</td>
    <td>isis-viewer-xxx-x.y.z-RCn</td>
</tr>
<tr>
    <td>example/archetype/<br/>&nbsp;&nbsp;xxxxapp</td>
    <td>prepare/isis-x.y.z<br/>(reuse same branch as core)</td>
    <td>xxxapp-archetype-x.y.z</td>
    <td>xxxapp-archetype-x.y.z-RCn</td>
</tr>
</table>

where `xxx` represents a specific component or archetype being released.

{note
In fact, git allows the same name to be used for both branches and for tags; within git they are namespaced to be unique.  However, using the same name for the branch confuses `maven-release-plugin`; thus the branch name is slightly different from the tag name.
}

