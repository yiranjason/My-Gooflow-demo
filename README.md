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
|**onItemAdd**@当某个元素（节点/连线/分组泳道）被添加时，触发的方法 |`(id,type,json)`| **id**：元素唯一标识<br>**type**：'node'节点，'line'连线，'area'分组泳道<br>**json**：描述元素的相应结构数据|
|**onItemDel**@当某个元素（节点/连线/分组泳道）被删除时，触发的方法 |`(id,type)`| **id**：元素唯一标识<br>**type**：'node'节点，'line连线'，'area'分组泳道|
|**onItemMove**@当某个元素（节点/分组泳道）被移动至新位置时，触发的方法|`(id,type,left,top)`|**id**：元素唯一标识<br>**type**：'node'节点，'area'分组泳道<br>**left**：元素在新位置上相对于工作区的左边距，单位像素<br>**top**：元素在新位置上相对于工作区的上边距，单位像素|
|**onItemRename**@当某个元素（节点/连线/分组泳道）被重命名时，触发的方法|`(id,name,type)`|**id**：元素唯一标识<br>**name**：元素的新名称<br>**type**：'node'节点，'line'连线，'area'分组泳道|
|**onItemFocus**@当操作某个元素（节点/连线）被由不选中变成选中时，触发的方法|`(id,type)`|**id**：元素唯一标识<br>**type**：'node'节点，'line'连线|
|**onItemBlur**@当操作某个元素（节点/连线）被由选中变成不选中时，触发的方法|`(id,type)`|**id**：元素唯一标识<br>**type**：'node'节点，'line'连线|
|**onItemResize**@当某个元素（节点/分组泳道）被重定义大小或造型时，触发的方法|`(id,type,width,height)`|**id**：元素唯一标识<br>**name**：元素的新名称<br>**type**：'node'节点，'line'连线，'area'分组泳道<br>**width**：元素的新宽度<br>**height**：元素的新高度|
|**onItemMark**@当用醒目颜色标注某个元素（节点/连线）时触发的方法|`(id,type,mark)`|**id**：元素唯一标识<br>**type**：'node'节点，'line'连线|
|**onLineMove**@当移动某条折线中段的位置时，触发的方法|`(id,M)`|**id**：元素唯一标识<br>**M**：折线中段的新X坐标（当type='lr'时）或者新y坐标（当type='tb'时），单位像素|
|**onLineSetType**@当变换某条连线的类型时，触发的方法|`(id,type)`|**id**：元素唯一标识<br>**type**：连线的新类型，有三种：'sl'直线；'lr'中段可左右移动的折线'；'tb'中段可上下移动的折线有直线|

#### Method interface | 方法接口

|方法|示例|描述|
|:-|:-|:-|
|createGooFlow|`var demo = $("selector").createGooFlow(options);`|所有方法的基础，此方法返回一个 GooFlow 对象如果需要用到下面的方法，则必须初始化一个用于存储该对象的变量|