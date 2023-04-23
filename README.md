# sd_webui 食用指南
介于国内没有完善的stable-diffusion-webui食用指南 踩过一部份坑后 决定自己整理一个.

具体安装教程 官方已经说明的很清楚了 就不在这里赘述.

有需求的 可以先看看官方的教程 有问题可以在本项目底下提issues 有看到会回复.  
官方链接：https://github.com/AUTOMATIC1111/stable-diffusion-webui  

# 正片开始

教程设备：MacBook Pro M1 Pro; OS版本：13.3.1  
win和mac只有安装环节的区别 食用方式还是一样的；

推荐插件：   
https://github.com/VinsonLaro/stable-diffusion-webui-chinese  
https://github.com/Mikubill/sd-webui-controlnet  
https://github.com/fkunn1326/openpose-editor  
https://github.com/pkuliyi2015/multidiffusion-upscaler-for-automatic1111  
https://github.com/adieyal/sd-dynamic-prompts  
https://github.com/toshiaki1729/stable-diffusion-webui-dataset-tag-editor  
https://github.com/Coyote-A/ultimate-upscale-for-automatic1111  
ps：教程底下都有详细安装说明 我就不贴出来了  

插件安装完毕后 算是可以真正开始起步了；  
win cmd/mac ter 输入命令 webui.bat\/.webui.sh 启动项目；  
访问 http://127.0.0.1:7860/ 进入界面；  

原始界面  
<img width="1337" alt="image" src="https://user-images.githubusercontent.com/49552459/233818016-5156d616-a21c-48e4-be72-b68498edcfcd.png">

安装汉化插件后 在选项栏 Settings - User interface - Localization (requires restart) 切换语言;  
切换后需要重启 拉到顶部依次点击按钮 Apply settings - Reload UI；  

切换成功后  
<img width="1728" alt="image" src="https://user-images.githubusercontent.com/49552459/233818332-519e8215-a84d-451a-9b1b-0d36aab4f2ab.png">

### 选项介绍：

txt2img：文生图 根据文字描述生成图片；

img2img：图生图 顾名思义就是用图片生成图片；

Extras：高清化 简单理解就是“无损”放大图片用的 提高质量和细节；

PNG info：图片信息 可以获取由 SD webui 原始生成的png图片，png底下的exif信息里会写入图片生成所使用的参数；

Checkpoint Merger：模型（ckpt）合并 可以合并不同的模型，生成新的模型；

Train：训练 可以训练自己想要的模型；（这个我还在研究 到时候单独出教程

Settings：设置界面；

Extensions：扩展 插件管理页面；

# 模型

生成图片需要基于模型，可以从已有模型库下载；    
官方模型库：https://huggingface.co/models  
推荐模型库：https://civitai.com/  

### 模型一般分俩种类型：  

##### 1 是 CHECKPOINT MERGE（合并模型）  
CM模型下载好后 需要放到项目目录 /stable-diffusion-webui/models/Stable-diffusion 底下；

页面第一个选择框 选择的就是合并模型；  
<img width="424" alt="image" src="https://user-images.githubusercontent.com/49552459/233818876-35ec72f4-649c-4ec7-be45-2088fab60d11.png">

##### 2 是 LORA （训练模型）  
LORA模型下载好后 需要放到项目目录 /stable-diffusion-webui/models/Lora 底下;  

在txt2img/img2img选项下 Prompt（提示词）框里使用以下语法食用：  

\<lora:lora_name:num\>   
lora_name：下载的lora模型名称；  
num：模型占比，适用于使用多个lora模型时 调整单个模型的占比 数字0.1到1;  

如图：  
<img width="968" alt="image" src="https://user-images.githubusercontent.com/49552459/233819208-c1fb23fe-1c53-4290-85d8-63caa0fdaf8a.png">

选择好模型后 就要开始填写Prompt(提示词)了；

# txt2img

### Prompt(提示词)：  

用文字描述你想要生成的图片；  
输入语言为英语 支持用口语化的形式描述 不过一般还是用一个个的关键字(逗号隔开)去描述；

### 语法：

##### 1.分隔：
多个关键字之间 需要用英文符号逗号‘,’分隔开 逗号前后允许空格和换行的存在；  
eg：1girl, long hair, smile, full body, long legs, (1个女孩，长发，微笑，全身，长腿）


##### 2.混合：  
多个关键字之间用英文符号'|'分隔 可以实现多个要素 需要注意混合比例；  
eg：1girl, long hair, pink | purple hair, (1个女孩，长发，粉色和紫色混合头发）

##### 3.增强/减弱：  
分俩种写法
1. (提示词:权重数值)
  + 数值从0.1 ~ 100 默认是1 低于1就是减弱 高于1就是加强
  + eg：(beautiful eyes:1.2),(light smile:1.8)
2. (((提示词))) / [提示词]
  + 倍数 一层阔号代表增强1.1倍 俩层就是1.1\*1.1=1.21倍 依次类推
  + eg：(((glasses))),\[long hair\]

##### 4.渐变：  
我的理解是 先按语法第一个提示词生成主体 再向第二个提示词进行过渡；  
语法：\[提示词1:提示词2:num\]  

num：
  + 数字大于1时，表示第‘num‘步之前按‘提示词1’生成 第‘num‘步后 按‘提示词2’叠加效果；  
  + eg：1girl, long hair, [pink:purple:10] hair,    
  + 数字小于1时，表示总步数的百分之’num‘按’提示词1‘生成 之后按‘提示词2’叠加效果；  
  + 1girl, long hair, [pink:purple:0.5] hair,  
ps：这里的步数指 Sampling steps 采样步数  

##### 5.交替  
轮流替换使用提示词；  
语法：\[提示词1|提示词2\] in a field  
eg：\[cow|horse\] in a field,（牛马混合物 简单解释就是 先按牛生成 再按马生成 实测生成的是牛头马身hhh）   

### 范例：  

提示词有推荐按以下格式去填写 有一定的先后顺序 方便调整；

画质词 > 风格词 > 主体 > 主题外表(从上到下）> 主体情绪 > 主体姿势（从上到下）> 背景词 > 其他描述
  + 画质词：低/中/高 等；
  + 风格词：写实/动漫/插画/油画 等；
  + 主体：1任何主体 1代表1个主体 可以是人 可以是动物 等；
  + 主体外表：
    + 发型：长/短发 刘海 高/低单/双马尾 卷发；
    + 发色：任意颜色 头顶发色 挑染发色；
    + 衣服：任何衣物 可以指定颜色 状态；
    + 头部：头部饰品 帽子 发夹；
    + 眼睛：颜色 美瞳；
    + 颈部：颈部饰品；
    + 胸部：大中小；
    + 腹部：是否露出腹部 肚脐；
    + 臀部：大中小；
    + 腿部：长短粗细 鞋类；
  + 主体情绪：任何情绪 可以加修饰词 笑 -> 微笑；
  + 主体姿势：
    + 基本动作：走 跑 站 坐 蹲 趴 跪；
    + 头部动作：低头 仰头 歪头 面向观众 回头看；
    + 手部动作：举手 放置部位；
    + 腰部动作：弯腰；
    + 腿部动作：交叉腿 盘腿 M形开腿 二郎腿 小日子的跪坐也可以；
    + 其他动作：战斗姿态 背对背；
  + 背景词：
    + 场景：室内/外 城市 郊外；
    + 地点：办公室 咖啡厅 电影院 教学楼；
    + 天气：任何天气 可以带强度 大太阳 暴雨；
  + 其他描述：细节描述词

eg：high quality,（高质量的）realistic,（写实的）1girl, short hair, brown hair, white shirt, brown eyes, heart necklace, breasts, abdomen, ass, legs, high heels, （1个女孩，棕色短发，白色衬衫，棕色眼睛，心形项链，胸部，腹部，臀部，腿，高跟鞋）light smile,（微笑）sitting, looking at viewer, hand on hip,(坐姿，看向观众，单手叉腰）outdoors, cityscape,（在室外，城市背景） 

### Negative prompt(反向提示词)：  

用文字描述不想在图片中出现的东西；（具体食用方式 还在研究）

1. 对图片进行去噪处理，使其看起来更像你的提示词；  
2. 对图片进行去噪处理，使其看起来更像你的反向提示词（无条件条件）；  
3. 观察这两者之间的差异，并利用它来产生一组对噪声图片的改变；  
4. 尝试将最终结果移向前者而远离后者；  
5. 一个相对比较通用的负面提示词设置；  

部分反向提示词：worst quality,low quality,normal quality,bad hands,text,error,missing fingers,unclear eyes,fewer digits,cropped,jpeg artifacts,Humpbacked,signature,watermark,blurry,missing arms,long neck,missing limb,too many fingers,mutated,poorly drawn,out of frame,bad hands,lowres,bad anatomy,poorly drawn,cloned face,bad face

### Sampling Steps(采样迭代步数)：  

AI绘图是有一个过程的：  
先随机出一个噪声底片 后根据你的提示词和反向提示词一步步调整图片；  
Sampling Steps设置的就是调整的步数 步骤越多 每一步调整就越精细 但是生成时间就会相应增加；  
所谓 慢工出细活；  
不过大部分场景 步数一般是20到40之间 超过40后都是肉眼很难区分的细节了；  

### Sampling method(采样方法)： 

选择AI绘图的风格 具体区别可以自己搜一下 我还没研究出个所以然；

### Width/Height(宽度/高度)：

图片的尺寸 单位是像素 适当增加可以提高图片的细节 但是相对应的运行成本也会增加；

### Batch count(生成次数)： 

同样的配置 生成的时候跑几次；

### Batch size(每次数量)： 

每次生成的图片数量 公式是Batch count\* Batch size = 最终生成的图片数量 比较吃显存；

### CFG Scale(提示词引导系数)： 

设置图片跟提示词的匹配程度 一般值7～15 太高会降低画质；

### Seed(图像生成种子)： 

一个固定随机数生成器输出的值 以相同参数和随机种子生成的图像会得到相同的结果 适用于使用他人提供的配置 能画出接近的图片；  
默认值 -1 则每次都会使用一个新的随机数；  

### Restore faces(面部修复)： 

能使人脸更加真实 我还没研究出个所以然；

### Tiling(无缝贴图)： 

生成拼接的图像 类似拼图；

### Hires. fix(高分辨率修复)： 

还没研究出个所以然；

# 已有作品食用指南

以下以 https://civitai.com/ 的作品为例；

进入网站后 选择喜欢的模型 需要关注的是 模型的Type；  
下载的时候要根据不同的类型放置在不同的目录底下 上文[模型一般分俩种类型](#模型一般分俩种类型)有提到；   

<img width="1726" alt="image" src="https://user-images.githubusercontent.com/49552459/233831051-04610d43-913f-42fa-9f6f-98d307b62aad.png">

拉到页面底下 会有该模型的其他作者的作品 点开一个进入到详情页；  
详情页拉到底部 会有这张图片生成的参数 一一对应copy到你的webui下面 点击Generate(生成）就可以静候佳音了；  
<img width="1727" alt="image" src="https://user-images.githubusercontent.com/49552459/233831410-42f40b12-c011-4bf0-ac34-5037ee33ba6d.png">


# 总结

目前整理的大概就是这些 后续会继续完善教程；  
如果食用教程时发现有问题的地方或者有任何建议 欢迎提Issue 我有看到都会回复的；

如果觉得这篇教程帮助到了你 可以请我吃根棒棒糖🍭；  
<img src="https://user-images.githubusercontent.com/49552459/233831831-d98d3881-4cb7-4450-a395-a4af4898efa2.jpeg" width="240px" height="320px" />
<img src="https://user-images.githubusercontent.com/49552459/233831832-5a77ce53-32a2-4a3b-98f0-107aa4a648a7.jpeg" width="240px" height="380px" />




