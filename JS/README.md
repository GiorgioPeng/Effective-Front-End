# JS优化

## 减少前端代码耦合
什么是代码耦合? --牵一发而动全身  

### JS代码耦合  
解决方法:  
    - 减少全局变量的使用  
    - 多使用传参的方式

解耦的意义:  
    - 减少debug难度(明确每个变量的更改处)

### JS/CSS/HTML耦合
解决方法:  
    - 少在JS里面更改样式属性, 尽量通过增删类来更改样式(滚轮/鼠标/键盘等事件除外)

解耦的意义:  
    - 减少debug难度(明确每个样式定义的位置)  
    - 增删类的时候, 可以通过子类选择器来较为方便的控制子类的样式(.parent1 .child/.parent2 .child)

### 减少重复代码
> 写代码原则: 低耦合,高内聚 

尽量确保一个模块只负责一个功能(单一职责原则)

__发现重复代码 -> 封装成一个函数 -> 封装成一个模块 -> 封装成一个插件__

极端:  
    - 拆分太细, 简单功能反而变得复杂  

什么时候进行拆分:  
    - 函数太大,功能太复杂  
    - 逻辑太过复杂  
    - 存在可能复用的情况

### 封装成一个类
当在复用的时候, 如果每个地方都存在自己一些个性化的数据/样式等, 可以考虑封装成一个类,通过使用私有变量等进行定制  
如: 有三个地方都需要使用进度条,每个进度条的颜色,长度都不相同.  
```javascript
function progress(container,color,length){
    this.container = container;
    this.color = color;
    this.length = length;
    // ...
}

```

### 使用[策略模式](https://www.runoob.com/design-pattern/strategy-pattern.html)
JS是面向函数编程的语言, 使用策略模式的自然性远超C++/JAVA等语言
```javascript
swith(behavior){
    case 'done':
        // do sth;
        break;
    case 'sleep':
        // do sth;
        break;
    default:
        break;
}
// 如果每增加一个条件, 需要对 swith/if-else 语句进行更改,可能需要改动逻辑
// 但是根据程序设计的开闭原则(对拓展开放,对修改封闭),使用策略模式可能会更好
var todo = {
    done:function(){
        // do sth
    },
    sleep:function(){
        // do sth
    }
    // 每次只需要增加函数就可以使用不同的行为
}
// 调用
if(todo[type]==='function'){
    todo[type]();
}

```

