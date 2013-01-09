Bug Branch Creation
-------------------

```
git checkout dev-3.x
git pull upstream dev-3.x
git checkout -b foo-123456
```

do code stuff (should always be pushing to origin)

_If you have travis connected, this will show you build failures_

* do tests 
* do builds
* do commits as you go on all files but builds

Everyday
--------

```
git checkout dev-3.x
git pull upstream dev-3.x
git checkout foo-123456
git merge dev-3.x
```

(Fix any merge issues to make sure I'm clean)

When you are ready for a Pull Request
-------------------------------------

```
git merge dev-3.x
git push origin foo-123456
```

issue pr through github's ui agains dev-3.x
-------------------------------------------

when the pr is approved

```
git checkout dev-3.x
git pull upstream dev-3.x
git merge foo-123456
```

build and add commit build files

push up to dev-3.x

`git push upstream dev-3.x`