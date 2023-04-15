---
page-title: "Unity3D 拆包工具 AssetStudio 编译构建_Jaihk662的博客-CSDN博客"
url: https://mgamebox.notion.site/Unity3D-AssetStudio-_Jaihk662-CSDN-2dd143f811e346b9bc0cde7055b41dec
date: "2023-04-14 11:22:57"
---
#Unity3d
AssetStudio 这个工具就不介绍了，如果你看到了这篇文章那么你肯定带有目的~

其实无脑的话只要下载一个 [release](https://github.com/Perfare/AssetStudio/releases) 版本就可以，也就是下载并找到对应的 .exe 文件直接双击运行，看到下面这个界面就算是第一步成功：

![](https://mgamebox.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F8b528607-92a0-494a-8ac5-db8590c3097f%2F2021062417471389.png?id=6665dcec-6bed-489d-93da-ce668f8b139c&table=block&spaceId=47911401-7d9f-446f-97f5-b01eb2c2486d&width=1400&userId=&cache=v2)

不过有的时候需求没有那么简单，比如你要解的游戏包加了密，又或者你想要的是美术的一手资源，那么可能就没那么好办了，要不解出来的都是乱码，要不就是图片格式不正确，或者都是碎片资源，要你一个一个手动去加工处理……

所以最好的是从 github 上拿源码，然后自己去编译一份，这样你就可以改这个工具本身的代码逻辑了，也就是本文下面要介绍的

![](https://mgamebox.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F5287f73e-c01f-488c-b42f-10736b235337%2F20210624175527209.png?id=a8dba2fa-e194-449d-b1e4-5c15c024d3f7&table=block&spaceId=47911401-7d9f-446f-97f5-b01eb2c2486d&width=940&userId=&cache=v2)

之后就是熟悉的 git 操作了，clone 就可以

![](https://mgamebox.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F1e99280b-3f3e-4933-a170-d7cc5bc1bf0a%2F20210624175637837.png?id=c0b869a3-b610-4753-830b-c0a737b6dc85&table=block&spaceId=47911401-7d9f-446f-97f5-b01eb2c2486d&width=1280&userId=&cache=v2)

![](https://mgamebox.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F80d446e3-441c-45b7-a3a7-afee1b516826%2F20210624175712928.png?id=ba187cbd-dcd2-4481-bd4d-3ff638ccd493&table=block&spaceId=47911401-7d9f-446f-97f5-b01eb2c2486d&width=1140&userId=&cache=v2)

![](https://mgamebox.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F3766a011-7832-4145-9172-dabcc6216883%2F20210624175821331.png?id=e8657498-dec8-4db1-96ca-2a0e1a873854&table=block&spaceId=47911401-7d9f-446f-97f5-b01eb2c2486d&width=1040&userId=&cache=v2)

注意 github 上的 readme 有这样一句话：

![](https://mgamebox.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F3e485fcd-704b-4a6c-af36-a73e17a99ec3%2F20210624190316205.png?id=8cd07b15-da38-44f1-a079-1c470afb4b38&table=block&spaceId=47911401-7d9f-446f-97f5-b01eb2c2486d&width=1400&userId=&cache=v2)

之后打开 VS：上面菜单 → 项目 → 属性，按照以下步骤设置：

找到你对应 SDK 的 include 文件地址：默认是 C:\\Program Files\\Autodesk\\FBX\\FBX SDK\\2020.0.1\\include，把这个地址添加到配置属性 → C/C++ → 附加包含目录里面，并且复制一份里面的内容到你的 VS include 文件夹下，这个路径默认是 C:\\Program Files (x86)\\Microsoft Visual Studio\\2019\\Community\\VC\\Tools\\MSVC\\14.25.28610\\include。当然如果你自定义了安装目录，就要去你的安装目录里面找，下面同理

和步骤①几乎一样，找到对应 SDK 的 lib 附加目录库：默认地址是 C:\\Program Files\\Autodesk\\FBX\\FBX SDK\\2020.0.1\\lib\\vs2017\\x86\\debug，把这个地址添加到配置属性 → 连接器 → 常规 → 附加库目录里面，前提是你使用的是 debug 模式，release 模式类似

见下图③④，配置属性 → 连接器 → 输入 → 附加依赖项添加 libfbxsdk.dll，配置属性 → 连接器 → 输入 → 忽略特定默认库添加 LIBCMT

![](https://mgamebox.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fb3b2689a-ccc6-4de3-b5b7-b6f92cc81ba9%2F20210624190704907.png?id=f93939e2-d61b-4b9d-8807-33ab0be10874&table=block&spaceId=47911401-7d9f-446f-97f5-b01eb2c2486d&width=1400&userId=&cache=v2)

![](https://mgamebox.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F7dfcea85-d0fe-466f-8c62-6d1c2f6dac11%2F20210624191124703.png?id=f7dedf5d-9452-4e65-852b-0498f50723be&table=block&spaceId=47911401-7d9f-446f-97f5-b01eb2c2486d&width=1400&userId=&cache=v2)

![](https://mgamebox.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Faa59be55-8259-4955-8bca-b1b710b16b84%2F20210624191351583.png?id=3597ffde-6d87-49b2-9b37-605156391ea1&table=block&spaceId=47911401-7d9f-446f-97f5-b01eb2c2486d&width=840&userId=&cache=v2)

![](https://mgamebox.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F48c6dbcb-7c09-4d4a-858e-5dd9aae6fd5d%2F20210624191359448.png?id=f54001c4-39fd-4a4d-9fab-1146452c3d24&table=block&spaceId=47911401-7d9f-446f-97f5-b01eb2c2486d&width=990&userId=&cache=v2)

搞定之后，生成所有解决方案，注意报错，然后设置启动项目为 AssetStudioGUI，点击运行，搞定，后面就可以自由发挥了

![](https://mgamebox.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Faac4fa43-e865-46cf-8b0d-3d6982f60014%2F20210624191653798.png?id=dc13a511-432e-4717-8f2c-d83ba387bde8&table=block&spaceId=47911401-7d9f-446f-97f5-b01eb2c2486d&width=950&userId=&cache=v2)

![](https://mgamebox.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fa4d41968-e029-40ca-8d18-ce9b1b54485d%2F20210624191735568.png?id=536f1bc3-1107-4c28-8b89-9cde9759f03b&table=block&spaceId=47911401-7d9f-446f-97f5-b01eb2c2486d&width=1400&userId=&cache=v2)

如果对应的游戏没有加密的话，就要简单很多，几乎不需要任何基础知识和学习成本，按照步骤来就可以了，网上教程也一大堆

不过需要注意的是，很多游戏会有 obb 小包以及大量热更的内容，因此从官网下载的 apk 包里面资源是不全的，以明日方舟为例：apk 包的大小只有 1.97 个 G

![](https://mgamebox.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fb5a6ed46-aee2-49a5-b9f7-14fa83160742%2F20210625151348349.png?id=7dda1cb4-9bd6-400a-8dcf-150313f7739a&table=block&spaceId=47911401-7d9f-446f-97f5-b01eb2c2486d&width=1070&userId=&cache=v2)

而在你第一次进游戏的时候，还会需要再下载 1.7 个 G左右，这部分内容在 Android/data/com.hypergryph.arknights 文件夹内，如果是模拟器的话路径可能不同，并且拷贝前需要将它们先复制一份到共享文件夹里

![](https://mgamebox.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Ff23051cd-2d29-4897-a8f6-1146e2a05799%2F20210625151928326.png?id=291ede87-a91e-43a9-aec5-76a300776655&table=block&spaceId=47911401-7d9f-446f-97f5-b01eb2c2486d&width=1400&userId=&cache=v2)

热更文件：Android/data/com.\[name\]

obb 包：Android/obb/com.\[name\]，这个只有少部分游戏有，明日方舟就无

好了，不考虑 obb 包的话，两个文件里面的 AB 路径就会是完全相同的，因此拷贝去叠起来就可以得到整包的内容了

![](https://mgamebox.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F8c4f1d8a-cabf-4986-8419-509597644b05%2F2021062515300881.png?id=c44aafad-7656-4d5d-9fae-27b297c6dd11&table=block&spaceId=47911401-7d9f-446f-97f5-b01eb2c2486d&width=510&userId=&cache=v2)

![](https://mgamebox.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fc374b63f-d904-4c15-ba13-5c445255ce02%2F20210626210834769.png?id=7a2da687-8564-499f-b39f-d7333cb35b91&table=block&spaceId=47911401-7d9f-446f-97f5-b01eb2c2486d&width=630&userId=&cache=v2)

![](https://mgamebox.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fbb9a0151-001b-491c-bb47-4ae84d17ed6c%2F20210626210907794.png?id=f6e15855-ce99-492f-b3c3-26041dea1724&table=block&spaceId=47911401-7d9f-446f-97f5-b01eb2c2486d&width=1380&userId=&cache=v2)

Filter Type 就是分类筛选，而点击左边的 Export 就可以导出

![](https://mgamebox.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fafbfd261-6052-4c69-9df0-38d3a03d1b66%2F20210626210939658.png?id=3d84a5ad-298a-4ee9-953d-527bb2949e08&table=block&spaceId=47911401-7d9f-446f-97f5-b01eb2c2486d&width=960&userId=&cache=v2)