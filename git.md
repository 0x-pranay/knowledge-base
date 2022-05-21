# GIT



### stash



#### How to access dropped stash. [Solution](https://stackoverflow.com/a/91795)

Once you know the hash of the stash commit you dropped, you can apply it as a stash:

```
git stash apply $stash_hash
```

Or, you can create a separate branch for it with

```
git branch recovered $stash_hash
```



### Compare two braches

[Ref: devconnected](https://devconnected.com/how-to-compare-two-git-branches/#:~:text=In%20order%20to%20compare%20two,branch%20names%20separated%20by%20dots.&text=Using%20this%20command%2C%20Git%20will,can%20use%20to%20see%20modifications.)



```
git diff master..feature
```

![Compare two branches using git diff](https://devconnected.com/wp-content/uploads/2019/11/git-diff-double-dot.png)

#### using triple dot syntax: 

 **compares the top of the right branch (the HEAD) with the common ancestor of the two branches**



![Compare two branches using triple dot syntax](https://devconnected.com/wp-content/uploads/2019/11/triple-dot.png)

```
git diff branch1...branch2
```





#### How to access a lost commit 

Use reflog

