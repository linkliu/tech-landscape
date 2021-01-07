---
category: LayaBox
tags: [U3D, LayaBox,NavMesh,自动寻路]
---

## 在LayaBox中使用Unity的导航网格，实现AI自动寻路

使用这个这个库的好处在于，你不必了解AStar算法，一样可以使用AStar算法来进行AI导航。只需要调用接口即可。

下面我给出LayaBox的示例项目地址和Unity导出网格示例项目地址，各位按需克隆下来即可

Unity示例项目：[https://github.com/linkliu/ExportNavMesh](https://github.com/linkliu/ExportNavMesh)

LayaBox示例项目：[https://github.com/linkliu/LayaNavMesh](https://github.com/linkliu/LayaNavMesh)





原始的教程在[http://ask.layabox.com/question/47899](http://ask.layabox.com/question/47899)这里，大家可以去看看这里也行

这次的实例会从下面三个方面来讲解：

1. Laya要用到的导航组件库NavMesh.js
2. Unity如何将Navmesh数据导出成json文件【Laya中用到】
3. Unity中用到的NavMeshComponents



开始之前，说一下相关软件的版本

LayaAir 2.9 ,Laya引擎库2.7.1,Unity 2018.4.11f1

### 1.Laya中用到的导航组件库NavMesh.js

<div align="center"><img src="https://linkliu.github.io/tech-landscape/assets/img/Laya/diagram1.png"/></div>

<div align="center">可以直接在Unity中对导航网格进行编辑，非常的方便。</div>



NavMesh.js可以直接从这里去拿[https://github.com/lear315/NevMesh.Js/tree/main/build](https://github.com/lear315/NevMesh.Js/tree/main/build)

名字可能跟我的不一样，但是里面内容完全一样，我这里是强迫症发作，把**Nev**改成了**Nav**。然后只要拿**NavMesh.js**和**NavMesh.d.ts**这两文件就行了。NavMesh.js请放在Laya项目的**bin/libs**目录下面。**NavMesh.d.ts**放在项目的libs文件夹中。并且在bin/index.js中增加loadLib("libs/NevMesh.js")，注意需在loadLib("js/bundle.js");前面。完成上面这些步骤，就把导航组件库NavMesh.js放到我们的项目中了

### 2.Unity如何将Navmesh数据导出成json文件

将Unity的导航网格数据导出成LayaBox需要的json数据，需要用到两个关键文件，一个是把导航网格转换成.obj文件的**NavMeshExport.cs**。另一个是Python自动转换脚本[**convert_obj_three.py**](https://github.com/lear315/NevMesh.Js/blob/main/python/convert_obj_three.py)，这两个文件的获取方式，我贴在下面：

NavMeshExport.cs：[https://github.com/lear315/NevMesh.Js/tree/main/unity](https://github.com/lear315/NevMesh.Js/tree/main/unity)

convert_obj_three.py： [https://github.com/lear315/NevMesh.Js/tree/main/python](https://github.com/lear315/NevMesh.Js/tree/main/python)

**NavMeshExport.cs**是一个Unity中的一个C#脚本，只要放到Unity中即可，便会在Unity中生成一个导出菜单，合并在LayaBox的导出菜单中。如下图

<div align="center"><img src="https://linkliu.github.io/tech-landscape/assets/img/Laya/diagram1.jpg"/></div>

点击**Export**按钮，就会把当前的导航网格导出到**ExportNavMesh**文件中，里面就是需要下一步需要的.obj文件。



**convert_obj_three.py**是一个python脚本，所以各位需要安装python，并且配置配置好python环境，并且把python添加到系统的环境变量中去。

这个脚本的使用方法是 **python convert_obj_three.py -i xx.obj -o xx.json**，这个命令是把上一步生成的.obj文件转换成.json文件，这样我们就能在LayaBox中使用这个.json文件来进行AI导航了。

我的示例项目中已经做好了一键obj转json的功能，具体的用法是：选中你要转换的obj文件，然后右键，菜单选择**Convert Navmesh to Json**，就回自动在当前目录下生成一个同名的.json文件。这个就是LayaBox需要的文件，把这个文件放在LayaBox中的一个目录中。
<div align="center"><img src="https://linkliu.github.io/tech-landscape/assets/img/Laya/diagram2.jpg"/></div>

### 3.Unity中用到的NavMeshComponents

Unity中的导航网格的生成需要用到NavMeshComponents组件，目前这个组件Unity没有集成到Unity编辑器中，至少Unity2018以及之前的版本没有。但是Unity官方把它们放在Github上，地址在这里：[https://github.com/Unity-Technologies/NavMeshComponents](https://github.com/Unity-Technologies/NavMeshComponents)

克隆下来后，你只需要把**Assets/NavMeshComponents**这个文件复制到自己的项目中就行了，其他的东西可以不用。

NavMeshComponents的用法我就不细讲了，各位可以到[https://docs.unity3d.com/Manual/NavMesh-BuildingComponents.html](https://docs.unity3d.com/Manual/NavMesh-BuildingComponents.html)查看，也可以看这个中文的的博客[https://blog.csdn.net/wangjiangrong/article/details/88823523](https://blog.csdn.net/wangjiangrong/article/details/88823523)各位按需观看吧。



### 总结

完成上面的三个步骤后，准备工作都OK了，具体的使用，各位可以去看我的[LayaBox示例项目]()吧，哪里有完整的代码。

感谢各位耐心看完。