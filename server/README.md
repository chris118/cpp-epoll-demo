# add submodule
```
git submodule add https://gitee.com/chris118/glog.git 3rdparty/glog
git submodule add https://gitee.com/chris118/handy.git 3rdparty/handy
```

# use submodule
```
git submodule init && git submodule update
git submodule update --init --recursive
```

# shutdown glog test
```
# Unit testing

set(BUILD_TESTING OFF)
```