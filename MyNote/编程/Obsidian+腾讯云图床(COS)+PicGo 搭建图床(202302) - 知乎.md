---
page-title: "Obsidian+腾讯云图床(COS)+PicGo 搭建图床(202302) - 知乎"
url: https://zhuanlan.zhihu.com/p/514517568
date: "2023-04-14 09:55:37"
---
之前一直使用的是Gitee 或者Github 作为图床，但是由于后续图片越来越多，导致占用空间太大，以及访问速率等因素。 切换使用腾讯云COS。

使用三个月来，感觉挺不错的。因为个人写文档一直喜欢 Markdown 风格。 所以使用了Obsidian 。

下面是我总结的使用步骤以及注意事项。

整个过程分为以下三步：

1.  配置腾讯云COS： 存放图片并支持URL访问
2.  安装并配置PicGo ：实现上传图片并获取URL的工具
3.  安装并配置 Obsidian 的 auto upload image with picgo 插件: 在Obsidian 中使用上述功能。  
    

## 1\. 配置腾讯云COS

这里我选择的是腾讯云COS(Cloud Object Storage, 对象存储) . 官网如下：[对象存储数据处理\_COS数据处理\_数据处理方案-腾讯云](https://link.zhihu.com/?target=https%3A//cloud.tencent.com/product/cos)。

选择它的主要理由是腾讯云 COS 有免费额度。

![](https://pic4.zhimg.com/v2-ab30e0c81bf8d8fb4217e49b41dbad37_b.jpg)

具体的可以参考：[对象存储 免费额度-购买指南-文档中心-腾讯云-腾讯云](https://link.zhihu.com/?target=https%3A//cloud.tencent.com/document/product/436/6240)

### 1.1 创建存储桶

> 腾讯云建议使用子账号，这部分也可以参考官网的说明：[访问管理 新建子用户-用户指南-文档中心-腾讯云-腾讯云](https://link.zhihu.com/?target=https%3A//cloud.tencent.com/document/product/598/13674) 。

我这里暂未使用子账号。

打开腾讯云对象存储控制台，创建存储桶

![](https://pic1.zhimg.com/v2-b26c9909efccdf2cdd9b907e6c548570_b.jpg)

然后，

![](https://pic3.zhimg.com/v2-8cdc75b39d065907a4662ecaec2ab366_b.jpg)

需要注意的是： - 所属地域：尽量里自己所在的位置越近越好。 - 访问权限一定要选择**公有读私有写**，否则图片无法读取。 - 内容安全可以暂时不选。

然后可以直接“下一步”。

![](https://pic3.zhimg.com/v2-ec00d04d6db2f90c3c1f5bffef00735a_b.jpg)

最后，可以直接点击“创建”。

![](https://pic3.zhimg.com/v2-0d48ae68f3dd453529a64706fcb77472_b.jpg)

![](https://pic2.zhimg.com/v2-db8f8b0fcb7c0f817200c5cb947d8f21_b.jpg)

名称： image-1304515076 存储区域：ap-shanghai

后面配置图床的时候需要用到这两个。

### 1.2 访问管理

选择“立即使用”

![](https://pic1.zhimg.com/v2-b54f7fd9c6e06e3651d405a1c130aa2c_b.jpg)

下拉选择“密钥管理”，选择“API密钥管理”

![](https://pic2.zhimg.com/v2-52a6190eaaa9d905c1a4a70467a29c35_b.jpg)

新建密钥

（这里我已经新建好了）

![](https://pic4.zhimg.com/v2-23040a74e2e707dd6920f72a122e86ff_b.jpg)

APPID,Secretld 和Secretkey 下面配置腾讯云COS图床的时候用得到。

## 2\. 安装并配置PicGo

### 2.1 安装PicGo

这里直接去官网下载安装。

[PicGo](https://link.zhihu.com/?target=https%3A//picgo.github.io/PicGo-Doc/zh/) 或者[Github-PicGo](https://link.zhihu.com/?target=https%3A//github.com/Molunerfinn/PicGo)

我的电脑是Mac 安装之后的效果如下

![](https://pic3.zhimg.com/v2-9cf767a131c6f86643ce61ac984cf8ce_b.jpg)

### 2.2 配置腾讯云COS图床

![](https://pic1.zhimg.com/v2-57d3044598f484012c40193d5fc87768_b.jpg)

-   COS版本： 选择V5
-   APPID, Secretld 和Secretkey : 参考密钥管理
-   存储空间名： 就是存储桶的名称: image-1304515076
-   存储区域： 存储桶的存储区域： ap-shanghai
-   指定存储路径： 这里设置的是Obsidian

当前我使用的是 PicGo-2.3.0， 如果是PicGo-2.3.1。 这部分有一点区别需要注意下。

2.3.1 版本中的 "设定Bucket" 和 2.3.0 版本中的 “设定存储空间名”是一样的。

![](https://pic1.zhimg.com/v2-196a815975b4c8ea9612b5bdef96bce8_b.jpg)

### 2.3 验证上传

我们可以选择一张图片测试一下。

将图片拖到虚线框内，如果下面的进度条一直是蓝色则表示上传成功并转换成URL

如果是红色，那表示失败了。需要检查一下配置。

![](https://pic1.zhimg.com/v2-c8f64e81a1205d2fec2ee7fb0b1c8c74_b.jpg)

可以查看下相册

![](https://pic2.zhimg.com/v2-231b3c244910a859154b03ceade039a5_b.jpg)

或者查看腾讯云COS

![](https://pic3.zhimg.com/v2-cee7438ad1e6879123dd4e2303ce1636_b.jpg)

## 3\. 安装Obsidian 插件

Obsdian 安装 [GitHub - renmu123/obsidian-image-auto-upload-plugin: auto upload image with picgo](https://link.zhihu.com/?target=https%3A//github.com/renmu123/obsidian-image-auto-upload-plugin) 插件

安装成功过之后， Obsidian 选择 设置 找到 “Image auto upload Plugin”。

![](https://pic1.zhimg.com/v2-d19459268bb7249a8d89587b937e6eb0_b.jpg)

-   打开自动上传
-   PicGo server : 可以直接使用默认配置。

**有个地方需要特别注意的是**：

如果直接使用 markdown 的语法插入图片，是不会使用到图床的，引用的还是本地图片。

如果需要使用图床，正确的做法是**复制图片**，然后粘贴到Obsidian. 这样才会自动上传并返回URL。

我们可以看下上面这张图片上传成功并返回URL。

![](https://pic1.zhimg.com/v2-5fe575d855414f8f376229bf0d812ba0_b.jpg)

如果上传失败，可以按照上述步骤依次检查一下。