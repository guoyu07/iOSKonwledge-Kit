### wgs84，gcj-02,bd-09是什么?

wgs84是国际标准，从GPS设备中取出的原始数据就是这个标准的数据，iOS的SDK中用到的坐标系统也是国际标准的坐标系统WGS-84；

gcj-02是中国标准，行货GPS设备取出的原始数据是该标准的数据，根据规定，国内出版的各种地图系统，必须至少采用gcj-02对地理位置进行首次加密。网络上也称之为火星坐标。

bd-09是百度标准，百度SDK使用的就是这个标准。

如何转换？  
[转换方法](https://github.com/JackZhouCn/JZLocationConverter)

