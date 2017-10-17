# React 基础知识介绍

## hello world

以下是一个最简单的demo，将一个最简单的组件渲染到页面上。

```jsx
import React from 'react'
import { render } from 'react-dom'

// 定义组件
class Hello extends React.Component {
    render() {
        // return 里面写jsx语法
        return (
            <p>hello world</p>
        )
    }
}

// 渲染组件到页面
render(
    <Hello/>,
    document.getElementById('root')
)
```

## jsx 语法

### 使用一个父节点包裹

```jsx
// 三个 <p> 外面必须再包裹一层 <div>
return (
  <div>
    <p>段落1</p>
    <p>段落2</p>
    <p>段落3</p>
  </div>
)
```

```jsx
// { } 中返回的两个 <p> 也要用 <div> 包裹
return (
  <div>
    <p>段落1</p>
    {
      true 
      ? <p>true</p>
      : <div>
        <p>false 1</p>
        <p>false 2</p>
      </div>
    }
  </div>
)
```

### 注释

```jsx
    return (
        // jsx 外面的注释
        <div>
            {/* jsx 里面的注释 */}
            <p>hello world</p>
        </div>
    )
```

### 样式

对应 html 的两种形式，jsx 的样式可以这样写：
css样式：`<p className="class1">hello world</p>`，注意这里是`className`，而 html 中是`class`
内联样式：`<p style={{display: 'block', fontSize: '20px'}}>hello world</p>`，注意这里的`{{...}}`，还有`fontSize`的驼峰式写法

### 事件

```jsx
class Hello extends React.Component {
    render() {
        return (
            <p onClick={this.clickHandler.bind(this)}>hello world</p>
        )
    }

    clickHandler(e) {
        // e 即js中的事件对象，例如 e.preventDefault()
        // 函数执行时 this 即组件本身，因为上面的 .bind(this)
        console.log(Date.now())
    }
}
```

### 循环

```jsx
class Hello extends React.Component {
    render() {
        const arr = ['a', 'b', 'c']
        return (
            <div>
                {arr.map((item, index) => {
                    return <p key={index}>this is {item}</p>
                })}
            </div>
        )
    }
}
```

### 判断

```jsx
return (
  <div>
    <p>段落1</p>
    {
      true 
      ? <p>true</p>
      : <p>false</p>
      </div>
    }
  </div>
)
```

也可以这样使用：

`<p style={{display: true ? 'block' ? 'none'}}>hello world</p>`


## 代码分离

### page 层

containers文件夹下

### subpage 层

某个containers文件夹下的文件夹

### component 层

components文件夹下，多个页面公用的模块


## 数据传递 & 数据变化

### props

父组件给子组件传递数据

### state

组件内部自身的属性

## 智能组件 & 木偶组件

containers和components文件夹下的组件

## 生命周期

- **`getInitialState`**

初始化组件 state 数据，但是在 es6 的语法中，我们可以使用以下书写方式代替

```jsx
class Hello extends React.Component {
    constructor(props, context) {
        super(props, context);
        // 初始化组件 state 数据
        this.state = {
            now: Date.now()
        }
    }
}
```

- **`render`**

最常用的hook，返回组件要渲染的模板。

- **`comopentDidMount`**

组件第一次加载时渲染完成的事件，一般在此获取网络数据。实际开始项目开发时，会经常用到。

- **`shouldComponentUpdate`**

主要用于性能优化，React 的性能优化也是一个很重要的话题，后面一并讲解。

- **`componentDidUpdate`**

组件更新了之后触发的事件，一般用于清空并更新数据。实际开始项目开发时，会经常用到。

- **`componentWillUnmount`**

组件在销毁之前触发的事件，一般用户存储一些特殊信息，以及清理`setTimeout`事件等。