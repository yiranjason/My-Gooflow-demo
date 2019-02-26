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
| :-- | :-- | :--: |
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
|toolBtns|['start',<br>'end',<br>'fork',<br>'join',<br>'complex',<br>'node',<br>'task',<br>'chat',<br>'state',<br>'plug']|左侧工具栏按钮(根据数组出现顺序的不同，还可以进行自定义排序)|