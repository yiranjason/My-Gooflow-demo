# My-gooflowDemo

## Web流程图绘制

### [Gooflow.js](https://github.com/huangjunsen/GooFlow)

### [jsplumb.js](https://github.com/jsplumb/jsplumb) 

- 中文教程：https://github.com/wangduanduan/jsplumb-chinese-tutorial
- 官网demo： https://jsplumbtoolkit.com

### [KityMinder Editor](https://github.com/fex-team/kityminder-editor)

> 百度脑图中发现的，该demo来源于百度fex团队

#### 结合三种方式的相应比较，和入手简易性，固采用了gooflow.js进行

---

### [gooflow.js-jQuery版本API](https://gooflow.xyz/docs/)

> Step1: 引入相应的文件【Jquery\gooflow.min.js\gooflow.min.css】

> Step2: 绘制流程图的容器指定 <br>
    `<div id="demo"></div>`
    
> Step3: 激活生成 <br>
    `var demo1 = $("#demo").createGooFlow(options);`
    
##### Option | 参数配置

| 参数 | 默认值 | 描述 |
| :-- | :-- | :-- |
|id|""|作为流程图在页面中的唯一标识，必选。或者提供含有id属性的dom|
|MainContener|$('body')[0]|工作区的父级元素非position:absolute时，默认即可；<br>外围存在绝对定位的元素，则应该增加绝对定位容器的dom|
|width|'auto'|定义整个控件的宽(含工具栏和滚动条)，默认和父级容器同宽|
|height|500|定义整个控件的高(含顶部工具栏、滚动条)|
|initNum|1|计算默认元素名称后缀的起始编码Sequence|
|initLabelText|'newFlow_1'|初始化时标题的内容，仅当haveHead==true时有效|
|workWidth|null|定义画布的宽，如忽略，则根据width自动计算|
|workHeight|null|定义画布的高，规则同workWidth|
|haveHead|true|是否显示头部工具栏|
|headBtns|`['save','undo','redo','reload','expand','new']`|顶部栏的按钮从左至右依次都有哪些类型名的按钮，仅当haveHead==true时有效。按钮【除撤销和重做外】的点击事件需要自定义|
|headBtnRemarks|`['保存','撤销','重做','重置画布','扩大画布','清空画布']`|头部工具栏按钮提示文本|
|haveTool|true|是否显示左侧工具栏|
|toolBtns|`["task","node","chat","state","plug"]`|左侧工具栏按钮(根据数组出现顺序的不同，还可以进行自定义排序)|
|haveGroup|true|是否启用组织划分框编辑如为否, 则左侧工具栏的 group 工具将不出现, 但是已经画了的“组织划分框”还是会出现的|
|useOpenStack|true|是否启用回滚线|
|editable|true|是否可编辑, 仅在 haveTool=false 时有意义|

#### Event hook | 事件钩子

- 顶部栏按钮事件

> 当工具栏按钮被点击时触发的事件定义(虚函数)，只有初始化GooFlow实例时设置了顶部栏，这些事件钩子才存在。因为可直接用this访问GooFlow实例本身，无传参；用户可自行重定义。
另外，用户还可通过GooFlow实例内置的bindHeadBtnEvent接口，自行扩展另外自定义的头部按钮的点击事件。<br>
`instance.myEvent = function(){
        this;  //GooFlow实例本身
        //TODO: 事件响应的实现
};`

|事件|意义|
|:-|:-|
|onBtnNewClick|工具栏回调函数：新建流程图按钮被点中|
|onBtnOpenClick|工具栏回调函数：打开流程图按钮事件定义|
|onBtnSaveClick|工具栏回调函数：保存流程图按钮定义|
|onFreshClick|工具栏回调函数：重载流程图按钮定义|
|onExpandClick|工具栏回调函数：扩大画布按钮定义|
|onPrintClick()|打印机按钮事件定义|

- 流程图元素事件

> 节点/连线/分组泳道的一些操作事件，用户可自行重定义。这些事件可直接通过this访问GooFlow实例本身；并且这些事件触发的方法若返回false将阻止默认操作或事件发生。<br>
`instance.myEvent = function( args[] ){
    this;  //GooFlow实例本身
    //TODO: 事件响应的实现
    return bool; //根据实例情况返回false阻止默认事件，或者返回其它值让默认事件发生
};`

|事件及描述|传参|参数说明|
|:-|:-|:-|
|onItemAdd|`(id,type,json)`|**id**：元素唯一标识<br>**type**：'node'节点，'line'连线，'area'分组泳道|
