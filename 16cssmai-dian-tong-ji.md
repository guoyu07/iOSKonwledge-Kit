# CSS 埋点统计

> 当一个网站或者 App 的规模达到一定程度，需要分析用户在 App 或者网站的相应操作，则需要埋点统计用户行为，这个不用多说，具体实现有 JS 脚本写好埋点事件并调接口，今天 get 到一种新的埋点统计方式保证耳目一新。下面代码简单示范一下。

```
//index.html

<!DOCTYPE html>
<html>

    <head lang="en">
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width,initial-scale=1,minimum-scale=1,maximum-scale=1,user-scalable=no" />
        <title>CSS埋点</title>
        <style>
            .background {
                background-size: 100% 100%;
                width: 100%;
                height: 100%;
                position: fixed;
                z-index: -100;
            }

            html {
                background-color: #fff;
            }

            .notice-content {
                border: 1px #ccc solid;
                padding: 19px;
                border-radius: 10px;
                width: 80%;
                margin-left: 10%;
                margin-top: 10%;
            }

            .check-content {
                padding: 0!important;
                width: 80%!important;
                margin-left: 25px;
                margin-top: 10px;
            }

            .confirm {
                float: left;
                position: relative!important;
                left: 6%;
                height: 32px!important;
                line-height: 32px!important;
            }

            .btn {
                border: 1px solid #ff6689;
                background-color: #ff6689;
                width: 60%;
                margin-left: 20%;
                margin-top: 36px;
                font-size: 16px;
                font-weight: bold;
                color: #FFFFFF;
            }

            .title {
                display: block;
                text-align: center;
                font-size: 20px;
                margin-bottom: 19px;
            }

            span {
                display: block;
                margin-bottom: 7px;
            }

            .mui-checkbox input[type=checkbox]:checked:before,
            .mui-radio input[type=radio]:checked:before {
                color: #ff6689;
            }

            .body-content {
                width: 100%;
                height: 100%;
            }

            body {
                background-color: rgba(239, 239, 244, 0)!important;
            }

            .link:active::after{
                margin: 100px 100px;
                color: red;
                content: url("http://192.168.1.100:8888/Hotels_Server/view/count.php?action=visit");
            }
        </style>
    </head>

    <body>
        <div class="loading">
            </div>
        <div style="" class="body-content">
            <div class="background">
                <!-- <img id="background" src="img/background.png"> -->
            </div>

            <div class="notice-content">
                <label class="title">登记须知</label>
                <span>1.本次登记仅限于中国地区。</span>
                <span>2.完成登记审核通过后，生育登记服务卡可到乡（镇、街道）直接领取，也可选择邮寄到付快递给申请人。</span>
                <span>3.申请登记信息需真实完整，如有虚假，申请人将承担相应的法律责任。</span>
            </div>
            <a class="link title">访问</a>
        </div>
    </body>
</html>
```

```
//count.php
<?php
/**
 * Created by PhpStorm.
 * User: geek
 * Date: 2018/1/18
 * Time: 上午9:56
 */

    $actionName =  $_REQUEST["action"];

    //时间格式化
    $time = time();
    $time = Date("Y-m-d",$time);

    echo "访问动作->" .$actionName. " 访问时间->" . $time;
?>
```

![css点击统计](https://raw.githubusercontent.com/FantasticLBP/iOSKonwledge-Kit/master/assets/QQ20180118-095837%402x.png)

![php代码统计](https://raw.githubusercontent.com/FantasticLBP/iOSKonwledge-Kit/master/assets/屏幕快照%202018-01-18%20上午9.58.10.png)

**说明**

* 当然这种方式使用比较简单的事件埋点。复杂的话还是需要 JS 操作。
* JS 埋点统计用户可以通过浏览器禁用，CSS的话没办法禁用



