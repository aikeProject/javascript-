#### javascript 动效

```
该文章一些知识，来源于《javascript网页动画设计》一书
可以直接去阅读该书

该书中使用的 velocity.js 2.0以下下的版本
```

[javascript网页动画设计](https://re.jd.com/search?keyword=javascript%E7%BD%91%E9%A1%B5%E5%8A%A8%E7%94%BB%E8%AE%BE%E8%AE%A1&enc=utf-8)


##### velocity 的使用

- 安装

- npm 安装

```
npm install velocity-animate@1.5.2
```

- 直接引用

- [velocity](https://github.com/julianshapiro/velocity)

```
注意`velocity.js 2.0` 
不要使用 github上这两个cdn引用有bug，到写这篇文章 `2019-8-16` 貌似都没有解决

问题：easing 缓动不生效
```

```
<script src="//cdn.jsdelivr.net/npm/velocity-animate@2.0/velocity.min.js"></script>
<script src="//cdn.jsdelivr.net/npm/velocity-animate@2.0/velocity.ui.min.js"></script>
```

- 获取 `velocity.js 1.5.2`

```
npm install velocity-animate@1.5.2

node_modules
    velocity-animate
        velocity.js
        velocity.ui.js

去 node_modules 里把文件拷贝到你想使用的地方
然后在浏览器里直接引用就行了
```

- 建议使用 `velocity.js 1.5.2` 版本，[官网](http://VelocityJS.org)文档全面
- `velocity.js 2`以上的版本，文档在[wiki](https://github.com/julianshapiro/velocity/wiki)里面，我感觉么不是很完善，而且2以上版本指不定有什么bug
- 本来学习《javascript网页动画设计》时，打算用`velocity.js` 2以上版本学习的，后来发现还是`velocity.js` 2以下版本好用


##### velocity.js 基础知识

```
结合JQuery使用
参数
属性
值
链式操作
选项
其它功能
```

##### 结合JQuery使用

```
var $move = $('#move');


$move.velocity({opacity: 0});
```

##### 不使用jQuery

```
var move = document.getElementById('move');

Velocity(move, {
    opacity: 0
});
```

##### 参数

参数1 是对象 css属性的期望值

参数2 是对象 指定动画选项

```


$move.velocity({width: 200, height: 200, opacity: 1}, {duration: 400, easing: 'swing'});
```

第二个参数不传对象

```
// 动画持续时间 1000 毫秒 默认缓动类型 'swing'
$move.velocity({width: 200, height: 200, opacity: 1}, 1000);

// 持续时间 1000 毫秒 缓动类型 'ease-in-out'
$move.velocity({top: 50}, 1000, 'ease-in-out');

// 默认持续时间 400 毫秒，缓动类型 'ease-out'
$move.velocity({left: 50}, 'ease-out');

// 动画执行完毕
$move.velocity({top: 0}, 200, function () {
    console.log('complete');
});
```

##### 属性

注意：将复合属性，拆分为他们的子属性

```
$move.velocity({padding: 50});

$move.velocity({paddingLeft: 50});
```

##### 值 

- 大多数默认单位`px`，rotateZ 这种css3 属性 默认单位`deg`

- v1 版本

```
$move.velocity({
    top: 50, // 默认 px
    left: '50%', // 手动指Z
    rotateZ: 25, // 默认 deg
}, 1000);
```

- v2 版本

```
$move.velocity({
    transform: ["rotateZ(150)", 'rotateZ(0)']
}, 1000);
```

- 注意：

```
对比velocity v1 v2 版本，对于css3 
属性 rotate scale translate 使用已经发生了变化
```

##### 链式调用

```
$move
    .velocity({width: 200})
    .velocity({height: 200});
```

##### easing 缓动效果

- 三角函数缓动 (https://easings.net/)[https://easings.net/]

```
$move.velocity({width: 200}, 'easeInOutSine');

// 我看了一下，它源码里打包的效果有缓动函数有这些

["ease", [0.25, 0.1, 0.25, 1.0]],
["ease-in", [0.42, 0.0, 1.00, 1.0]],
["ease-out", [0.00, 0.0, 0.58, 1.0]],
["ease-in-out", [0.42, 0.0, 0.58, 1.0]],
["easeInSine", [0.47, 0, 0.745, 0.715]],
["easeOutSine", [0.39, 0.575, 0.565, 1]],
["easeInOutSine", [0.445, 0.05, 0.55, 0.95]],
["easeInQuad", [0.55, 0.085, 0.68, 0.53]],
["easeOutQuad", [0.25, 0.46, 0.45, 0.94]],
["easeInOutQuad", [0.455, 0.03, 0.515, 0.955]],
["easeInCubic", [0.55, 0.055, 0.675, 0.19]],
["easeOutCubic", [0.215, 0.61, 0.355, 1]],
["easeInOutCubic", [0.645, 0.045, 0.355, 1]],
["easeInQuart", [0.895, 0.03, 0.685, 0.22]],
["easeOutQuart", [0.165, 0.84, 0.44, 1]],
["easeInOutQuart", [0.77, 0, 0.175, 1]],
["easeInQuint", [0.755, 0.05, 0.855, 0.06]],
["easeOutQuint", [0.23, 1, 0.32, 1]],
["easeInOutQuint", [0.86, 0, 0.07, 1]],
["easeInExpo", [0.95, 0.05, 0.795, 0.035]],
["easeOutExpo", [0.19, 1, 0.22, 1]],
["easeInOutExpo", [1, 0, 0, 1]],
["easeInCirc", [0.6, 0.04, 0.98, 0.335]],
["easeOutCirc", [0.075, 0.82, 0.165, 1]],
["easeInOutCirc", [0.785, 0.135, 0.15, 0.86]]
```

- css 缓动

```
$move.velocity({left: 500}, 'ease');

$move1.velocity({left: 500}, 'ease-in-out');
```

- 贝塞尔曲线缓动 [https://cubic-bezier.com/](https://cubic-bezier.com/)

```
$move.velocity({left: 500}, 500, [0.17, 0.67, 0.83, 0.67]);

$move1.velocity({left: 500}, 500, [.42, 0, .58, 1]);
```

- 弹簧物理 [张力，摩擦力]

```
[张力, 摩擦力]

张力越大 速度和弹动幅度越大
摩擦力越小 弹动速度越快

亲自试试 感受更明显

$move.velocity({left: 500}, 1000, [250, 20]);

$move1.velocity({left: 500}, 1000, [500, 25]);
```


#### 参数选项

##### `begin` 开始 `complete` 完成

```
$move.velocity({left: 500}, {
    easing: [250, 15],
    duration: 1000,
    begin: function () {
        console.log('--- 动画开始 ---')
    },
    complete: function () {
        console.log('--- 动画结束 ---')
    }
});
```

##### `loop` 循环

```
    // 循环两次
    $move.velocity({left: 500}, {
        easing: [250, 15],
        duration: 1000,
        loop: 2
    });
    
    // 无限循环
    $move.velocity({left: 500}, {
        easing: [250, 15],
        duration: 1000,
        loop: true
    });
```

##### delay 延迟

```
$move.velocity({left: 500}, {
    easing: [250, 15],
    duration: 1000,
    delay: 500,
});
```

##### `display`（显示）和 `visibility`（可见性）

```
    // display
    $move.velocity({left: 500}, {
        easing: [250, 15],
        duration: 1000,
        display: 'none'
    });

    // hidden
    $move.velocity({left: 500}, {
        easing: [250, 15],
        duration: 1000,
        visibility: 'hidden'
    });
```


#### 其它功能

##### `scrolling` 滚动

- 相对于浏览器滚动，让浏览器滚动到元素所在位置

```
css

    #move2 {
            width: 100px;
            height: 100px;
            background: red;
            border-radius: 50%;
            position: absolute;
            padding: 0;
            text-align: center;
            top: 2000px;
        }

html

    <div id="move2">3</div>

js

    $('#move2').velocity('scroll', {
        duration: 1000,
        easing: 'spring'
    });
```

- 相对于父级元素滚动

滚动到距离顶部200px的位置

```
$move.velocity('scroll', {
    container: $move,
    duration: 1000,
    offset: "200px"
});
```

- 默认是`y`轴方向滚动，可设置为`x`轴方向滚动

```
$('#move2').velocity('scroll', {
    duration: 1000,
    easing: 'spring',
    axis: 'x'
});
```

##### `color`颜色

```
$element.velocity({
    // 背景颜色变动
    backgroundColor: "#000",
    // 透明度变动
    backgroudColorAlpha: .5,
    // 文字透明度
    colorAlpha: 0.85,
    // 文字颜色
    color: "#ff0000",
})
```

##### `transform` 变换

```
$element.velocity({
    // x 轴移动
    translateX: "200px",
    // y 轴移动
    translateY: "200px",
    // z 轴移动
    translateZ: "200px",
    // x 轴旋转
    rotateX: "45deg",
    // y 轴旋转
    rotateY: "45deg",
    // z 轴旋转
    rotateZ: "45deg",
    // 缩放
    scaleX: 1,
    scaleY: 1
});
```


#### 动画工作流

##### 淡入效果

```
    var fadeIn = {
        // 属性
        p: {
            opacity: 1,
            top: '50px'
        },
        // 选项
        o: {
            duration: 1000,
            easing: 'linear'
        }
    };
    
    // 淡入
    $move.velocity(fadeIn.p, fadeIn.o);
```

##### 对不同元素设置动画

- 一般做法

```
// 一般做法，通过嵌套回调的方式

    $move.velocity({
        translateX: "200px",
    }, function () {
        $move1.velocity({
            translateX: "200px",
        }, function () {

        });
    });
```

- 优化做法

```
组织排序动画
需要 ui pack 插件支持，velocity.ui.js 
```

- [ velocity.ui.js](http://velocityjs.org/#uiPack)

```
    $.Velocity.RunSequence([
        {
            elements: $move,
            properties: {
                translateX: 500
            },
            options: {duration: 1000}
        },
        {
            elements: $move1,
            properties: {
                translateX: 500
            },
            options: {duration: 1000}
        }
    ]);
```

##### 打包效果

```
// 名称后缀
// In结尾 自动淡入 （opacity 0 -> 1）
// Out结尾 动画结束后，将元素display设置为none

    $.Velocity.RegisterEffect('shadowIn', {
        defaultDuration: 1000,
        calls: [
            [{opacity: 1, scale: 1}, 0.4],
            [{boxShadowBlur: 50}, .6]
        ]
    }).RegisterEffect('shadowOut', {
        defaultDuration: 1000,
        calls: [
            [{boxShadowBlur: 50}, .8],
            [{opacity: 0, scale: 0}, 0.8],
        ],
        reset: {
            opacity: 1
        }
    });

    $move.velocity('shadowIn');
    $move.velocity('shadowOut');
```


#### `velocityjs`动效设计插件 [vmd](http://velocityjs.org/#vmd) 的使用

```
在 body 元素最后引入，其实就是需要等dom元素加在完毕引入
<script src="https://julian.com/research/velocity/vmd.min.js"></script>
```

#### 使用介绍

- [官方视频](https://www.youtube.com/watch?v=7IxhIMIdkPs&hd=1) 翻墙你懂的，基本看一遍就知道这个插件怎么用了
- 我看后觉得需要注意的是

![](https://user-gold-cdn.xitu.io/2019/8/19/16ca7bf3807f4410?w=1558&h=806&f=jpeg&s=249980)

```
双击出现一个面板，可以输入css属性
a-z 执行动画
1 开始全部动画
2 重置全部动画
```

- 其中需要注意的是如何在控制台输出动画代码

```
双击图中黑色部分，就可以看到控制台输出了代码
```


![](https://user-gold-cdn.xitu.io/2019/8/19/16ca7c3565b092be?w=2612&h=950&f=jpeg&s=190554)

- 插件包含`velocity.js`、`velocity.ui.js`、`Jquery.js` 无需重复引入
- 插件蛮简单的，引入在页面中尝试一下，马上就会了


#### 文本动画

##### `jquery.blast.js`的使用

```
为制作文本动画做准备

blast.js 可以方便的将文本拆成字符、单词和句子
```
- 按字符分割 `character`

```
    <div>
        Hello Wold
    </div>
     
    $('div').blast({delimiter: 'character'});
    
    输出：
    
    <div aria-label="Hello world" class="blast-root">
        <span class="blast" aria-hidden="true">H</span>
        <span class="blast" aria-hidden="true">e</span>
        <span class="blast" aria-hidden="true">l</span>
        <span class="blast" aria-hidden="true">l</span>
        <span class="blast" aria-hidden="true">o</span>
        <span class="blast" aria-hidden="true">w</span>
        <span class="blast" aria-hidden="true">o</span>
        <span class="blast" aria-hidden="true">r</span>
        <span class="blast" aria-hidden="true">l</span>
        <span class="blast" aria-hidden="true">d</span>
    </div>
```

- 按单词分割 `word`

```
<div>
     Hello Wold
</div>
    
$('div').blast({delimiter: 'word'});

<div aria-label="Hello world" class="blast-root" style="">
    <span class="blast" aria-hidden="true" style="">Hello</span>
    <span class="blast" aria-hidden="true" style="">world</span>
</div>
```

- 按句子进行分割 `sentence`

```
<div>
    Blast.js separates text in order to facilitate typographic manipulation. It has four delimiters built in: character,
    word, sentence, and element. Alternatively, Blast can match custom regular expressions and phrases.
</div>

$('div').blast({delimiter: 'sentence'});

<div aria-label="Blast.js separates text in order to facilitate typographic manipulation. It has four delimiters built in: character,word, sentence, and element. Alternatively, Blast can match custom regular expressions and phrases." class="blast-root" style="">
    <span class="blast" aria-hidden="true">Blast.js separates text in order to facilitate typographic manipulation.</span>
    <span class="blast" aria-hidden="true">It has four delimiters built in: character,word, sentence, and element.</span>
    <span class="blast" aria-hidden="true" style="">Alternatively, Blast can match custom regular expressions and phrases.</span>
</div>
```

- `customClass` (自定义类)

```
$('div').blast({
    delimiter: 'word',
    customClass: 'my-class'
});

<div aria-label="Hello Wold" class="blast-root">
    <span class="blast my-class" aria-hidden="true">Hello</span>
    <span class="blast my-class" aria-hidden="true">Wold</span>
</div>
```

- `generateValueClass` (生成值类)

```
是否添加一个特有的类 （.blast-[delimiter]-[textValue]）
仅支持 character word
```

```
$('div').blast({
    delimiter: 'word',
    generateValueClass: true
});

<div aria-label="Hello Wold" class="blast-root">
    <span class="blast blast-word-hello" aria-hidden="true">Hello</span>
    <span class="blast blast-word-wold" aria-hidden="true">Wold</span>
</div>
```

- `tag` 标签，指定包裹文本元素的标签

```
用div包裹文本元素

$('div').blast({
    delimiter: 'word',
    tag: 'div'
});


<div aria-label="Hello Wold" class="blast-root">
    <div class="blast" aria-hidden="true">Hello</div>
    <div class="blast" aria-hidden="true">Wold</div>
</div>
```

- `reverse` (反转)，还原为原始的文本

```
$('div').blast({
    delimiter: 'word',
});

setTimeout(function () {
    $('div').blast(false);
}, 2000);
```


##### 让文本过度进入视图或离开视图

- 替换已有文本

```
$('div')
    .html('This is our new message.')
    .blast({
        delimiter: 'word'
    })
    .css({opacity: 0})
    .velocity({opacity: 1}, {duration: 2000});
```

- 错开动画

```
$('div')
    .html('This is our new message.')
    .blast({
        delimiter: 'word'
    })
    .css({opacity: 0})
    .velocity('transition.fadeIn', {stagger: 500});
```

- 过度文本离开视图

```
$('div').blast({delimiter: 'word'});

$('div .blast').velocity(
    'transition.fadeOut',
    {
        stagger: 50,
        backwards: true,
        complete: function () {
            $('div')
                .html('This is our new message.')
                .blast({
                    delimiter: 'word'
                })
                .css({opacity: 0})
                .velocity('transition.fadeIn', {stagger: 50});
            }
        }
    );
```

- 华丽过度文本

```
对于有些3D变换，这些效果不能用于css中display为"inline"的元素
所以在动画之前，先将元素 display 设置为 'inline-block'
```

```
$('div').blast({delimiter: 'word'});

$('div .blast')
    .css({display: 'inline-block'})
    .velocity(
        'transition.perspectiveDownOut',
        {
            stagger: 50,
            // 反转元素集合，让动画元素后面的先执行，看到效果你就懂了
            backwards: true,
            complete: function () {
                $('div')
                    .html('This is our new message.')
                    .blast({delimiter: 'word'})
                    .css({opacity: 0, display: 'inline-block'})
                    .velocity('transition.perspectiveDownIn', {stagger: 50});
            }
        }
);
```



#### 链接

- [（一）javascript 动效](https://juejin.im/post/5d562bd76fb9a06b0202bda4)
- [（二）javascript 动效](https://juejin.im/post/5d564d756fb9a06b30703d3c)
- [（三）javascript 动效](https://juejin.im/post/5d5a08556fb9a06afb61c93b)
- [（四）javascript 动效](https://juejin.im/post/5d5a0a4fe51d453b7403f989)
- [（五）javascript 动效](https://juejin.im/post/5d5ca8dbf265da03de3b05cd)