---
title: h5移动开发01-2D/3D转化、动画
---

# H5移动Web开发01

### 一.2D转化

##### 1.介绍及2D坐标系

- 2D：使元素旋转缩放等，页面表现丰富，配合动画做效果
- 坐标系
    - 2D：direction方向
        - X正方向：水平向右
        - Y正方向：垂直向下

##### 2.位移

1. 移动 translate 语法：
    1. 单个使用
        1. 固定的px值：正值，向右移动 
            1. `transform：translateX(100px);`
            2. `transform：translateY(100px);`
        2. 百分数:**相对于自身宽高**
            1. `transform: translateX(200%);`
            2. `transform: translateY(100%);`
    2. 合起来写
        1. `ransform: translate(100px, 100px);`
        2. `transform: translate(-100px, -100px);`
        3. `transform: translate(-50%, -50%);`
        4. `transform: translate(50px, 100%);`
2. 与定位区别:
    1. 定位会脱标,可能会影响其他盒子的布局,translate不会影响(微调一个盒子的位置)
    2. 定位会使行内元素变为块级元素,translate完全不对行内元素生效
3. ==居中方案==
    1. **语法：不用关心自身盒子宽高**

```css
/* 移动  不用关心盒子的本身的宽高  */
position: absolute;
/* 相对于父亲 宽高 */
top: 50%;
left: 50%;
/* 相对于自身 宽高 */
transform: translate(-50%, -50%);
```

##### 3.旋转

语法:单位是deg，正值顺时针

默认围绕中心点旋转

```css
transform: rotate(45deg);
```

##### 4.中心点

语法:可以影响旋转的效果:

```css
/* 具体PX值*/
transform-origin:100px 100px;
/* 百分数*/
transform-origin:50% 50%;
/* 方位名词*/
transform-origin:left bottom;

/* 单个参数，第二个值默认为50%*/
transform-origin:0;
```

##### 5.缩放

1. 语法

    ```css
    /* 长度、宽度方向 缩放 */
    transform:scale(2,3);
    
    /* 长度、宽度方向 缩放为同一个比例*/
    transform:scale(2);
    transform:scale(0.5);
    ```

    

2. 场景:鼠标悬浮,按钮放大

3. 特点:

    1. transform后面所有的属性都不会影响其它盒子的位置
    2. 缩放:使下面的文字,css属性,子元素都会跟着缩放

##### 6.综合语法

* 单独多次写，不生效，下面的会把上面的层叠掉；

```
transform: translate(x,y);
transform: rotate(90deg);
```

* 更为简洁地综合起来写2D相关的属性；

```css
/* 移动在旋转前面 */
transform: translate(x,y) rotate(90deg) scale(x,y);

/* 旋转在前面 */
transform: rotate(90deg) translate(x,y) scale(x,y);
```

* **使用顺序不同，出现的效果不同，因为旋转会改变初始轴向；**



### 二.伪元素

1. 什么是伪元素:页面html结构中没有元素,但是页面中缺真实存在

2. 常用:做小图标引用;字体图标引用,手动实现小图标

3. 特点:

    1. **content**属性不能丢  ---> content:'';
    2. 行内元素
    3. div::before:hover不能这样用；用法：div:hover::before
    4. **伪元素只能在双标签上使用**

    

### 三.动画

##### 1.定义

- 页面内实现一些列动画，可以循环播放，也可以播放几次；使丰富页面；
- 动画 animation 是CSS3中具有**颠覆性**的特征之一，可通过设置一个元素在多个时间节点上的不同样式来达到一个动画的效果；

##### 2.语法:1定义 2调用 3时间

```css
@keyframes 动画名称 {
	from {
		/* css code*/
	}
	to {
	
	}
}

div {
    /* 2.调用 */
    animation-name: dong_hua;
    /* 3.执行时间 duration 持续时间*/
    animation-duration: 2s;
}
```

状态里可以写2D转化，也可以写我们基础班学习的各种属性

##### 3.动画序列

语法:时间节点,可以更为精准的控制动画的多个状态节点,使得动画的变化更为丰富

```css
@keyframes name {
    /* 开始状态:*/
    0% {
    }
    
    50% {
    }
    75% {
    }
    83% {
       
    }
    /* 结束状态 */
    100% {
    }
}
```

注意:

1. 动画序列就是时间节点时的状态
2. n步变化就需要n+1个节点
3. **动画从开始执行到经过动画节点,都是基于上一个状态进行变化**

##### 4.属性

> 丰富我们的动画特性，能做更多的属性控制

| 属性                      | 描述                                                         |
| ------------------------- | ------------------------------------------------------------ |
| @keyframes                | 规定动画                                                     |
| animation                 | 所有动画属性的简写属性,除了animation-play-state属性          |
| animation-name            | 规定@keyframes动画的名称                                     |
| animation-duration        | 规定动画完成一个周期所花费的秒或者毫秒,默认是0               |
| animation-timing-function | 规定动画的速度曲线,默认是"ease" **linear :匀速**  **steps(n) 把上面的一大步，拆为n小步完成** |
| animation-delay           | 规定动画何时开始,默认是0                                     |
| animation-iteration-count | 规定动画被播放的次数,默认是1  **infinite: 无限次**           |
| animation-direction       | 规定动画是否在下一个周期逆向播放,默认是"normal"  alternate逆向播放 |
| animation-play-state      | 规定动画是否正在运行或者暂停,默认是"running"                 |
| animation-fill-mode       | 规定动画结束后状态,保持:forwards 回到起始:backwards          |

- animation-timing-function：动画 运动 速度曲线：速度快慢的体现；

```css
div{
    /* 匀速  */
    animation-timing-function: linear;

    /* 慢-快-慢  默认值  */
    animation-timing-function: ease;

    /* 慢-快  */
    animation-timing-function: ease-in;

    /* 快-慢  */
    animation-timing-function: ease-out;

    /* 慢-快-慢  */
    animation-timing-function: ease-in-out;
}
```

- animation-timing-function：steps(n)  分步 实现 老电影一帧一帧，整个动画分为几步骤完成

```css
/* 分步 实现 老电影一帧一帧，整个动画分为几步骤完成*/
animation-timing-function: steps(n);
```

- animation-delay：动画推迟多久执行；动画得等待。
- animation-iteration-count：播放循坏次数 1 2  infinite无限次 

```css
div{
    /* 指定次数设置  */
    animation-iteration-count: 2;

    /* 无限次数设置  */
    animation-iteration-count: infinite;
}
```

- animation-direction：循环方向：若0% 红色; 100% 黑色

```css
div{
    /*1 默认值 0-100 */
    animation-direction: normal;
    
    /*2 100-0 */
    animation-direction: reverse;
    
    /*3 0-100-0 */
    animation-direction: alternate;

    /*4 100-0-100 */
    animation-direction: alternate-reverse;
}
```

- animation-fill-mode：动画等待或者结束的状态设置；

```css
div{
    /*1 动画结束后，元素样式停留在 100% 的样式 */
    animation-fill-mode: forwards;
    
    /*2 在延迟等待的时间内，元素样式停留在 0% 的样式 
    动画结束的时候，回到div本身的样式（回到起始状态）
    */
    animation-fill-mode: backwards;
    
    /*3 同时设置了 forwards和backwards两个属性值
    在动画等待时间，样式为元素样式停留在 0% 的样式，
    动画结束时，元素样式停留在 100% 的样式
     */
    animation-fill-mode: both;
}
```

- animation-play-state：暂停和播放

```css
div{
    /*1 播放 */
    animation-play-state: running;
    /*2 暂停*/
    animation-play-state: paused;
}
```

- 设置 animation-direction ，需设置动画 多次 执行；
- 设置 animation-fill-mode，不能设置 无限 执行；

##### 5.简写

简写：动画名称 持续时间 速度曲线 等待时间 执行次数 执行的方向 动画等待或结束的状态

```css
animation: name duration timing-function delay iteration-count direction fill-mode;
```

- 组动画：需要用 逗号 隔开；

```css
animation: name_1 5s linear,name_2 2s linear;
```

- animation-play-state 没有在简写内

### 四.前缀

- 新特性，对各家浏览器更好的兼容，以便以后出了兼容问题，我们可以从这个方向想；

- -moz-：代表 firefox 浏览器私有属性
- -ms-：代表 ie 浏览器私有属性
- -webkit-：代表 safari、chrome 私有属性
- -o-：代表 Opera 私有属性

```css
-moz-border-radius: 10px; 
-webkit-border-radius: 10px; 
-o-border-radius: 10px; 
border-radius: 10px;
```

- 没有工程化工具，根据业务需要写这些前缀，解决样式的兼容；
- 有工程化工具，注意这些工具包的配置。webpack gulp

### 五.3D转化

##### 1.坐标系

在2D基础坐标上，增加一条垂直屏幕向外的一个轴线Z轴正向；

##### 2.位移

语法:

```css
div {
    /* 单独分开写 使用1*/
    transform: translateX(100px);
    transform: translateY(-100px);
    transform: translateY(100%);
    transform: translateZ(100px);
    
    /* 写在一起*/
    transform: translateX(100px) translateY(100px) translateZ(100px);

    /* 三个方向同时写的简写 使用2*/
    transform: translate3d(100px,100px,100px);
    
}
```

注意:

* XY 方向可以设置px值和%（因为有宽高）；
* **Z 轴只能设置 px，不能设置%（原因是盒子没有厚度）**

##### 3.视距

开启立体空间的第一步；设置与被观测的物体的距离，有距离才会有近大远小的效果

1. 语法:`perspective: 300px;`
2. 作用:近大远小的效果
3. 加在哪里
    1. body：以body的视角进行观测下面所有的子元素，形成统一的透视感
    2. 加在每个盒子的父亲上，即站在每个父亲的角度上进行观测，产生透视感
4. 值的大小：越小，变化越剧烈

##### 4.旋转

* 2D旋转：平面内；3D旋转：空间；效果更为丰富；

* 2D旋转：关键词 绕着，正方向是在屏幕内顺时针方向；现在看来，就是绕着Z轴的旋转；

语法:

```css
img:hover {
   transform: rotateX(45deg);
   transform: rotateY(45deg);
   transform: rotateZ(-45deg);
}
```

* 自定义轴向：（了解即可）

```css
img:hover {
    /* 1, 1, 0为空间向量坐标 x y z */
    transform: rotate3d(1, 1, 0, 45deg);
}
```

##### 5.3D呈现 transform-style

**子元素做3D转换，需在其父级上加transform-style属性，这样子元素做的3D转化才能为观测到**

语法:

```css
/* 设置在有子元素的父级上； */
/* 默认值：不开启*/
transform-style: flat;


/* 给子元素开启3D环境*/
transform-style: preserve-3d; 
```

与视距的差别

- 视距perspective：
    - **近大远小**，透视感
    - body(一般情况下)、各自父亲；观测角度不同
- 3D呈现：
    - **父亲给亲生子元素一个3D空间，子元素做3D转化可呈现出来**
    - **上下级的父亲上加；**（你要做什么事情，得经过你父母的同意）；可能会加多个地方

##### 6.缩放

语法:

```css
/* 宽 缩放 */
transform: scaleX(1);
/* 高 缩放 */
transform: scaleY(1);

/* 厚度 缩放？没有厚度 */
transform: scaleZ(1);

/* 宽，高 缩放一倍，厚度放大两倍 ,Z轴方向缩放没有效果*/
transform: scale3d(1,1,2)
```

* 特点：
    * 3D缩放，相对于自身宽高厚，Z轴缩放不生效，因为没有厚；
    * 下面子元素、文字、设置属性都会跟着缩放；

##### 7.简写

语法:

```css
transform: translateY() rotateX();
```

注意：旋转会改变轴向，会影响效果

### 六.总结

* 2D：
    * 移动：设置PX，百分数（自身的宽高）；**绝对的上下左右居中解决方案；**
    * 旋转：rotate(45deg)
    * 缩放：scale(2)，宽高方向都是使用同一个缩放比；
    * 简写：rotate(45deg) 写在移动前面，改变盒子初始化轴向；

* 动画：
    * 定义：@keyframes 动画名称 {}
    * 动画序列：时间节点，0%  100%；里面正常写CSS代码；
    * 属性重点：
        * timing-function：速度曲线，
            * linear，
            * steps() :遇到分帧图；
        * fill-mode：forwards 向前，动画结束的时候，停留在100%节点上；

```css
animation: name duration timing-function delay iteration-count direction fill-mode;

animation-play-state  没有写在简写里面，不常用；
```

* 3D：
    * 移动z轴方向：设置%没有效果，没有厚度；
    * 旋转：左手工具，把大拇指的朝向你自己眼睛，四个手指弯曲的方向就是顺时针方向；
    * 缩放Z轴方向：没有效果，没有厚度；
    * 视距：
        * 作用：近大远小的透视感；
        * 加给谁：
            * body：管理下面所有的子元素，形成统一的透视感。一般情况下加在body上；
            * 各自的父亲：管理父亲下面的所有的子元素，形成各自父亲单独的透视感觉；
        * 值的大小：越小，变化越为剧烈；
    * 3D呈现：
        * 作用：给亲生的子元素，开启3D空间，子元素做3D转化才能被观测到；
        * 加给谁：HTML结构上 上下级的父亲；