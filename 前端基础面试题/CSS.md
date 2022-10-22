### 一、CSS选择器及其优先级

#### 优先级：

!important>

内联样式>

id选择器（#xxx{}）>

类选择器(.xxx{})=属性选择器(div[id='1']{})=伪类选择器(li:last-child{})>

标签选择器(div{})=伪元素选择器(li::after{})>

相邻兄弟选择器(h1+p{})=子代选择器(ul>li{})=后代选择器(li a{})=通配符选择器(*{})

#### 总结:

1、如果优先级相同,则最后出现的样式生效

2、!important声明的样式优先级最高



### 二、行内元素和块级元素的区别

#### 常见的行内元素及其特点:

1、常见的行内元素:span、input、button、img、a(锚点)、b(粗体)...

2、设置宽高无效

3、可以设置水平的margin和padding属性,不能设置垂直方向的margin和padding

4、不会自动换行

#### 常见的块级元素及其特点：

1、常见的块级元素：div、h1~h6、table、ul、li、p、form...

2、可以设置宽高

3、margin和padding属性都可以生效

4、多个块级元素,默认从上到下排列

#### 相互转换

display:inline(行内元素)=====display:block(块级元素)=====display:inline-block(行内块元素)

行内块元素：1、可以设置宽高 2、margin和padding属性都有效  3、当宽度超出,会换行



### 三、display常用属性值及其用法

1、none:元素不显示,并且会从文档流中移除

2、block:块级元素类型,默认宽度为父级元素宽度,可设置宽高,换行显示

3、inline:行内元素类型,默认宽度为内容宽度,不可设置宽高,同行显示

4、inline-block:行内块元素类型,默认宽度为内容宽度,可以设置宽高,同行显示

5、inherit:规定从父级继承display属性值



### 四、CSS隐藏元素的方法

1、dispaly:none

​	(1)该元素不会在页面中占位置(从标准文档流中脱离)

​	(2)不会响应绑定的监听事件

2、visibility:hidden

​	(1)该元素会在页面中占位置

​	(2)不会响应绑定的监听事件

3、opacity:0

​	(1)该元素会在页面中占位置

​	(2)会响应绑定的监听事件

4、transform: scale(0)

​	(1)该元素会在页面中占位置

​	(2)不会响应绑定的监听事件

​	(3)块级元素或者行内块元素才能生效



### 五、display:none和visibility:hidden的区别

1、相同点:都可以设置元素隐藏不可见

2、不同点

​	(1)在渲染树中:display:none会让元素从渲染树中消失,不会占据任何空间

​								visibility:hidden不会让元素从渲染树中消失,会占据空间,只是内容不可见了

​	(2)在继承上: display:none是非继承属性,子孙节点随着父节点从渲染树中消失,通过修改子孙节点的属性也无法显示

​						 visibility:hidden是继承属性,子孙节点修改属性之后还是可以显示的

​	(3)修改常规文档流中的元素,display会造成文档重排,但是修改visibility只会造成元素重绘

### 



### 六、伪类选择器

##### 1、特点：

​	(1)将特殊的效果添加到特定的选择器上

​	(2)在已有的元素上添加样式的,不会产生新的元素

##### 2、分类

​	(1)结构伪类

- :root 匹配文档的根元素
- :empty 匹配没有子元素的元素,包括文本节点,但不包括注释
- :first-child 匹配一组兄弟元素中的第一个元素
- :last-child 匹配一组兄弟元素中的最后一个元素
- :last-of-type 匹配一组兄弟元素中的某种类型的最后一个 例如:有一堆div和a和img  他们其中的最后一个都被选中
- :only-child  匹配没有兄弟的元素,即该元素是另一个元素的唯一子元素,例如div中只有一个p标签,这时使用p:only-child
- :only-of-type 匹配没有相同类型的兄弟元素。例如class是.p,则.p:only-of-type会选择.p类名中只有一种的兄弟元素
- :nth-child() 会找出该元素的所有兄弟元素,然后按照位置匹配,下标就是从1开始的
- :nth-last-child() 会找出该元素的所有兄弟元素,然后按照位置匹配,如果匹配的数字对不上的话,css就失效了
- :nth-of-type() 和上面的相似但是需要匹配元素类型,就是选择出所有类型的元素,按照括号中的数字选择第几个
- :nth-last-of-type() 和上面类似,类推可得出

​	(2)链接伪类

- 未访问 :link         未点击之前的颜色
- 已访问 :visited  点击之后的颜色
- 激活 :active      就是鼠标按下未松开时的颜色
- 悬停 :hover      鼠标经过的颜色     和active冲突

​	(3)表单伪类 

- :enable和:disable 分别应用于启用和禁用的状态
- :checked应用于单选框或复选框的选择状态
- :require和:optional 应用于控件的必选和可选状态
- :valid和:invalid用于验证文本框中的数据是否有效,前则有效,后者无效
- :read-write和:read-only应用于文本框的读写和只读状态
- :in-range和:out-of-range应用于数值类型的文本框,依靠min和max两个属性之间判断

​	(4)其他伪类

- :target
- :not()
- :lang



### 七、伪元素选择器

##### 特点

(1)在特定选择器前后添加伪元素

(2)会产生新的元素 (例如before、after 仅部分)

##### 分类

(1)::before 在元素之前插入修饰的内容(行内元素)

(2)::after 在元素之后插入修饰的内容(行内元素)

(3)::first-letter 匹配块级元素内容的第一行的第一个首字符,如果加了::before也算在里面

(4)::first-line 匹配块级元素内容的第一行

(5)::placeholder 自定义表单控件占位符文本的样式

(6)::selection 选择的是选中的内容样式

##### 总结

伪元素和伪类的区别

​	伪类用冒号(:),伪元素用双冒号(::)

​	

### 八、说说position属性值具体有哪些

##### 分类

 (1)static

- 默认值,没有定位,元素出现在文档流中
- 会忽略top,bottom,left,right属性值

 (2)inherit

- 继承父元素的position属性值

 (3)fixed

- 生成绝对定位的元素
- 脱离文档流
- 指定元素相对于屏幕视图来指定位置

 (4)absolute

- 生成绝对定位的元素
- 脱离文档流
- 相对于父元素进行定位(父元素非static)如果父元素static则继续往上寻找非static,如果都没有则以html来定位

 (5)relative

- 生成相对定位的元素
- 不脱离文档流
- 相对于自身原来的位置进行定位



### 九、px、em、rem的区别

- px:固定像素
- em:相对于父级元素的font-size来设置的
- rem:相对于根元素的font-size来设置的
  - em,rem更适用于响应式布局



### 十、总结CSS中常见的布局单位

- vw: 相对于视图窗口的宽度,视图窗口的宽度100vw
- vh: 相对于视图窗口的高度,视图窗口的高度100vh

- vmin:vm和vh中较小值
- vmax:vm和vh中较大值
- 百分比:子元素的百分比是相对于父元素
  - vw/vh和百分比的区别:
    - vw/vh:相对于视图窗口
    - 百分比:百分比相对于父元素

### 十一、盒模型

- 盒模型由四个部分组成:margin、padding 、border、content
- box-sizing
  - content-box（标准盒模型）
    - 实际宽度=border\*2+padding\*2+content的宽度
    - 实际高度=border\*2+padding\*2+content的高度
  - border-box（怪异盒模型）
    - 实际宽度=设置的width
    - 实际高度=设置的height
    - content的宽度=width-padding\*2-border\*2
    - content的高度=height-padding\*2-border\*2

### 十二、瀑布流

​		  .box{

​                 columns: 3;   //每一行几张图片

​                 column-gap:10px  //间隙

​                }

### 十三、了解BFC及其使用场景

- 什么是BFC?
  - 全称:块级格式化上下文
  - BFC是一个完全独立的空间,让空间里面的子元素不会影响到外面的布局
- 触发BFC的属性
  - display:inline-block/flex/table-cell
  - overflow:hidden
- BFC作用
  - (1)解决float布局脱离文档流,高度塌陷的问题
  - (2)解决margin塌陷问题
  - (3)解决多栏问题

###  十四、总结七种垂直水平居中的方法

##### 1、定位+cale(固定宽高)   

-    position: absolute;

     top:calc(50% - 50px);

     left:calc(50% - 50px)

- 注意！！！:减号两边都要有空格否则calc不生效

##### 2、定位+margin(固定宽高)

-   .box2 .inner{

     position: absolute;

     top: 50%;

     left: 50%;

     margin-top: -50px;

     margin-left: -50px;

    }

##### 3、定位+margin:auto(不定宽高)

-   .box3 .inner{

     position: absolute;

     margin: auto;

     left: 0;

     right: 0;

     top: 0;

     bottom: 0;

    }

- 注意!!!!使用margin:auto要把上下左右设置为0

##### 4、定位+transform(不定宽高)

-   .box4 .inner{

     position: absolute;

     left: 50%;

     top: 50%;

     transform: translate(-50%,-50%);

    }

##### 5、flex布局(不定宽高)

-   .box5{

     display: flex;

     align-items: center;

     justify-content:center;

    }

##### 6、gird布局(不定宽高)

-   .box6{

     display: grid;

     align-items: center;

     justify-content:center;

    }

##### 7、table-cell(不定宽高)

-   .box7{

     display: table-cell;

     text-align: center;

     vertical-align: middle;

    }

    .box7 .inner{

     display: inline-block;

    }

- 注意:table-cell只对行内块元素生效

### 十五、flex弹性布局

##### 1、定义

###### 1.1、容器

采用flex布局的元素,称为flex容器,简称容器

###### 1.2、项目

容器里面所有的子元素称为flex项目,简称项目

###### 1.3、主轴和交叉轴

容器默认存在两根轴:水平的主轴和垂直的交叉轴

##### 2、容器的属性

- flex-direction属性
  - 作用:决定主轴的方向
  - 分类:
    - row(默认值,主轴为水平方向,起点在左端)
    - row-reverse(主轴为水平方向,起点在右端)
    - column(主轴为垂直方向,起点在上方)
    - column-reverse(主轴为垂直方向,起点在下方)
- flex-wrap属性
  - 作用:决定一条轴线排不下该如何换行
  - 分类:
    - nowrap:默认值，不换行，会自适应在同一行
    - wrap:换行
    - wrap-reverse:换行，第一行在下方
- flex-flow属性
  - 作用：flex-direction和flex-wrap的结合，书写顺序不影响结果
  - flex-flow:row,wrap
- justify-content属性
  - 作用：定义项目在主轴上如何对齐
  - 分类:
    - flex-start:默认值,水平（交叉轴）方向左对齐
    - flex-end:水平方向右对齐
    - center:水平居中
    - space-between：水平方向两端对齐,项目之间的间隔都相等
    - space-around:水平方向每个项目两侧的间隔相等，所以项目之间的间隔比边框之间的间隔大一倍
- align-items属性
  - 作用:定义项目在交叉轴上如何对齐
  - 分类：
    - flex-start:起点对齐
    - flex-end:终点对齐
    - center:中间对齐
    - baseline:项目的第一行文字的基线对齐
    - stretch：默认值，如果项目未设置高度或者auto，将占满整个容器的高度
- align-content属性
  - 作用：定义了多根轴线的对齐方式，**如果项目只有一根轴线，该属性不起作用**
  - 分类：
    - flex-start:与交叉轴的起点对齐
    - flex-end:与交叉轴的终点对齐
    - center：与交叉轴的中点对齐
    - space-between:与交叉轴两端对齐，轴线之间的间隔平均分布
    - space-around:每根轴线两侧的间隔都相等，所以轴线之间的间隔与轴线与边框的间隔大一倍
    - strech:默认值，如果项目未设置高度或者auto，将占满整个交叉轴

##### 3、项目的属性

###### 	3.1、order属性

- 作用：定义了项目的排列顺序，数值越小，排列越靠前，默认为0

###### 	3.2、flex-grow属性

- 作用:定义了项目的放大比例，默认为0，如果存在剩余控件，也不放大，如果项目所有的flex-grow属性都为1,它们将等分剩余空间(有的话)

- 也可以通过flex-grow改变分配的比例

-   .son:last-child{

     flex-grow: 4;

    }

###### 	3.3、flex-shrink属性

- 作用:定义了项目的缩小比例，默认为1，如果空间不足，该项目将缩小(空间足够,此属性无效),如果所有项目的flex-shrink属性都为1，当空间不足时，都等比例缩小
- 设置为0则不缩小，等于设置为自私的元素;设置为2则缩小两倍，比别人更能贡献自己

###### 	3.4、flex-basis属性

- 作用:定义在分配多余空间之前，项目占据的主轴空间。浏览器根据这个属性，计算主轴是否有多余的空间，他的默认值是auto，即项目的本来大小
- flex-basis:200px 如果项目有多余空间，设置为200px 那么会放大到200的宽度

###### 	3.5、flex属性

- 定义:flex属性是flex-grow,flex-shrink和flex-basis的简写, 默认值为0 1 auto  后两个属性可选

###### 	3.6、align-self

- 允许单个项目由与其他项目不一样的对齐方式，可广覆盖align-items属性，默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch
- 选项
  - auto、flex-start、flex-end、center、baseline、stretch

### 十六、flex布局中的flex-grow和flex-shrink

flex布局中flex-grow和flex-shrink的详细计算公式，

flex-grow:有剩余空间，分配到的权重值，默认为0

flex-shrink:收缩系数，只是一个宽度变小的权重分量

列出box1和box2的计算过程公式

1、判断所有子元素总宽度和与容器宽度的大小

（1）子元素总宽度和<容器宽度

​		剩余空间宽度=400-200-50=150

​		box1分配的空间=150\*2/3=100

​		box2分配的空间=150\*1/3=50

​		box1实际宽度=box1分配到的空间+200=300

​		box2实际宽度=box2分配到的空间+50=100

2、子元素总宽度>容器宽度

​		溢出空间宽度=500-400=100

​		每个元素收缩的权重=flex-shrink*宽度

​		总权重:2\*200+2\*300=1000

​		box1的收缩值=100\*（2\*200/1000）  
