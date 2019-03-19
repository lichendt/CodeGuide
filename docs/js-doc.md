
## <h2 id="golden-rule">最佳原则</h2>

坚持制定好的代码规范。

无论团队人数多少，代码应该同出一门。

如果你想要为这个规范做贡献或觉得有不合理的地方，请访问[New Issue](https://github.com/AlloyTeam/CodeGuide/issues/new)。

## <h2 id="nameing-rule"> 命名规则</h2>

### <h3 id="project-naming">项目命名</h3>

全部采用小写方式， 以下划线分隔。

例：my_project_name

### <h3 id="folder-naming">目录命名</h3>

参照项目命名规则；

有复数结构时，要采用复数命名法。

例：scripts, styles, images, data_models

### <h3 id="js-naming">JS文件命名</h3>

参照项目命名规则。

例：account_model.js

### <h3 id="css-naming">CSS, SCSS文件命名</h3>

参照项目命名规则。

例：retina_sprites.scss

### <h3 id="html-naming">HTML文件命名</h3>

参照项目命名规则。

例：error_report.html


## <h2 id="javascript">JavaScript</h2>

### <h3 id="js-indentation">缩进</h3>

使用soft tab（4个空格）。

```javascript
var x = 1,
    y = 1;

if (x < y) {
    x += 10;
} else {
    x += 1;
}
```

### <h3 id="js-line-max-length">单行长度</h3>

不要超过80，但如果编辑器开启word wrap可以不考虑单行长度。

### <h3 id="js-semicolon">分号</h3>

以下几种情况后需加分号：

- 变量声明
- 表达式
- return
- throw
- break
- continue
- do-while

```javascript
/* var declaration */
var x = 1;

/* expression statement */
x++;

/* do-while */
do {
    x++;
} while (x < 10);
```

### <h3 id="js-space">空格</h3>

以下几种情况不需要空格：

- 对象的属性名后
- 前缀一元运算符后
- 后缀一元运算符前
- 函数调用括号前
- 无论是函数声明还是函数表达式，'('前不要空格
- 数组的'['后和']'前
- 对象的'{'后和'}'前
- 运算符'('后和')'前

以下几种情况需要空格：

- 二元运算符前后
- 三元运算符'?:'前后
- 代码块'{'前
- 下列关键字前：`else`,`while`,`catch`,`finally`
- 下列关键字后：`if`,`else`,`for`,`while`,`do`,`switch`,`case`,`try`,`catch`,`finally`,`with`,`return`,`typeof`
- 单行注释'//'后（若单行注释和代码同行，则'//'前也需要），多行注释'*'后
- 对象的属性值前
- for循环，分号后留有一个空格，前置条件如果有多个，逗号后留一个空格
- 无论是函数声明还是函数表达式，'{'前一定要有空格
- 函数的参数之间

```javascript
// not good
var a = {
    b :1
};

// good
var a = {
    b: 1
};

// not good
++ x;
y ++;
z = x?1:2;

// good
++x;
y++;
z = x ? 1 : 2;

// not good
var a = [ 1, 2 ];

// good
var a = [1, 2];

// not good
var a = ( 1+2 )*3;

// good
var a = (1 + 2) * 3;

// no space before '(', one space before '{', one space between function parameters
var doSomething = function(a, b, c) {
    // do something
};

// no space before '('
doSomething(item);

// not good
for(i=0;i<6;i++){
    x++;
}

// good
for (i = 0; i < 6; i++) {
    x++;
}
```

### <h3 id="js-blank-line">空行</h3>

以下几种情况需要空行：

- 变量声明后（当变量声明在代码块的最后一行时，则无需空行）
- 注释前（当注释在代码块的第一行时，则无需空行）
- 代码块后（在函数调用、数组、对象中则无需空行）
- 文件最后保留一个空行

```javascript
// need blank line after variable declaration
var x = 1;

// not need blank line when variable declaration is last expression in the current block
if (x >= 1) {
    var y = x + 1;
}

var a = 2;

// need blank line before line comment
a++;

function b() {
    // not need blank line when comment is first line of block
    return a;
}

// need blank line after blocks
for (var i = 0; i < 2; i++) {
    if (true) {
        return false;
    }

    continue;
}

var obj = {
    foo: function() {
        return 1;
    },

    bar: function() {
        return 2;
    }
};

// not need blank line when in argument list, array, object
func(
    2,
    function() {
        a++;
    },
    3
);

var foo = [
    2,
    function() {
        a++;
    },
    3
];


var foo = {
    a: 2,
    b: function() {
        a++;
    },
    c: 3
};
```

### <h3 id="js-new-line">换行</h3>

换行的地方，行末必须有','或者运算符；

以下几种情况不需要换行：

- 下列关键字后：`else`,`catch`,`finally`
- 代码块'{'前

以下几种情况需要换行：

- 代码块'{'后和'}'前
- 变量赋值后

```javascript
// not good
var a = {
    b: 1
    , c: 2
};

x = y
    ? 1 : 2;

// good
var a = {
    b: 1,
    c: 2
};

x = y ? 1 : 2;
x = y ?
    1 : 2;

// no need line break with 'else', 'catch', 'finally'
if (condition) {
    ...
} else {
    ...
}

try {
    ...
} catch (e) {
    ...
} finally {
    ...
}

// not good
function test()
{
    ...
}

// good
function test() {
    ...
}

// not good
var a, foo = 7, b,
    c, bar = 8;

// good
var a,
    foo = 7,
    b, c, bar = 8;
```

### <h3 id="js-comments-single-line">单行注释</h3>

双斜线后，必须跟一个空格；

缩进与下一行代码保持一致；

可位于一个代码行的末尾，与代码间隔一个空格。

```javascript
if (condition) {
    // if you made it here, then all security checks passed
    allowed();
}

var zhangsan = 'zhangsan'; // one space after code
```

### <h3 id="js-comments-multiline">多行注释</h3>

最少三行, '*'后跟一个空格，具体参照右边的写法；

建议在以下情况下使用：

- 难于理解的代码段
- 可能存在错误的代码段
- 浏览器特殊的HACK代码
- 业务逻辑强相关的代码

```javascript
/*
 * one space after '*'
 */
var x = 1;
```

### <h3 id="js-comments-documentation">文档注释</h3>

各类标签@param, @method等请参考[usejsdoc](http://usejsdoc.org/)和[JSDoc Guide](http://yuri4ever.github.io/jsdoc/)；

建议在以下情况下使用：

- 所有常量
- 所有函数
- 所有类

```javascript
/**
 * @func
 * @desc 一个带参数的函数
 * @param {string} a - 参数a
 * @param {number} b=1 - 参数b默认值为1
 * @param {string} c=1 - 参数c有两种支持的取值</br>1—表示x</br>2—表示xx
 * @param {object} d - 参数d为一个对象
 * @param {string} d.e - 参数d的e属性
 * @param {string} d.f - 参数d的f属性
 * @param {object[]} g - 参数g为一个对象数组
 * @param {string} g.h - 参数g数组中一项的h属性
 * @param {string} g.i - 参数g数组中一项的i属性
 * @param {string} [j] - 参数j是一个可选参数
 */
function foo(a, b, c, d, g, j) {
    ...
}
```

### <h3 id="js-quote-marks">引号</h3>

最外层统一使用单引号。

```javascript
// not good
var x = "test";

// good
var y = 'foo',
    z = '<div id="test"></div>';
```

### <h3 id="js-variable-naming">变量命名


- 标准变量采用驼峰式命名（除了对象的属性外，主要是考虑到cgi返回的数据）
- 见名知意,用词准确，不用拼单和拼音首字母，英文除常用缩写词如URL、TCP外，尽量不用缩写
- 常量常量全大写，用下划线连接，使用 UPPER_CASE_WITH_UNDERLINE 规则
- 变量使用 lowerCamelCase 规则
- 'ID'在变量名中全大写
- 'URL'在变量名中全大写
- 'Android'在变量名中大写第一个字母
- 'iOS'在变量名中小写第一个，大写后两个字母
- 构造函数，大写第一个字母
- jquery对象必须以'$'开头命名


```javascript
var thisIsMyName;

var goodID;

var reportURL;

var AndroidVersion;

var iOSVersion;

var MAX_COUNT = 10;

function Person(name) {
    this.name = name;
}

// not good
var body = $('body');

// good
var $body = $('body');
```

### <h3 id="js-variable-declaration">变量声明</h3>

- 一个函数作用域中所有的变量声明尽量提到函数首部，用一个var声明，不允许出现两个连续的var声明。
- 尽量使用解构赋值
- 不可声明无用变量

```javascript
function doSomethingWithItems(items) {
    // use one var
    var value = 10,
        result = value + 10,
        i,
        len;

    for (i = 0, len = items.length; i < len; i++) {
        result += 10;
    }
}
```

### <h3 id="js-function">函数</h3>



函数调用括号前不需要空格；

立即执行函数外必须包一层括号；

不要给inline function命名；

参数之间用', '分隔，注意逗号后有一个空格。

```javascript
// no space before '(', but one space before'{'
var doSomething = function(item) {
    // do something
};

function doSomething(item) {
    // do something
}

// not good
doSomething (item);

// good
doSomething(item);

// requires parentheses around immediately invoked function expressions
(function() {
    return 1;
})();

// not good
[1, 2].forEach(function x() {
    ...
});

// good
[1, 2].forEach(function() {
    ...
});

// not good
var a = [1, 2, function a() {
    ...
}];

// good
var a = [1, 2, function() {
    ...
}];

// use ', ' between function parameters
var doSomething = function(a, b, c) {
    // do something
};
```

### <h3 id="js-array-object">数组、对象</h3>

对象属性名不需要加引号；

对象以缩进的形式书写，不要写在一行；

数组、对象最后不要有逗号。

单行定义的数组值间需在逗号后面带一个空格

单行定义的中括号内侧需各带一个空格

单行定义的对象值间需在逗号后面带一个空格

单行定义的大括号内侧需各带一个空格

冒号左侧不需要带空格，右侧带一个空格

```javascript
// not good
var a = {
    'b': 1
};

var a = {b: 1};

var a = {
    b: 1,
    c: 2,
};

// good
var a = {
    b: 1,
    c: 2
};

let array1 = [ 1, 2, 3, 4 ];
let array2 = [
  'Hello',
  'World!'
];

let obj1 = { key1: 'value1', key2: 'value2', key3: 'value3' };
let obj2 = {
  key1: 'value1',
  key2: 'value2',
  key3: 'value3'
};
```

### <h3 id="js-brace">括号</h3>

下列关键字后必须有大括号（即使代码块的内容只有一行）：`if`,`else`,`for`,`while`,`do`,`switch`,`try`,`catch`,`finally`,`with`。

```javascript
// not good
if (condition)
    doSomething();

// good
if (condition) {
    doSomething();
}
```

### <h3 id="js-literal-value-null">null</h3>

适用场景：

- 初始化一个将来可能被赋值为对象的变量
- 与已经初始化的变量做比较
- 作为一个参数为对象的函数的调用传参
- 作为一个返回对象的函数的返回值

不适用场景：

- 不要用null来判断函数调用时有无传参
- 不要与未初始化的变量做比较

```javascript
// not good
function test(a, b) {
    if (b === null) {
        // not mean b is not supply
        ...
    }
}

var a;

if (a === null) {
    ...
}

// good
var a = null;

if (a === null) {
    ...
}
```

### <h3 id="js-literal-value-undefined">undefined</h3>

永远不要直接使用undefined进行变量判断；

使用typeof和字符串'undefined'对变量进行判断。

```javascript
// not good
if (person === undefined) {
    ...
}

// good
if (typeof person === 'undefined') {
    ...
}
```

### <h3 id="js-jshint">jshint</h3>

用'===', '!=='代替'==', '!='；

for-in里一定要有hasOwnProperty的判断；

不要在内置对象的原型上添加方法，如Array, Date；

不要在内层作用域的代码里声明了变量，之后却访问到了外层作用域的同名变量；

变量不要先使用后声明；

不要在一句代码中单单使用构造函数，记得将其赋值给某个变量；

不要在同个作用域下声明同名变量；

不要在一些不需要的地方加括号，例：delete(a.b)；

不要使用未声明的变量（全局变量需要加到.jshintrc文件的globals属性里面）；

不要声明了变量却不使用；

不要在应该做比较的地方做赋值；

debugger不要出现在提交的代码里；

数组中不要存在空元素；

不要在循环内部声明函数；

不要像这样使用构造函数，例：`new function () { ... }`,`new Object`；

```javascript
// not good
if (a == 1) {
    a++;
}

// good
if (a === 1) {
    a++;
}

// good
for (key in obj) {
    if (obj.hasOwnProperty(key)) {
        // be sure that obj[key] belongs to the object and was not inherited
        console.log(obj[key]);
    }
}

// not good
Array.prototype.count = function(value) {
    return 4;
};

// not good
var x = 1;

function test() {
    if (true) {
        var x = 0;
    }

    x += 1;
}

// not good
function test() {
    console.log(x);

    var x = 1;
}

// not good
new Person();

// good
var person = new Person();

// not good
delete(obj.attr);

// good
delete obj.attr;

// not good
if (a = 10) {
    a++;
}

// not good
var a = [1, , , 2, 3];

// not good
var nums = [];

for (var i = 0; i < 10; i++) {
    (function(i) {
        nums[i] = function(j) {
            return i + j;
        };
    }(i));
}

// not good
var singleton = new function() {
    var privateVar;

    this.publicMethod = function() {
        privateVar = 1;
    };

    this.publicMethod2 = function() {
        privateVar = 2;
    };
};
```

### <h3 id="js-miscellaneous">杂项</h3>

不要混用tab和space；

不要在一处使用多个tab或space；

换行符统一用'LF'；

对上下文this的引用只能使用'_this', 'that', 'self'其中一个来命名；

行尾不要有空白字符；

switch的falling through和no default的情况一定要有注释特别说明；

不允许有空的代码块。

```javascript
// not good
var a   = 1;

function Person() {
    // not good
    var me = this;

    // good
    var _this = this;

    // good
    var that = this;

    // good
    var self = this;
}

// good
switch (condition) {
    case 1:
    case 2:
        ...
        break;
    case 3:
        ...
    // why fall through
    case 4
        ...
        break;
    // why no default
}

// not good with empty block
if (condition) {

}
```

## <h2 id="check">编辑器配置和构建检查</h2>

### <h3 id="check-sublime3">sublime3插件</h3>

1. 安装node包

   - jscs`npm install jscs -g`
   - jshint`npm install jshint -g`
   - csscomb`npm install csscomb -g`
   - csslint`npm install csslint -g`

2. 安装gem包

   - scss-lint`gem install scss_lint`

3. 安装sublime3 [Package Control](https://packagecontrol.io/installation#st3)

   - 按下``ctrl+` ``
   - 复制粘贴以下代码`import urllib.request,os,hashlib; h = 'eb2297e1a458f27d836c04bb0cbaf282' + 'd0e7a3098092775ccb37ca9d6b2e4b7d'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)`

4. 安装sublime3插件

   - 按下`ctrl+shift+p`，输入'ip'（Install Package）

   - 输入以下插件的名字，按顺序逐个进行安装：

     - `EditorConfig`
     - `Sass`
     - `SublimeLinter`
     - `SublimeLinter-jscs`
     - `SublimeLinter-jshint`
     - `SublimeLinter-csslint`
     - `SublimeLinter-contrib-scss-lint`
     - `JSFormat`
     - `CSScomb`

5. 插件的配置文件

   将以下配置文件分别下载后放入项目根目录下：

   - `EditorConfig`[配置文件](.editorconfig)

   - `JSCS`[配置文件](.jscsrc)

   - `JSHint`[配置文件](.jshintrc)

     注意：全局变量需要手动加到配置文件的globals属性里，例：

     ```json
     {
         "globals": {
             "ImageHandle": true
         }
     }
     ```

   - `CSSLint`[配置文件](.csslintrc)

   - `SCSS-Lint`[配置文件](.scss-lint.yml)

6. 编辑器及插件设置

   - `sublime3`自身

     Preferences->Setting-User，增加下面两个配置：

     ```json
     {
         "translate_tabs_to_spaces": true,
         "word_wrap": true
     }
     ```

     点击右下角的Spaces->Convert Indentation to Spaces可以将文件中的所有tab转换成空格

   - `JSFormat`

     Preferences->Package Settings->JSFormat->Setting-User，下载[配置文件](jsformat_setting_user.json)覆盖

     配置好后格式化的默认快捷键是`ctrl+alt+f`

   - `SublimeLinter`

     右键->SublimeLinter->Lint Mode，有4种检查模式，建议选择`Load/save`

     右键->SublimeLinter->Mark Style，建议选择`Outline`

     右键->SublimeLinter->Choose Gutter Theme，建议选择`Blueberry-round`

     右键->SublimeLinter->Open User Settings，将linter里面jscs的args改成`["--verbose"]`，将linter里面csslint的ignore改成`"box-model,adjoining-classes,box-sizing,compatible-vendor-prefixes,gradients,text-indent,fallback-colors,star-property-hack,underscore-property-hack,bulletproof-font-face,font-faces,import,regex-selectors,universal-selector,unqualified-attributes,overqualified-elements,duplicate-background-images,floats,font-sizes,ids,important,outline-none,qualified-headings,unique-headings"`

     当光标处于有错误的代码行时，详细的错误信息会显示在下面的状态栏中

     右键->SublimeLinter可以看到所有的快捷键，其中`ctrl+k, a`可以列出所有错误

   - `CSScomb`

     Preferences->Package Settings->CSScomb->Setting-User，下载[配置文件](csscomb_setting_user.json)覆盖

     配置好后格式化的默认快捷键是`ctrl+shift+c`

### <h3 id="check-grunt">grunt插件</h3>

1. 在项目中安装grunt插件

   - jscs`npm install grunt-jscs --save-dev`
   - jshint`npm install grunt-contrib-jshint --save-dev`
   - csslint`npm install grunt-contrib-csslint --save-dev`
   - scss-lint`npm install grunt-scss-lint --save-dev`

2. 插件的配置文件

   - `JSCS`

     ```javascript
     {
         options: {
             config: true,
             verbose: true
         },
         files: {
             src: [...]
         }
     }
     ```

   - `JSHint`

     ```json
         options: {
             jshintrc: true
         },
         files: {
             src: [...]
         }
     }
     ```

   - `CSSLint`

     ```json
     {
         options: {
             csslintrc: '.csslintrc'
         },
         files: {
             src: [...]
         }
     }
     ```

   - `SCSS-Lint`

     ```json
         options: {
             config: '.scss-lint.yml'
         },
         files: {
             src: [...]
         }
     }
     ```

### 

