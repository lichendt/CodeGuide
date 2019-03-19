
## <h2 id="react">react核心代码规范及要求</h2>

### <h3 id="react-requirements">一、基本原则（Basic Rules）</h3>

1. 语法上根据生命周期方法执行的顺序编写代码

   （1 生命周期方法［`getDefaultProps`, `getInitialState`, `componentWillMount`, `componentDidMount`,`componentWillReceiveProps`, `shouldComponentUpdate`, `componentWillUpdate`, `componentDidUpdate`,`componentWillUnmount］`

   （2 其他的私有方法

   （3 render()方法

2. 事件处理函数的命名: “handle+EventName”

3. 组件验证

react 组件都应该完成 `propTypes` 验证。每一个 `this.props` 的属性都应该有一个与之对应的`propTypes`。

避免使用这些没有描述意义的 prop-types:

- React.PropTypes.any

- React.PropTypes.array

- React.PropTypes.object

最好使用：

- React.PropTypes.arrayOf

- React.PropTypes.objectOf

- React.PropTypes.instanceOf

- React.PropTypes.shape

4、能用 `props` 就不要用 `state`，这一定程度上可以减少应用程序的复杂度

5、尽量少用jQuery去操作DOM（有必要的话，把jquery插件包装在React组件中）

6、尽量不用例如backbone的模型，可以直接使用 `flux action`，或者 `$.ajax` 来代替。

7、每个文件中只包含一个 React 组件。

8、尽可能地使用JSX语法。

9、除非不用JSX语法创建一个应用，否则不要使用`React.createElement`方法。

### <h3 id="react-base-guide">二、基础规范</h3>

1. 统一全部采用 Es6  

2. 每个文件只包含的一个 React 组件（联系紧密的组件可以使用「命名空间的形式」）。  

3. 始终使用 JSX 语法，不要使用 `React.createElement` 创建 ReactElement，以提高编写速度、可读性、可维护性（没有 JSX 转换的特殊场景例外，如在 `console` 中测试组件）。  

### <h3 id="react-naming-rule">三、命名规范</h3>

- **扩展名**：使用 .js 作为 React 组件的扩展名；  
- **文件名**：使用大驼峰，如 MyComponent.js；  
- **组件命名**：组件名称和文件名一致，如 MyComponent.js 里的组件名应该是 MyComponent；一个目录的根组件使用 index.js 命名，以目录名称作为组件名称；  

```javascript
    // file contents
    const CheckBox = React.createClass({
      // ...
    })

    module.exports = CheckBox;

    // in some other file
    // bad
    const CheckBox = require('./checkBox');

    // bad
    const CheckBox = require('./check_box');

    // good
    const CheckBox = require('./CheckBox');
```

- **引用命名**：React 组件使用大驼峰命名法，HTML 标签、组件实例使用小驼峰命名法；  

```javascript
// bad
const Footer = require('./Footer/Footer.js') 
// bad
const Footer = require('./Footer/index.js') 
// good
const Footer = require('./Footer')
```

- **属性命名**  

1. React 组件的属性使用**小驼峰命名法**；  
2. 使用 `className` 代替 `class` 属性；  
3. 使用 `htmlFor` 代替 `for` 属性。  

- **传递给 HTML 的属性：**  

1. 传递给 HTML 元素的自定义属性，需要添加 `data-` 前缀，React 不会渲染非标准属性；  
2. [无障碍](http://www.w3.org/WAI/intro/aria) 属性 `aria-` 可以正常使用。  

- **属性设置** 
  1. 在组件行内设置属性（以便 `propTypes` 校验），不要在外部改变属性的值；  
  2. 属性较多使用 `{...this.props}` 语法；  
  3. 重复设置属性值时，前面的值会被后面的覆盖。  

```javascript
    var component = <Component />;
    component.props.foo = x; // bad
    component.props.bar = y; // also bad

    // good
    var component = <Component foo={x} bar={y} />;

    // good
    var props = {};
    props.foo = x;
    props.bar = y;
    var component = <Component {...props} />;

    var props = { foo: 'default' };
    var component = <Component {...props} foo={'override'} />;
    console.log(component.props.foo); // 'override'
```

- **属性对齐方式**

1. 属性较少时可以行内排列；  
2. 属性较多时每行一个属性，闭合标签单独成行

```javascript
    // bad - too long
    <input type="text" value={this.state.newDinosaurName} onChange={this.inputHandler.bind(this, 'newDinosaurName')} />  

    // bad - aligning attributes after the tag
    <input type="text"  
           value={this.state.newDinosaurName}
           onChange={this.inputHandler.bind(this, 'newDinosaurName')} /> 

    // good
    <input  
      type="text"
      value={this.state.newDinosaurName}
      onChange={this.inputHandler.bind(this, 'newDinosaurName')}
     />

     // if props fit in one line then keep it on the same line
    <Foo bar="bar" />

    // children get indented normally
    <Foo
      superLongParam="bar"
      anotherSuperLongParam="baz"
    >
      <Spazz />
    </Foo>


    // bad
    <Foo
      bar="bar"
      baz="baz" />

    // good
    <Foo
      bar="bar"
      baz="baz"
    />
```

- **带命名空间的组件**  

如果一个组件有许多关联子组件，可以以该组件作为命名空间编写、调用子组件。

```javascript
var MyFormComponent = React.createClass({ ... });
    MyFormComponent.Row = React.createClass({ ... });
    MyFormComponent.Label = React.createClass({ ... }); 
    MyFormComponent.Input = React.createClass({ ... });

    var Form = MyFormComponent;

    var App = (

    );
```

### <h3 id="react-component-standard">四、组件相关规范</h3>

### 组建声明

```javascript
    // bad 
    export default React.createClass({ 
        displayName: 'ReservationCard', // stuff goes here 
    });

    // good 
    const ReservationCard = React.createClass({ 
        // stuff goes here
    });

    export default ReservationCard;
```

### 行内迭代

运算逻辑简单的直接使用行内迭代。

```javascript
    return (
      <div>
        {this.props.data.map(function(data, i) {
          return (<Component data={data} key={i} />)
        })}
        </div>
    );
```

### 注释

组建之间的注释需要用'{}'包裹

```javascript
   var content = (
      <Nav>
        {/* child comment, put {} around */}
        <Person
          /* multi
             line
             comment */
          name={window.isLoggedIn ? window.name : ''} // end of line comment
        />
      </Nav>
    );
```

### 引号使用

1.HTML/JSX 属性使用双引号`"`

2.JS 使用单 `'`

```jsx
// bad
<Foo bar='bar' />
// good
<Foo bar="bar" />

// bad
<Foo style={{ left: "20px" }} />

// good
<Foo style={{ left: '20px' }} />

// JavaScript Expression
const person = <Person name={window.isLoggedIn ? window.name : ''} />;

// HTML/JSX
const myDivElement = <div className="foo" />;
const app = <Nav color="blue" />;
const content = ( <Container> {window.isLoggedIn ? <Nav /> : <Login />} </Container>
);
```

### 条件 HTML

1. 简短的输出在行内直接三元运算符；

   ```jsx
   {this.state.show && 'This is Shown'}
   {this.state.on ? 'On' : 'Off'}
   ```

2. 较复杂的结构可以在`.render()` 方法内定义一个以 `Html` 结尾的变量。

   ```jsx
       var dinosaurHtml = ''; 
       if (this.state.showDinosaurs) {  
         dinosaurHtml = (
           <section>
             <DinosaurTable />
             <DinosaurPager />
           </section>
         );
       }
   
       return (  
         <div>
           ...
           {dinosaurHtml}
           ...
         </div>
       );
   ```

### 小括号`()` 的使用

1. 多行的 JSX 使用 `()` 包裹，有组件嵌套时使用多行模式；

   ```jsx
   // bad
    return (<div><ComponentOne /><ComponentTwo /></div>);
   // good
   var multilineJsx = (  
     <header>
       <Logo />
       <Nav />
     </header>
   );
   
   // good
   return (
     <div>
       <ComponentOne />
       <ComponentTwo />
     </div>
   );
   ```
2. 单行 JSX 省略 `()`

   ```jsx
   var singleLineJsx = <h1>Simple JSX</h1>;
   // good, when single line
   render() {
     const body = <div>hello</div>;
     return <MyComponent>{body}</MyComponent>;
   }
   ```

### 自闭合标签

1. JSX 中所有标签**必须闭合**；  
   - 没有子元素的组件使用自闭合语法，自闭合标签 **`/` 前留一个空格**。

```jsx
// bad
 <Logo></Logo>
 <Logo/>
 // very bad
<Foo                 />

// bad
<Foo />

// good
<Logo />
```

### **组件内部代码组织**

1. **不要使用下划线前缀**命名 React 组件的方法；  

```jsx
 // bad
    React.createClass({
      _onClickSubmit() {
        // do stuff
      }

      // other stuff
    });

    // good
    React.createClass({
      onClickSubmit() {
        // do stuff
      }

      // other stuff
    });
```

2. 按照生命周期组顺序织组件的方法、属性；  
   - 方法（属性）之间空一行；  

   - `.render()` 方法始终放在最后；  

   - 自定义方法 React API 方法之后、`.render()` 之前。

     顺序：继承 React.Component 的类的方法遵循下面的顺序

     1.constructor  

     2.optional static methods

     3.getChildContext

     4.componentWillMount

     5.componentDidMount  

     6.componentWillReceiveProps

     7.shouldComponentUpdate

     8.componentWillUpdate

     9.componentDidUpdate

     10.componentWillUnmount

     11.clickHandlers or eventHandlers like onClickSubmit() or onChangeDescription()

     12.getter methods for render like getSelectReason() or getFooterContent()

     13.Optional render methods like renderNavigation() or renderProfilePicture()

     14.render

```jsx
    // React 组件中按照以下顺序组织代码
    React.createClass({  
      displayName: '',

      mixins: [],

      statics: {},

      propTypes: {},

      getDefaultProps() {
        // ...
      },

      getInitialState() {
        // do something
      },

      componentWillMount() {
          // do something
      },

      componentDidMount() {
        // do something: add DOM event listener, etc.
      },

      componentWillReceiveProps() {
      },

      shouldComponentUpdate() {},

      componentWillUpdate() {},

      componentDidUpdate() {},

      componentWillUnmount() {
          // do something: remove DOM event listener. etc.
      },

      // clickHandlers or eventHandlers like onClickSubmit() or onChangeDescription()
      handleClick() {
        // ...
      },

      // getter methods for render like getSelectReason() or getFooterContent()

      // Optional render methods like renderNavigation() or renderProfilePicture()

      render() {
        // ...
      }
    });
```

- 定义 propTypes，defaultProps，contextTypes 等等…

```jsx
import React, { PropTypes } from 'react';

const propTypes = {
  id: PropTypes.number.isRequired,
  url: PropTypes.string.isRequired,
  text: PropTypes.string,
};

const defaultProps = {
  text: 'Hello World',
};

class Link extends React.Component {
  static methodsAreOk() {
    return true;
  }

  render() {
    return <a href={this.props.url} data-id={this.props.id}>{this.props.text}</a>
  }
}

Link.propTypes = propTypes;
Link.defaultProps = defaultProps;

export default Link;
```

使用 React.createClass 时，方法顺序如下：

1.displayName
2.propTypes
3.contextTypes
4.childContextTypes
5.mixins

6.statics 
7.defaultProps 
8.getDefaultProps
9.getInitialState
10.getChildContext
11.componentWillMount
12.componentDidMount
13.componentWillReceiveProps
14.shouldComponentUpdate
15.componentWillUpdate
16.componentDidUpdate
17.componentWillUnmount

18.clickHandlers or eventHandlers like onClickSubmit() or onChangeDescription()
19.getter methods for render like getSelectReason() or getFooterContent()
20.Optional render methods like renderNavigation() or renderProfilePicture()
21.render

## <h3 id="react-agreements">五、约定</h3>

### **注释**

文件头部注释  

```jsx
/* ------------------------------------------------------------
 author : cattleya
 create:2016-12-30
 descreption:recharge 相关样式（包含input/label/button）
 ------------------------------------------------------------ */
```

注：尽量避免使用多行注释 `/* */`,应使用多个单行注释  `//`  

函数注释，可使用块级注释  

```jsx

/* *函数注释
*@ param {string} p1 参数1的说明
*@ param {string} p2 参数2的说明，比较长
*@ return 返回值描述 */ aa() => {
    alert();
}
```

**条件(三元)操作符 (?:)**  

三元操作符用于替代 if 条件判断语句。  

```jsx
// bad
if (val != 0) { return foo();
} else { return bar();
} 

// good
return val ? foo() : bar();
```

## <h3 id="react-css">六、react 中 CSS使用的相关规范</h3>

### **代码组织**

**Class 和 ID**  

- 使用语义化、通用的命名方式（不能使用汉语拼音）；  
- 使用连字符 作为 ID、Class 名称界定符，不要驼峰命名法和下划线；  
- 避免选择器嵌套层级过多，尽量少于 3 级；  
- 避免选择器和 Class、ID 叠加使用；  

```css
    /* Not recommended */
    .red {}
    .box_green {}
    .page .header .login #username input {}
    ul#example {}

    /* Recommended */
    #nav {}
    .box-video {}
    #username input {}
    #example {}
```

/* Not recommended */
    .red {}
    .box_green {}
    .page .header .login #username input {}
    ul#example {}

**声明块格式**  

- 选择器分组时，保持独立的选择器占用一行；  
- 有多个选择器公用同一css代码块时，选择器应以逗号分隔，并换行  
- 声明块的左括号 { 前添加一个空格；  
- 声明块的右括号 } 应单独成行；  
- 声明语句中的 ` : ` 后应添加一个空格；  
- 声明语句应以分号 ` ;`  结尾；  
- 一般以逗号分隔的属性值，每个逗号后应添加一个空格；  
- 对于属性值或颜色参数，省略小数前面的 0 （例如，.5 代替 0.5；-.5px 代替 -0.5px）；  
- 十六进制值应该全部小写和尽量简写，例如，#fff 代替 #ffffff；  
- 避免为 0 值指定单位，例如，用 margin: 0; 代替 margin: 0px;；  

```css
/* Not recommended */ 
.selector, .selector-secondary, .selector[type=text] {
 padding:15px;
 margin:0px 0px 15px;
 background-color:rgba(0, 0, 0, 0.5);
 box-shadow:0px 1px 2px #CCC,inset 0 1px 0 #FFFFFF
 }

 .m-userlist .list { position: relative; height: 100px;overflow: hidden} 

 /* Recommended */ 
 .selector,
.selector-secondary,
.selector[type="text"] {
  padding: 15px;
  margin-bottom: 15px;
  background-color: rgba(0,0,0,.5);
  box-shadow: 0 1px 2px #ccc, inset 0 1px 0 #fff;
}
```

**hack**  

能不使用`hack`尽量不要使用，如果必须使用，请将`hack`加在属性上  
如  

```css
.head{  
 *height: 200px
}
```

**媒体查询（Media query）的位置**  

将媒体查询放在尽可能相关规则的附近。不要将他们打包放在一个单一样式文件中或者放在文档底部。如果你把他们分开了，将来只会被大家遗忘。  

```css
    .element { ... }
    .element-avatar { ... }
    .element-selected { ... }

    @media (max-width: 768px) {
      .element { ...}
      .element-avatar { ... }
      .element-selected { ... }
    }
```

**引号使用**  

url() 、属性选择符、属性值使用双引号。 参考[ Is quoting the value of url() really necessary?](http://stackoverflow.com/questions/2168855/is-quoting-the-value-of-url-really-necessary)  

```css
/* Not recommended */ 
html { 
    font-family: 'open sans', arial, sans-serif;
 }
/* Recommended */ 
html { 
    font-family: "open sans", arial, sans-serif;
} 

.selector[type="text"] {

}
```

**不要使用 @import**  

与 <link> 相比，@import 要慢很多，不光增加额外的请求数，还会导致不可预料的问题。  

替代办法：  

使用多个 元素；
通过 Sass 或 Less 类似的 CSS 预处理器将多个 CSS 文件编译为一个文件；
其他 CSS 文件合并工具；

**注释**  

不同模块的内容，在头部、媒体公告添加模块名称等  

如果下为头部、媒体公告css  

```css
/* 头部模块
 ============================================================================*/ 
/* 媒体公告模块
 ============================================================================*/ 
.m-userlist {
  /* 属性声明 */ 
  margin: 0 0 30px;
  /* 属性名:属性值; */
}

/* 左侧部分 */ 
.m-userlist .list { 
    position: relative; 
    height: 100px; 
    overflow: hidden;
}

/* 右侧部分 */ 
.m-userlist .list { 
    position: relative; 
    height: 100px; 
    overflow: hidden;
}
```

### CSS渲染性能优化，避免过分重排

当发生重排的时候，浏览器需要重新计算布局位置与大小，前端工程师要明白「浏览器渲染」[更多详情](http://www.jianshu.com/p/e305ace24ddf)。  

常见的重排元素:  

- width  
- height  
- padding  
- margin  
- display  
- border-width  
- position  
- top  
- left  
- right  
- bottom  
- font-size  
- float  
- text-align  
- overflow-y  
- font-weight  
- overflow  
- font-family  
- line-height  
- vertical-align  
- clear  
- white-space  
- min-height  

**正确使用 Display 的属性**  

- Display 属性会影响页面的渲染，请合理使用。  
- display: inline后不应该再使用 width、height、margin、padding 以及 float；  
- display: inline-block 后不应该再使用 float；  
- display: block 后不应该再使用 vertical-align；  
- display: table-* 后不应该再使用 margin 或者 float；  

  **不滥用 Float**

Float在渲染时计算量比较大，尽量减少使用。  

## <h2 id="react-eslint">七、代码校验工具</h2>

## <h3 id="react-eslint">eslint</h3>

- eslint 官方地址
  [ESLint](https://www.github.com/eslint/eslint) 

- eslint 的extends推荐持用 airbnb,项目前期可以先使用recommend过渡，具体设置和rules可以看 [ESLint 规则说明](https://cloud.tencent.com/developer/chapter/12618)

- 推荐持用的插件
  > - eslint
  > - husky
  > - prettier
  > - eslint-plugin-prettier
  > - ...






  /* TODO */