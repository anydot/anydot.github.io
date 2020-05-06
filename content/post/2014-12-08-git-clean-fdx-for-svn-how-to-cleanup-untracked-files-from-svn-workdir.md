+++
date = "2014-12-08T18:10:00+01:00"
title = "git clean -fdx for SVN -- how to cleanup untracked files from SVN workdir"

+++

```bash
# Cleanup files untracked by SVN
svn status --xml --no-ignore  | xmlstarlet sel -t -v '/status/target/entry[wc-status[@item="unversioned" or @item="ignored"]][@path!=".git"]/@path' | xargs rm -fr
```
