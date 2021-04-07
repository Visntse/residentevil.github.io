---
layout: default
---

### Development Unity3D Game From Wii’s Game Modle<br>
#### [JavaJdk](http://www.oracle.com/technetwork/java/javase/downloads/index.html)<br>
下载 JavaSe8U281
<hr>
#### [AndroidStudio](https://developer.android.com/studio/index.html)<br>
下载最新版并更新
<hr>
#### [Unity3D](https://store.unity.com/download?ref=personal)<br>
下载最新版
<hr>
#### [脚本](/other/Script.rar)<br>
拖入 Unity3D 的 Project 中
<hr>
#### 导入 Urp<br>
在`Window`下的`PackageManager`内安装`UniversalRp`
<hr>
#### 创建 Urp 渲染管线<br>
在`Project`内创建新渲染管线<br>
`Create`下的`Rendering`下的`UniversalRenderPipeline`下的`PipelineAsset`<br>
同时会创建`Renderer`名称结尾的渲染器，可适当调整配置渲染管线属性
<hr>
#### 启用 Urp 渲染管线<br>
在菜单栏`Edit`下的`ProjectSettings`下的`Graphics`下的`ScriptableRenderPipelineSettings`设置为上一步创建的`新渲染管线`
<hr>
#### 配置全局阳光<br>
`Light`下的`Mode`设置为`Realtime`
<hr>
#### 配置镜头<br>
`Camera`下的`PostProcessing`设置启用和`Antialiasing`设置为`Smaa`
<hr>
#### 创建后处理<br>
在`Hierarchy`内创建`Volume`下的`GlobalVolume`<br>
在`GlobalVolume`下的`Profile`创建`New`<br>
在`Project`内将会有新的`GlobalVolumeProfile`，可适当调整配置后处理特效
<hr>
#### 提取游戏模型与骨骼动画<br>
`Arc`文件用`BrresModelViewerAndConvert`打开<br>
`3DModels(NW4R)`是模型，`AnmChr(NW4R)`是骨骼动画<br>
模型导出为`Psk`格式，骨骼动画导出为`Psa`格式
<hr>
#### 转换模型与骨骼动画<br>
`DnUnPsaToolkit`依次添加`Psk`与`Psa`，并另存Psa为新文件<br>
`Psk`与`新Psa`用`Noesis`转换导出，类型选择`Fbx`<br>
转换时`AdbancedOptions`填入：<br>
```
-fmtoutidx 113 -smoothnorm 1 -combinemeshes -rotate 90 0 270 -scale 15 -fbxmeshmerge
```
<hr>
#### 导入 Fbx 至 Unity3D <br>
已实现脚本全自动化处理<br>
脚本在编辑器菜单栏创建`ChroniclesHorrorStory/AutoFix`菜单，将释放材质，贴图，骨骼等
<hr>
#### 骨骼动画绑定至模型<br>
已实现脚本全自动化处理<br>
脚本在编辑器菜单栏创建`ChroniclesHorrorStory/AutoFix`菜单，将绑定并设定相关数据等
