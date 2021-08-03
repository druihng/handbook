# gitbook





## submodule

```
git submodule add url
git submodule init
git submodule update
git submodule update --init
git submodule update --init --recursive

git clone --revurse-submodules url

```





```
$ git fetch
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From gitee.com:druihng/module_a
   5907165..9dbace3  master     -> origin/master

$ git merge origin/master
Updating 5907165..9dbace3
Fast-forward
 module_1 | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 module_1

$ git diff --submodule
Submodule module_a 5907165..9dbace3:
> add module_1
```

```
$ git submodule update --remote
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From gitee.com:druihng/module_a
   5907165..9dbace3  master     -> origin/master
Submodule path 'module_a': checked out '9dbace3519713713910832a48b3eaee93cc26566'

$ ls module_a/
module_1  module_a

```

