# iShow
A h5 page generator, generated by editing json, and then through the phone side of the page through a series of functions rendering
Now, the editor is still missing a lot of ways, the phone side has not finished, there is a long way to go, so stay tuned

网站在线地址： [https://qiuyaofan.github.io/ishowPage](https://qiuyaofan.github.io/ishowPage)

文档： [https://qiuyaofan.github.io/iShow/](https://qiuyaofan.github.io/iShow/) 


### 编辑器截图部分截图如下：
  
#### 设置

![ishow](https://note.youdao.com/yws/api/group/7193078/noteresource/350388A0F6F1484EB37C7C759EF5F75D/version/26?method=get-resource&shareToken=668A129724ED4966804FBF3F174EC812&entryId=158676252 "ishow")

#### 选择图片


![ishow](https://note.youdao.com/yws/api/group/7193078/noteresource/56C821E765B444D5B5FB7DCA22251D96/version/27?method=get-resource&shareToken=668A129724ED4966804FBF3F174EC812&entryId=158676252 "ishow")

#### 列表打开页面-编辑


![ishow](https://note.youdao.com/yws/api/group/7193078/noteresource/E00E381E8D1F4AEDB969339679315E28/version/28?method=get-resource&shareToken=668A129724ED4966804FBF3F174EC812&entryId=158676252 "ishow")

### json渲染的手机端示例（iphone6为例）

![ishow](https://img.kxz.com/assets/kxz/ishow-20170908/mobile.png "ishow")

### ishow编辑器的主要功能如下：

```
ishow v1.0功能列表
一：字体编辑
1.普通样式：背景颜色，文字颜色，字体，对齐，透明度，边距，行高，大小，加粗，倾斜，下划线，清除格式
2.边框样式：宽度，颜色，类型，圆角
3.阴影样式：阴影颜色，大小，半径，方向
4.点击可修改文字，拖拽改变位置

二：图片编辑
基本编辑：参考字体编辑
添加图片，替换图片
拉伸改变大小，旋转
上传图片
图片选择弹层有：预览，裁切（后台未接，只提供裁切返回坐标，宽度），选择，删除等功能

三：动画效果
打字机，渐变，淡入淡出，旋转，缩放等，动画种类参考易企秀
时间，延时，添加动画，预览动画，清除动画
多个动画
次数，循环（1.0暂不实现）

四：左侧页面总预览
添加新一页，删除，排序（1.0暂不实现）

五：键盘操作
左右键移动元素
删除键删除选中元素
撤销ctrl+z(最多缓存40个操作)

六：层级调整（还需完善优化）

七：表单配置添加
目前支持表单类型：输入框，单选，多选，下拉，按钮
支持添加验证

八：h5提交配置
标题，封面等


九：保存，发布（模版，h5 json）


十：多媒体
背景添加
音频添加
视频添加（1.0暂不实现）


十一：模版管理（1.0暂不实现，需要后台配合）
编辑模版，搜索模版

十二：手机端渲染
根据json完成动画播放，翻页，音频播放，屏幕适配等
表单提交后台（未实现）
```


## 上手

```
 # 克隆项目
git clone https://github.com/qiuyaofan/iShow.git

# 安装编辑器依赖
cd ishow
npm install

# 安装手机端依赖
cd ..
cd ishow-mobile
npm install

//or # 建议不要用cnpm  安装有各种诡异的bug 可以通过如下操作解决npm速度慢的问题
npm install --registry=https://registry.npm.taobao.org

```
## 本地开发 开启服务

```
# ishow 编辑器端
cd ishow
npm run dev

#在浏览器打开
http://localhost:9900

# ishow 手机端
cd ..
cd ishow-mobile
gulp watch

在浏览器打开
http://localhost:9910/view/wap.html
```

### ishow调用的外部插件

IUI组件部分

swiper：[http://www.swiper.com.cn/api/index.html](http://www.swiper.com.cn/api/index.html) 

饿了么element：[http://element.eleme.io/#/zh-CN/component/installation](http://element.eleme.io/#/zh-CN/component/installation) 

参考的开源架子：[https://github.com/PanJiaChen/vue-element-admin](https://github.com/PanJiaChen/vue-element-admin)

### 开发思路

编辑器最终生成的是json配置，手机端通过json配置渲染出相应的样式，动画等。

#### mock.js切换

目前编辑器是用mock实现模拟接口，如果需要换回自己的接口

1.去除src/main.js的mock调用

2.修改utils/fetch.js代码

```
//mock.js
resolve(res);
//没有mock
// if (res.code === 40001) {
//   // 登出
//   store.dispatch('FedLogOut').then(() => {
//     router.push({ path: '/login' })
//   });
// } else if (res.code !== 200) {
//   Message({
//     message: res.msg,
//     type: 'error',
//     duration: 5 * 1000
//   });
//   reject(res);
// } else {
//   resolve(res);
// }

注释掉resolve(res);
下面的取消注释即可
```

json格式如下所示

```
var JSON={
    "page":[
        {
            "page": 1,
            "json": [
                {
			      ／***
			      	控件类型
				      "1":"text",
				      "2":"img",
				      "3":"textarea",
				      "4":"radio",
				      "5":"checkbox",
				      "6":"select",
				      "7":"button"
			      ***／
                    "type": 2,
                    "content": "https://img.kxz.com/assets/kxz/fixedInputCover1_20170630/fb7bf5d8-56d6-46ea-a01b-35e6943647da_demo1-4.png",
                    // 位置
                    "position": {
                        "top": 360,
                        "left": 201
                    },
                    "width": 175,
                    "height": 125.2680965147453,
                    //基本样式属性
                    "text": {
                        "backgroundColor": "rgba(0,0,0,0)",
                        "opacity": 100,
                        "padding": 0,
                        "rotate": 94,
                        "borderWidth": 0,
                        "borderRadius": 0,
                        "borderColor": "rgba(204, 204, 204,1)",
                        "borderStyle": "solid",
                        "shadowColor": "rgba(204, 204, 204,1)",
                        "shadowWidth": 0,
                        "shadowRadius": 10,
                        "shadowDire": 0
                    },
                    //动画类型，支持多动画
                    "animate": [
                        {
                            "animationName": "fadeIn",
                            "animationDuration": 2,
                            "animationTimingFunction": "ease",
                            "animationDelay": 0.4,
                            "animationFillMode": "both",
                            "animationPlayState": "initial",
                            "isOut": false
                        }
                    ],
                    "id": 1501745923909,
                    //层级
                    "zIndex": 6
                }
            
            ],
            //这一页的背景图片
            "bgImage": {
                "backgroundColor": "",
                "coord": "",
                "url": ""
            }
        },
       
    ],
    //配置
    "setting": {
        //背景音乐
        "bgMusic": {
            "url": "ttp://192.168.1.100:8080/uploadfile/3/15/5/8765a93f-351e-4984-8a03-6ef746ea36fd_bg.mp3",
            "name": "enemy2_down.mp3"
        }
    }
};
```

#### 更新说明

2018-07-13 ：完善z-index控制功能，添加动画次数控制，优化替换裁切组件   
 
