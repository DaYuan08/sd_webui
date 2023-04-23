# sd_webui
介于国内没有完善的stable-diffusion-webui食用指南 踩过一部份坑后 决定自己整理一个.

具体安装教程 官方已经说明的很清楚了 就不在这里赘述.

有需求的 可以先看看官方的教程 有问题可以在本项目底下提issues 有看到会回复.  
官方链接：https://github.com/AUTOMATIC1111/stable-diffusion-webui  

#正片开始

教程设备：MacBook Pro M1 Pro; OS版本：13.3.1

推荐插件：   
https://github.com/VinsonLaro/stable-diffusion-webui-chinese  
https://github.com/Mikubill/sd-webui-controlnet  
https://github.com/fkunn1326/openpose-editor  
https://github.com/pkuliyi2015/multidiffusion-upscaler-for-automatic1111  
https://github.com/adieyal/sd-dynamic-prompts  
https://github.com/toshiaki1729/stable-diffusion-webui-dataset-tag-editor  
https://github.com/Coyote-A/ultimate-upscale-for-automatic1111  

ps：教程底下都有详细说明

插件安装完毕后 算是可以真正开始起步了

win cmd/mac ter 启动项目后 访问 http://127.0.0.1:7860/ 进入界面；

原始界面
<img width="1337" alt="image" src="https://user-images.githubusercontent.com/49552459/233818016-5156d616-a21c-48e4-be72-b68498edcfcd.png">

安装汉化插件后 在选项栏 Settings - User interface - Localization (requires restart) 切换语言（需要重启：拉到顶部依次点击按钮 Apply settings - Reload UI；

切换成功后 
<img width="1728" alt="image" src="https://user-images.githubusercontent.com/49552459/233818332-519e8215-a84d-451a-9b1b-0d36aab4f2ab.png">

选项介绍
txt2img：文生图 根据文字描述生成图片；

img2img：图生图 顾名思义就是用图片生成图片；

Extras：高清化 简单理解就是“无损”放大图片用的 提高质量和细节；

PNG info：图片信息 可以获取由 SD webui 原始生成的png图片，png底下的exif信息里会写入图片生成所使用的参数；

Checkpoint Merger：模型（ckpt）合并 可以合并不同的模型，生成新的模型;

Train：训练 可以训练自己想要的模型;（这个我还在研究 到时候单独出教程

Settings：设置界面;

Extensions：扩展 插件管理页面;

#模型

由界面第一个选项得知 生成图片需要基于模型 所以下文是模型食用教程；
官方模型库：https://huggingface.co/models
推荐模型库：https://civitai.com/

模型一般分俩种类型：
1是 CHECKPOINT MERGE（合并模型）
CM模型下载好后 需要放到项目目录 /stable-diffusion-webui/models/Stable-diffusion 底下；
页面第一个选择框 选择的就是合并模型；
<img width="424" alt="image" src="https://user-images.githubusercontent.com/49552459/233818876-35ec72f4-649c-4ec7-be45-2088fab60d11.png">

2是 LORA （训练模型）
LORA模型下载好后 需要放到项目目录 /stable-diffusion-webui/models/Lora 底下;
在txt2img/img2img选项下 Prompt（提示词）框里使用以下语法食用：
<lora:lora_name:num> 
lora_name：下载的lora模型名称；
num：模型占比，适用于使用多个lora模型时 调整单个模型的占比 数字0.1到1;

<img width="968" alt="image" src="https://user-images.githubusercontent.com/49552459/233819208-c1fb23fe-1c53-4290-85d8-63caa0fdaf8a.png">



