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
|MainContener|$('body')[0]||