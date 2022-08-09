# 西南交通大学VGE小组2022年暑期交流培训

> 本教程分为五部分，第一部分主要包括一些常用工具如git, node, conda的使用及开发环境配置，同时对本专业常用的一些第三方开源库进行简单介绍；第二部分针对小组DT平台的前端开发，主要包括vue, cesium的使用，同时介绍软件架构和模块设计的一些内容；第三部分为后端开发，本部分内容主要介绍使用不同语言如何快速搭建后端服务，没有涉及分布式等更高阶内容；第四部分为桌面端开发，分别使用qt框架和electron框架开发简单示例；第五部分为移动端开发，为了更好适配小组技术栈，主要介绍vant-cordova组合开发。

## 1. 环境配置与基础知识

### 1.1 使用[git](https://git-scm.com/)进行代码管理及多人协作

> git相关命令

1. 本地初始化git仓库
    ``` bash
    git init
    ```
2. 从远程克隆git仓库到本地
    ``` bash
    git clone url_to_repo
    ```
3. git分支相关内容
    * 创建新的分支
    ``` bash
    git checkout -b branch_name
    ```
    * 切换到分支
    ``` bash
    git checkout branch_name
    ```
    * 删除分支
    ``` bash
    git branch -d branch_name
    git branch -D branch_name # 强制删除分支
    ```
    * 查看分支
    ``` bash
    git branch -a # 查看包括远程仓库中的所有分支
    git branch -l # 查看本地所有分支
    ```
4. 添加要提交的变更文件
    ``` bash
    git add path_to_dir/path_to_file
    ```
5. 提交变更到仓库
    ``` bash
    git commit -m "message of description for this commit"
    ```
6. 上传变更到远程仓库某一分支
    ``` bash
    git push origin branch_name
    ```
7. 同步某分支远程代码到本地
    ``` bash
    git fetch origin branch_name
    ``` 
8. 同步某分支远程代码到本地分支
    ``` bash
    git checkout --track origin/branch_name
    ```
9. 拉取同时合并某一分支最新代码
    ``` bash
    git pull origin branch_name
    ```
10. 代码合并
    ``` bash
    git merge branch_name
    ```
    使用VSCode或GitKraken检查合并冲突代码
11. 远程仓库相关内容
    * 添加远程仓库关联到本地仓库
    ``` bash
    git remote add short_name url
    ```
    * 移除远程仓库关联
    ``` bash
    git remote remove short_name
    ```
    * 查看远程仓库关联情况
    ``` bash
    git remote show short_name
    ```
> 使用[github](https://github.com/)远程托管代码
1. [创建自己的仓库](https://docs.github.com/cn/github/getting-started-with-github/quickstart/create-a-repo)
2. fork别人的仓库
3. 为本地git添加github账号邮箱
    ``` bash
    git config --global user.name "username"
    git config --global user.email "email"
    ```

### 1.2 使用[npm](https://www.npmjs.com/)配置javascript开发环境

> npm相关基础命令
1. 下载安装[node.js](https://nodejs.org/)

2. 根据第三方库名称安装依赖
    ``` bash
    npm install libname # 为当前工程安装
    npm install -g libname # 全局安装
    ```
3. 安装指定版本号的依赖库
    ``` bash
    npm install libname@vmax.vmid.vmin
    ```
4. 编写package.json配置
    ``` json
    {
        "name": "ProjectName",
        "version": "max.mid.min",
        "description": "Some introduction",
        "main": "dist/CesiumMeshVisualizer.js",
        "module": "SourceES6/Main.js",
        "type": "module",
        "scripts": {
            "serve": "vue-cli-service serve",
            "build": "vue-cli-service build"
        },
        "keywords": [
            "NameA",
            "NameB",
        ],
        "author": {
            "name": "WouRaoyu",
            "email": "haoyu.wu@my.swjtu.edu.cn"
        },
        "license": "MIT",
        "dependencies": {
            "lib": "^version"
        },
        "devDependencies": {
            "lib": "^version",
        }
    }
    ```

5. 根据package.json配置调试工程

    ``` bash
    npm run serve
    ```

6. 根据package.json配置编译工程
    ``` bash
    npm run build
    ```

> vue相关基础命令
1. 使用[vue cli](https://cli.vuejs.org/zh/)或[vite](https://www.vitejs.net/)进行Vue项目的快速构建及开发
    ``` bash
    # vue cli
    npm install -g @vue/cli
    # vite
    npm install -g vite@latest
    ```
2. 初始化工程，构建工具会自动生成基础文件及目录结构
    ``` bash
    # vue cli
    vue create project-name
    # vite
    npm init vite@latest
    ```
3. 添加依赖库及调试打包与上述js基本一致

### 1.3 使用conda配置python及cpp开发环境

> conda相关命令

1. 安装[anaconda](https://www.anaconda.com/products/distribution)或[mimiconda](https://docs.conda.io/en/latest/miniconda.html)

2. 添加conda-forge镜像源
    ``` bash
    conda config --add channels conda-forge
    ```
3. 使用conda命令行安装配置依赖库
    ``` bash
    conda install libname=version
    ```
4. 移除依赖库
    ``` bash
    conda remove libname
    ```
5. 创建新的环境-没有配置文件
    ``` bash
    conda create -n envname
    ```
6. 查看已创建的所有环境
    ``` bash
    conda env list
    ```
6. 使用配置文件创建环境，新建file_name.yml文件，内容组织如下
    ``` yml
    channels:
        - conda-forge
        - defaults

    dependencies:
        - libname
    ```

    ``` bash
    conda env create -n gisenv -f file_name.yml
    ```
7. 激活conda环境
    ``` bash
    conda activate env-name
    ```
8. 到处conda环境配置文件
    ``` bash
    conda env export -n envname > file_name.yml
    ```
9. 删除conda环境
    ``` bash
    conda env remove -n envname
    ```

### 1.4 常用ide简单介绍及插件配置
1. 微软[Visual Studio](https://visualstudio.microsoft.com/)，主要用于C系列语言的开发，功能强大开箱即用，不依赖插件
2. 微软[Visual Studio Code](https://code.visualstudio.com/)，本身是文本编辑器，但插件非常丰富，支持各种语言，大量功能可以通过配置插件实现，如各类型语言语法高亮，配置编译环境, 可以在左侧边栏搜索并在线安装
    * 快捷键Ctrl + / -> 注释
    * 快捷键Ctrl + Shift + P -> 快捷指令搜索面板
    * 快捷键Ctrl + P -> 工程文件搜索
    * 快捷键Ctrl + F -> 文本字符串搜索 
3. 谷歌[Android Studio](https://developer.android.com/studio)，主要用于移动端Android系统软件的开发
4. Jetbrains[PyCharm](https://www.jetbrains.com/pycharm/)，主要用于Python的开发，功能强大开箱即用，不依赖插件

### 1.5 常用开源库简单介绍-js

1. GIS三维可视化引擎 [Cesium](https://cesium.com)
2. 三维可视化引擎 [Threejs](https://threejs.org)
3. 轻量化地学空间数据处理 [Turf](http://turfjs.org)
4. 图表数据可视化 [ECharts](https://echarts.apache.org)

### 1.6 常用开源库简单介绍-cpp

1. 地学空间数据处理库 [GDAL](https://gdal.org)
2. 计算几何算法库 [CGAL](https://www.cgal.org)
3. 参数化建模库 [OCCT](https://www.opencascade.com)
4. 科学数据三维可视化 [VTK](https://vtk.org)
5. 三维可视化 [OSG](http://www.openscenegraph.com)

### 1.7 常用开源库简单介绍-python

> 通常较为成熟的cpp语言项目都会有对应的python导出版本可供调用

1. 机器学习集成库 [scikit-learn](https://scikit-learn.org)
2. 深度学习框架 [tensorflow](https://www.tensorflow.org)
3. 深度学习框架 [pytorch](https://pytorch.org)
4. 图表数据可视化 [matplotlib](https://matplotlib.org)

## 2. 前端开发 

### 2.1 开发环境搭建
1. 前端开发需要配置PC端JS运行环境([node.js](https://nodejs.org/zh-cn/))，包管理器([npm](https://www.npmjs.com/))，代码编辑器([vscode](https://code.visualstudio.com/))，浏览器端调试运行环境([chrome](https://www.google.com/intl/zh-CN/chrome/))，npm不需要单独安装，其被包含在node.js安装包中
2. 小组目前大部分平台基于 [Vue 2.x](https://cn.vuejs.org/index.html) + [ElementUI 2.x](https://element.eleme.cn/#/zh-CN) 框架研发，VSCode需要安装Vetur插件来进行语法高亮
3. Vue提供[Vue Cli](https://cli.vuejs.org/zh/)进行Vue项目的快速构建及开发，为PC全局配置Vue Cli
    ``` bash
    npm install -g @vue/cli
    ```
### 2.2 初始化平台
1. 使用Vue Cli初始化工程
    ``` bash
    vue create dt-demo
    ```
2. 使用VSCode打开创建好的工程文件夹
3. 命令行使用npm安装基础依赖库[cesium, element-ui, sass, sass-loader]
    ``` bash
    npm install cesium@1.80.0
    npm install element-ui@2.15.0
    npm install sass@1.39.0
    npm install sass-loader@8.0.2
    ```
4. 为工程配置Cesium可视化引擎，在根目录新建vue.config.js文件
    * 方法一：配置node_modules中安装好的cesium
    ``` js
    const path = require('path')
    const webpack = require('webpack')
    const CopyWebpackPlugin = require('copy-webpack-plugin')

    let copyPath = ''
    let cesiumPath = 'node_modules/cesium/Source'
    if (process.env.NODE_ENV === 'production')  {
        cesiumPath = 'node_modules/cesium/Build/Cesium'
        copyPath = 'libs/'
    }

    const plugins = [
        new webpack.DefinePlugin({CESIUM_BASE_URL: JSON.stringify(copyPath)}),
        new CopyWebpackPlugin([{ from: path.join(cesiumPath, 'Workers'), to: copyPath + 'Workers' }]),
        new CopyWebpackPlugin([{ from: path.join(cesiumPath, 'Assets'), to: copyPath + 'Assets' }]),
        new CopyWebpackPlugin([{ from: path.join(cesiumPath, 'ThirdParty'), to: copyPath + 'ThirdParty' }]),
        new CopyWebpackPlugin([{ from: path.join(cesiumPath, 'Widgets'), to: copyPath + 'Widgets' }])
    ]

    module.exports = {
        publicPath: '/',
        outputDir: 'dist',
        runtimeCompiler: true,
        devServer: {
            open: true,
            host: '0.0.0.0',
            port: 8080,
            https: false,
            hotOnly: false
        },
        configureWebpack: {
            module: {
                unknownContextCritical: false,
            },
            resolve: {
                alias: {
                    '@': path.join(__dirname, "src")
                }
            },
            plugins: plugins
        },
    };
    ```
    * 方法二：将打包后的Cesium拷贝到public中以外部库形式直接引入
    ``` html
    <!--修改public文件夹中的index.html文件 在<head>中添加 -->
    <script src="./Cesium/Cesium.js"></script>
    <link rel="stylesheet" type="text/css" href="./Cesium/Widgets/widgets.css"/>
    ```
    ``` js
    const path = require('path')
    module.exports = {
        publicPath: '/',
        outputDir: 'dist',
        runtimeCompiler: true,
        devServer: {
            open: true,
            host: '0.0.0.0',
            port: 8080,
            https: false,
            hotOnly: false
        },
        configureWebpack: {
            module: {
                unknownContextCritical: false,
            },
            resolve: {
                alias: {
                    '@': path.join(__dirname, "src")
                }
            },
            externals: {
                'Cesium': 'Cesium'
            },
        },
    };
    ```
5. 在main.js中声明全局变量DTGlobe，用于动态存放后续构造的一些需要全局使用的变量，如viewer
    ``` js
    Vue.prototype.DTGlobe = new Array();
    ```
6. 修改工程自动生成的HelloWorld.vue文件，创建Viewer实例，如果要使用Cesium提供的地形及底图服务，需注册并申请[token](https://cesium.com/ion/tokens)
    ``` html
    <template>
        <div style="height: 100%; width: 100%">
            <div id="container" />
        </div>
    </template>

    <script>
    import * as Cesium from "cesium";
    // 如果是直接引入的node_modules中的cesium需要在vue中引入样式 否则不需要
    import 'cesium/Source/Widgets/widgets.css'
    export default {
        beforeMount() {
            this.$nextTick(() => {
                Cesium.Ion.defaultAccessToken = 'token';
                const viewer = new Cesium.Viewer("container");
                this.DTGlobe.push(viewer);
            })
        }
    };
    </script>

    <!-- Add "scoped" attribute to limit CSS to this component only -->
    <style lang="scss" scoped>
    #container {
        height: 100%;
        width: 100%;
    }
    ::v-deep {
        .cesium-viewer-bottom {
            display: none;
        }
    }
    </style>
    ```
7. 调整各页面样式，将三维场景填满整个视窗
    ``` css
    html,
    body,
    #app {
        overflow: hidden;
        height: 100%;
        width: 100%;
        padding: 0;
        margin: 0;
    }
    ```
8. 为平台添加背景图、平台名称、小组Logo
    ``` html
    <div id="background" />
    <div id="title-name"> VGE小组数字孪生测试系统 </div>
    <img id="vge-logo" src="./assets/vge.png" />
    ```
    ``` css
    #background {
        z-index: 9;
        background-image: url('./assets/bg.png');
        pointer-events: none;
        background-size: 100% 100%;
        background-repeat: no-repeat;
        position: absolute;
        height: 100%;
        width: 100%;
    }
    #title-name {
        top: 2vh;
        z-index: 9;
        color: white;
        width: 100%;
        font-size: 4vh;
        font-weight: bold;
        text-align: center;
        position: absolute;
        pointer-events: none;
    }
    #vge-logo {
        z-index: 9;
        width: 8vh;
        height: 8vh;
        left: 2vw;
        bottom: 5vh;
        position: absolute;
    }
    ```
9. 引入ElementUI，可直接引入全部组件也可按需引入
    * 全部引入
    ``` js
    import 'element-ui/lib/theme-chalk/index.css';
    import ElementUI from 'element-ui'
    Vue.use(ElementUI)
    ```
    * 按需引入
    ``` js
    import 'element-ui/lib/theme-chalk/index.css';
    import { NameOfComp } from 'element-ui';
    Vue.use(NameOfComp)
    ```
10. 创建自定义面板

### 2.3 CesiumJS实例功能
1. [Viewer](https://cesium.com/learn/cesiumjs/ref-doc/Viewer.html) 视图
    ``` js
    // container代表html中提前初始化的id为container的div
    const viewer = new Cesium.Viewer('container', {
        animation: false, // 动画播放器控件
        baseLayerPicker: false, // 图层选择控件
        cesiumLogo: false, // 是否显示cesium图标
        fullscreenButton: false, // 全屏按钮控件
        geocoder: false, // 地名检索控件
        homeButton: false, // home视角按钮控件
        vrButton: false, // vr模式切换按钮控件
        navigationHelpButton: false, // 原生帮助按钮控件
        sceneModePicker: false, // 投影方式选择图标控件
        timeline: false, // 底部时间线
        scene3DOnly: false, // 是否只渲染3D场景
        shouldAnimate: true, // 是否允许动画效果
        infoBox: false, // 属性信息窗口
        shadows: false, // 光照阴影效果
        terrainShadows: Cesium.ShadowMode.ENABLED, // 地形光照阴影
        imageryProvider: Cesium.createWorldImagery(), // 添加全球影像图层
        terrainProvider: Cesium.createWorldTerrain() // 添加全球地形
    })
    ```
2. [Globe](https://cesium.com/learn/cesiumjs/ref-doc/Globe.html) 主体地球
    * [ImageryLayer](https://cesium.com/learn/cesiumjs/ref-doc/ImageryLayer.html) 图层
        * [WebMapServiceImageryProvider](https://cesium.com/learn/cesiumjs/ref-doc/WebMapServiceImageryProvider.html) 加载WMS底图服务
        * [WebMapTileServiceImageryProvider](https://cesium.com/learn/cesiumjs/ref-doc/WebMapTileServiceImageryProvider.html) 加载WMTS底图服务
        * [UrlTemplateImageryProvider](https://cesium.com/learn/cesiumjs/ref-doc/UrlTemplateImageryProvider.html) 加载url模板影像底图（通常用于自定义切片影像）
        * [ArcGisMapServerImageryProvider](https://cesium.com/learn/cesiumjs/ref-doc/ArcGisMapServerImageryProvider.html) ArcGis底图服务（受网络限制有时会很慢）
        * [OpenStreetMapImageryProvider](https://cesium.com/learn/cesiumjs/ref-doc/OpenStreetMapImageryProvider.html) OSM底图服务（受网络限制有时会很慢）
        * [BingMapsImageryProvider](https://cesium.com/learn/cesiumjs/ref-doc/BingMapsImageryProvider.html) Bing底图服务（需要Bing的token）
        * [ImageryLayerCollection](https://cesium.com/learn/cesiumjs/ref-doc/ImageryLayerCollection.html) 图层集合
    ```js
        viewer.imageryLayers // 获取视图对应的图层集合
    ```
    * [Terrain](https://cesium.com/learn/cesiumjs/ref-doc/CesiumTerrainProvider.html) 地形
        * [createWorldTerrain](https://cesium.com/learn/cesiumjs/ref-doc/global.html?classFilter=glob#createWorldTerrain) 创建全球地形（需要Cesium的token）
        * [sampleTerrain](https://cesium.com/learn/cesiumjs/ref-doc/global.html?classFilter=Terrain#sampleTerrain) or [sampleTerrainMostDetailed](https://cesium.com/learn/cesiumjs/ref-doc/global.html?classFilter=Terrain#sampleTerrainMostDetailed) 地面点批量采样
        * [Globe#getHeight](https://cesium.com/learn/cesiumjs/ref-doc/Globe.html#getHeight) 获取地面高度 
        * [Globe#pick](https://cesium.com/learn/cesiumjs/ref-doc/Globe.html#pick) 获取射线与地面交点
    ```js
        viewer.terrainProvider // 获取视图对应的地形（唯一）
    ```
3. [Camera](https://cesium.com/learn/cesiumjs/ref-doc/Camera.html) 相机
    * [flyTo](https://cesium.com/learn/cesiumjs/ref-doc/Camera.html#flyTo) 飞行到视点
    * [setView](https://cesium.com/learn/cesiumjs/ref-doc/Camera.html#setView) 设置相机视点
    * [lookAt](https://cesium.com/learn/cesiumjs/ref-doc/Camera.html#lookAt) 相机看向目标位置
    * [lookAtTransform](https://cesium.com/learn/cesiumjs/ref-doc/Camera.html#lookAtTransform) 通过旋转矩阵设置看向目标
    * [Viewer#zoomTo](https://cesium.com/learn/cesiumjs/ref-doc/Viewer.html#zoomTo) 视图缩放至匹配位置
    * 沿路径漫游，flyTo函数和Callback组合实现
    * 绕点飞行，lookAt函数和Clock组合实现

4. [Entity](https://cesium.com/learn/cesiumjs/ref-doc/Entity.html) 实例 </br> 可以直接绑定CallbackProperty做动态及交互式功能比较友好
    * 点状
        * [PointGraphics](https://cesium.com/learn/cesiumjs/ref-doc/PointGraphics.html) 点
        * [BillboardGraphics](https://cesium.com/learn/cesiumjs/ref-doc/BillboardGraphics.html) 标牌
        * [LabelGraphics](https://cesium.com/learn/cesiumjs/ref-doc/LabelGraphics.html) 标签
    * 线状
        * [PolylineGraphics](https://cesium.com/learn/cesiumjs/ref-doc/PolylineGraphics.html) 折线
    * 面状
        * [PlaneGraphics](https://cesium.com/learn/cesiumjs/ref-doc/PlaneGraphics.html) 平面
        * [RectangleGraphics](https://cesium.com/learn/cesiumjs/ref-doc/RectangleGraphics.html) 长方形面 
        * [PolygonGraphics](https://cesium.com/learn/cesiumjs/ref-doc/PolygonGraphics.html) 多边形面
        * [EllipseGraphics](https://cesium.com/learn/cesiumjs/ref-doc/EllipseGraphics.html) 椭圆面
        * [WallGraphics](https://cesium.com/learn/cesiumjs/ref-doc/WallGraphics.html) 垂直连接面
    
    * 体状
        * [BoxGraphics](https://cesium.com/learn/cesiumjs/ref-doc/BoxGraphics.html) 盒体
        * [CylinderGraphics](https://cesium.com/learn/cesiumjs/ref-doc/CylinderGraphics.html) 锥柱体
        * [PolylineVolumeGraphics](https://cesium.com/learn/cesiumjs/ref-doc/PolylineVolumeGraphics.html) 沿线扫掠体
        * [PolygonGraphics Extruded](https://cesium.com/learn/cesiumjs/ref-doc/PolygonGraphics.html#extrudedHeight) 多边形拉伸体
        * [EllipseGraphics Extruded](https://cesium.com/learn/cesiumjs/ref-doc/EllipseGraphics.html#extrudedHeight) 椭圆面拉伸体
        
    * 模型（较少使用，通常使用Primitive来加载模型）
        * [ModelGraphics](https://cesium.com/learn/cesiumjs/ref-doc/ModelGraphics.html) glTF模型
        * [Cesium3DTilesetGraphics](https://cesium.com/learn/cesiumjs/ref-doc/Cesium3DTilesetGraphics.html) 3DTiles模型(基于glTF的封装)

    * [EntityCollection](https://cesium.com/learn/cesiumjs/ref-doc/EntityCollection.html) 实例集合
    ```js
        viewer.entities // 获取视图对应的实例集合
    ```
5. [Primitive](https://cesium.com/learn/cesiumjs/ref-doc/Primitive.html) 图元 </br> 与Entity相比，Primitive更加底层，可以实现的效果更丰富
    * 模型（通常使用Primitive来加载模型）
        * [Model](https://cesium.com/learn/cesiumjs/ref-doc/Model.htmL) glTF模型
        * [Cesium3DTileset](https://cesium.com/learn/cesiumjs/ref-doc/Cesium3DTileset.html) 3DTiles模型
            * [modelMatrix](https://cesium.com/learn/cesiumjs/ref-doc/Cesium3DTileset.html?#modelMatrix) [Tile#transform](https://cesium.com/learn/cesiumjs/ref-doc/Cesium3DTile.html?#transform) 位姿调整
            * [Cesium3DTileFeature](https://cesium.com/learn/cesiumjs/ref-doc/Cesium3DTileFeature.html) 属性查询
            * [Cesium3DTileStyle](https://cesium.com/learn/cesiumjs/ref-doc/Cesium3DTileStyle.html) 显示样式
            * [clippingPlanes](https://cesium.com/learn/cesiumjs/ref-doc/Cesium3DTileset.html?#clippingPlanes) 模型剖切
    * [PrimitiveCollection](https://cesium.com/learn/cesiumjs/ref-doc/PrimitiveCollection.html) 图元集合
    ```js
        viewer.primitives // 获取视图对应的图元集合
    ```

6. [CallbackProperty](https://cesium.com/learn/cesiumjs/ref-doc/CallbackProperty.html) 回调属性
    * 使用回调属性可以实现很多动态效果及功能
        * 动态标绘
        * 动态剖切
        * 实时交互
        * ......

7. [ScreenSpaceEventHandler](https://cesium.com/learn/cesiumjs/ref-doc/ScreenSpaceEventHandler.html) 交互事件
    * [ScreenSpaceEventType](https://cesium.com/learn/cesiumjs/ref-doc/global.html?#ScreenSpaceEventType)交互事件类型
    ``` js
    const handler = new Cesium.ScreenSpaceEventHandler(viewer.scene.canvas);
    handler.setInputAction((movement) => {
        ...
    }, Cesium.ScreenSpaceEventType.MOUSE_MOVE)
    ```

## 3. 后端开发

1. 为什么需要后端服务？
    * 响应前端的个性化请求
    * 存储动态数据

2. 后端服务和Apache/Nginx的区别
    * 服务是定制化的，可以根据请求动态返回数据，Apache等软件则是静态的服务器容器，其提供静态文件的挂载传输功能，但是本身不具备动态响应能力（可以通过一些插件的形式扩展）

### 3.1 后端开发-cpp

### 3.2 后端开发-node

1. 使用node.js + express框架快速搭建服务
    ```js
    const express = require("express")
    const path = require("path")
    const app = express();

    app.listen(8088, () => {
        console.log("App listening at port 8088\n http://localhost:8088 ")
    })
    ```
2. 监听网络请求
    ``` js
    // 监听GET请求
    app.get('path', (request，response) => {
        ...
    });
    // 监听POST请求
    app.post('path', (request，response) => {
        ...
    });
    ```
3. 设置静态挂载目录
    ``` js
    app.use(express.static(path.join(__dirname, '')));
    ```

### 3.3 后端开发-python

## 4. 桌面端开发

### 4.1 桌面端开发 qt-cpp

### 4.2 桌面端开发 qt-python

### 4.3 桌面端开发 electron-node

## 5. 移动端开发

### 5.1 移动端开发 vant-cordova

