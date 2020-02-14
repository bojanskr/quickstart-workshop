+++
title = "Update your fork"
chapter = false
weight = 60
+++


Keeping your local branch in sync with the upstream is a good practice. In the case of quickstarts we use the develop branch to run ci tests and aggregate changes for release. So it a good idea to keep track of the commit to upstream/develop so you work in progress is easily intregrated.

### Updating your fork

Fetch branches from remote.

`git fetch --all`

<pre>
    Fetching origin
    Fetching upstream
    .... (updates) ....
</pre>

Reset the HEAD of you fork so that it is even with your upstream branch.

`git reset --hard upstream/develop`

    HEAD is now at a29330a  Commit message of the last commit in upstream/develop

Force push your local changes to your origin. This will make upstream/develop and origin/develop even.

`git push --force-with-lease origin develop`

    Everything up-to-date
    or
    Shows pushed changes

{{% notice warning %}}
Be carefull all the changes in your forks develop branch will be lost. If you have any work in this branch stash it elsewhere!
{{% /notice %}}

