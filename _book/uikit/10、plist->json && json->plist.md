### 有时候需要ios端将一些资源处理好后给Android端人员使用。今天就遇到这样一个需求。通过简单的命令行就可以实现。

plist-&gt;json

```
cd /Users/geek/工作区/yhyy-doctor/heletalk-doctor/Class/MainViewController/HLPDFReader


plutil -convert json HLPDFCatagory.plist -o HLPDFCatagory.json
```

json-&gt;plist

```
plutil -convert xml1 HLPDFCatagory.json -o HLPDFCatagory.plist
```



