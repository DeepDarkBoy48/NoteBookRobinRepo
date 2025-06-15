# Vue.js 学习笔记

本教程整理了 Vue.js 入门相关的 HTML 和 JavaScript 代码示例。

## 1. 01 快速入门.html

这个文件是 Vue.js 的一个最基础的"Hello World"示例。它展示了如何：

1. 通过 CDN 引入 Vue.js。
2. 使用 `createApp` 创建一个 Vue 应用实例。
3. 在 `data` 选项中定义数据（例如 `msg`）。
4. 通过 `mount` 方法将 Vue 实例挂载到页面上的一个 DOM 元素（`#app`）。
5. 在 HTML 中使用双大括号 `{{ }}` 语法来显示 `data` 中的数据，实现了最基本的数据绑定。

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <div id="app">
      <h1>{{msg}}</h1>
    </div>

    <div>
      <h1>{{msg}}</h1>
    </div>
    <!-- 引入vue模块 -->
    <script type="module">
      import { createApp } from "https://unpkg.com/vue@3/dist/vue.esm-browser.js";
      // 定义一个接口来描述你的数据结构
      createApp({
        data() {
          return {
            msg: "hello vue3",
          };
        },
      }).mount("#app");
    </script>
  </body>
</html>
```

## 2. 02 指令 v-for.html

这个文件演示了 `v-for` 指令的用法，它是 Vue 中用于列表渲染的核心指令。

1. `v-for` 指令被用在 `<tr>` 元素上，表示需要根据数据多次渲染这个元素。
2. 它遍历 `articleList` 数组，数组中的每个 `article` 对象都将创建一个对应的 `<tr>`。
3. 在 `<tr>` 内部，可以使用 `{{ article.title }}` 等语法来访问当前遍历项的属性。

这对于从数组动态生成列表（如表格、列表项等）非常有用。

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <div id="app">
      <table border="1 solid" colspa="0" cellspacing="0">
        <tr>
          <th>文章标题</th>
          <th>分类</th>
          <th>发表时间</th>
          <th>状态</th>
          <th>操作</th>
        </tr>
        <!-- 哪个元素要出现多次,v-for指令就添加到哪个元素上 -->
        <tr v-for="(article,index) in articleList">
          <td>{{article.title}}</td>
          <td>{{article.category}}</td>
          <td>{{article.time}}</td>
          <td>{{article.state}}</td>
          <td>
            <button>编辑</button>
            <button>删除</button>
          </td>
        </tr>
      </table>
    </div>

    <script type="module">
      //导入vue模块
      import { createApp } from "https://unpkg.com/vue@3/dist/vue.esm-browser.js";
      //创建应用实例
      createApp({
        data() {
          return {
            //定义数据
            articleList: [
              {
                title: "医疗反腐绝非砍医护收入",
                category: "时事",
                time: "2023-09-5",
                state: "已发布",
              },
              {
                title: "中国男篮缘何一败涂地？",
                category: "篮球",
                time: "2023-09-5",
                state: "草稿",
              },
              {
                title: "华山景区已受大风影响阵风达7-8级，未来24小时将持续",
                category: "旅游",
                time: "2023-09-5",
                state: "已发布",
              },
            ],
          };
        },
      }).mount("#app"); //控制页面元素
    </script>
  </body>
</html>
```

## 3. 03 指令 v-bind.html

这个文件展示了 `v-bind` 指令的用法，它用于动态地绑定一个或多个 HTML 元素的 attribute。

1. `v-bind:href="url"` 将 `<a>` 标签的 `href` 属性的值与 Vue 实例中 `data` 的 `url` 属性绑定起来。
2. 当 `url` 数据发生变化时，渲染出来的 `<a>` 标签的 `href` 属性也会自动更新。
3. `v-bind:` 有一个常用的简写形式，即一个冒号 `:`，所以 `<a :href="url">` 和 `<a v-bind:href="url">` 的效果是完全相同的。

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <div id="app">
      <!-- <a v-bind:href="url">黑马官网</a> -->
      <a :href="url">黑马官网</a>
    </div>

    <script type="module">
      //引入vue模块
      import { createApp } from "https://unpkg.com/vue@3/dist/vue.esm-browser.js";
      //创建vue应用实例
      createApp({
        data() {
          return {
            url: "https://www.itheima.com",
          };
        },
      }).mount("#app"); //控制html元素
    </script>
  </body>
</html>
```

## 4. 04 指令 v-if&v-show.html

这个文件对比了 `v-if` 和 `v-show` 两个指令，它们都用于条件性地显示或隐藏元素。

1. `v-if`、`v-else-if`、`v-else`：这是"真正"的条件渲染，因为它们会确保在切换过程中，条件块内的事件监听器和子组件被适当地销毁和重建。如果初始条件为假，那么元素根本不会被渲染到 DOM 中。
2. `v-show`：这个指令只是简单地切换元素的 CSS `display` 属性。无论初始条件是什么，元素总是会被渲染，只是 display 属性可能为 `none`。

**选择**：

- 如果需要频繁切换，使用 `v-show` 性能更好。
- 如果条件在运行时很少改变，使用 `v-if` 更合适，因为它可以减少初始渲染的开销。

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>

  <body>
    <div id="app">
      手链价格为: <span v-if="customer.level>=0 && customer.level<=1">9.9</span>
      <span v-else-if="customer.level>=2 && customer.level<=4">19.9</span>
      <span v-else>29.9</span>

      <br />
      手链价格为:
      <span v-show="customer.level>=0 && customer.level<=1">9.9</span>
      <span v-show="customer.level>=2 && customer.level<=4">19.9</span>
      <span v-show="customer.level>=5">29.9</span>
    </div>

    <script type="module">
      //导入vue模块
      import { createApp } from "https://unpkg.com/vue@3/dist/vue.esm-browser.js";

      //创建vue应用实例
      createApp({
        data() {
          return {
            customer: {
              name: "张三",
              level: 2,
            },
          };
        },
      }).mount("#app"); //控制html元素
    </script>
  </body>
</html>
```

## 5. 05 指令 v-on.html

这个文件演示了 `v-on` 指令，它用于监听 DOM 事件，并在事件触发时执行一些 JavaScript 代码。

1. `v-on:click="money"` 表示当用户点击这个按钮时，会调用 Vue 实例中 `methods` 对象里的 `money` 方法。
2. `methods` 选项用于存放所有事件处理函数或业务逻辑方法。
3. `v-on:` 同样有一个常用的简写形式，即 `@` 符号，所以 `@click="love"` 和 `v-on:click="love"` 是等效的。

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <div id="app">
      <button v-on:click="money">点我有惊喜</button>  
      <button @click="love">再点更惊喜</button>
    </div>

    <script type="module">
      //导入vue模块
      import { createApp } from "https://unpkg.com/vue@3/dist/vue.esm-browser.js";

      //创建vue应用实例
      createApp({
        data() {
          return {
            //定义数据
          };
        },
        methods: {
          money: function () {
            alert("送你钱100");
          },
          love: function () {
            alert("爱你一万年");
          },
        },
      }).mount("#app"); //控制html元素
    </script>
  </body>
</html>
```

## 6. 06 指令 v-model.html

这个文件展示了 `v-model` 指令的强大功能，它用于在表单的 `<input>`, `<textarea>`, 及 `<select>` 元素上创建双向数据绑定。

1. `v-model="searchConditions.category"` 将输入框的值与 `data` 中的 `searchConditions.category` 属性绑定。
2. 这意味着：
   - 当用户在输入框中输入内容时，`searchConditions.category` 的值会自动更新。
   - 当程序中 `searchConditions.category` 的值改变时，输入框中显示的内容也会自动更新。
3. 这个例子还演示了 `methods` 中的方法（如 `clear`) 如何修改数据，以及 `mounted` 生命周期钩子的使用，它常用于在组件挂载到 DOM 后执行初始化操作（如从服务器获取数据）。

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>

  <body>
    <div id="app">
      文章分类: <input type="text" v-model="searchConditions.category" />
      <span>{{searchConditions.category}}</span>

      发布状态: <input type="text" v-model="searchConditions.state" />
      <span>{{searchConditions.state}}</span>

      <button>搜索</button>
      <button v-on:click="clear">重置</button>

      <br />
      <br />
      <table border="1 solid" colspa="0" cellspacing="0">
        <tr>
          <th>文章标题</th>
          <th>分类</th>
          <th>发表时间</th>
          <th>状态</th>
          <th>操作</th>
        </tr>
        <tr v-for="(article,index) in articleList">
          <td>{{article.title}}</td>
          <td>{{article.category}}</td>
          <td>{{article.time}}</td>
          <td>{{article.state}}</td>
          <td>
            <button>编辑</button>
            <button>删除</button>
          </td>
        </tr>
      </table>
    </div>
    <script type="module">
      //导入vue模块
      import { createApp } from "https://unpkg.com/vue@3/dist/vue.esm-browser.js";
      //创建vue应用实例
      createApp({
        data() {
          return {
            //定义数据
            searchConditions: {
              category: "",
              state: "",
            },

            articleList: [
              {
                title: "医疗反腐绝非砍医护收入",
                category: "时事",
                time: "2023-09-5",
                state: "已发布",
              },
              {
                title: "中国男篮缘何一败涂地？",
                category: "篮球",
                time: "2023-09-5",
                state: "草稿",
              },
              {
                title: "华山景区已受大风影响阵风达7-8级，未来24小时将持续",
                category: "旅游",
                time: "2023-09-5",
                state: "已发布",
              },
            ],
          };
        },
        methods: {
          clear: function () {
            //清空category以及state的数据
            //在methods对应的方法里面,使用this就代表的是vue实例,可以使用this获取到vue实例中准备的数据
            this.searchConditions.category = "";
            this.searchConditions.state = "";
          },
        },
        mounted: function () {
          console.log("Vue挂载完毕,发送请求获取数据");
        },
      }).mount("#app"); //控制html元素
    </script>
  </body>
</html>
```

## 7. 07axios 使用.html

这个文件独立于 Vue，演示了如何使用 `axios` 库来发送 HTTP 请求。在现代前端开发中，与后端服务器进行数据交互是必不可少的环节。

1. 首先通过 `<script>` 标签引入 `axios` 库。
2. 代码中展示了如何使用 `axios.post` 方法发送一个 POST 请求，并携带一个 `article` 对象作为请求体。
3. `.then()` 方法用于处理请求成功后的回调，`result.data` 通常包含了服务器返回的核心数据。
4. `.catch()` 方法用于捕获和处理请求过程中发生的错误。
5. 文件中还注释掉了 GET 请求和另一种 POST 写法的示例。

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>

  <body>
    <!-- 引入axios的js文件 -->
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
    <script>
      /* 发送请求 */
      /* axios({
            method:'get',
            url:'http://localhost:8080/article/getAll'
        }).then(result=>{
            //成功的回调
            //result代表服务器响应的所有的数据,包含了响应头,响应体. result.data 代表的是接口响应的核心数据
            console.log(result.data);
        }).catch(err=>{
            //失败的回调
            console.log(err);
        }); */
      let article = {
        title: "明天会更好",
        category: "生活",
        time: "2000-01-01",
        state: "草稿",
      };
      /*  axios({
             method:'post',
             url:'http://localhost:8080/article/add',
             data:article
         }).then(result=>{
             //成功的回调
             //result代表服务器响应的所有的数据,包含了响应头,响应体. result.data 代表的是接口响应的核心数据
             console.log(result.data);
         }).catch(err=>{
             //失败的回调
             console.log(err);
         }); */

      //别名的方式发送请求
      /* axios.get('http://localhost:8080/article/getAll').then(result => {
            //成功的回调
            //result代表服务器响应的所有的数据,包含了响应头,响应体. result.data 代表的是接口响应的核心数据
            console.log(result.data);
        }).catch(err => {
            //失败的回调
            console.log(err);
        }); */
      axios
        .post("http://localhost:8080/article/add", article)
        .then((result) => {
          //成功的回调
          //result代表服务器响应的所有的数据,包含了响应头,响应体. result.data 代表的是接口响应的核心数据
          console.log(result.data);
        })
        .catch((err) => {
          //失败的回调
          console.log(err);
        });
    </script>
  </body>
</html>
```

## 8. 08vue 案例.html

这是一个综合性的案例，它将前面学到的多个概念组合在一起，构建了一个简单的文章搜索和展示功能。

1. **数据绑定**: 使用 `v-model` 将搜索条件与输入框双向绑定。
2. **事件处理**: 使用 `v-on:click` (即 `@click`) 监听搜索按钮的点击事件，并调用 `search` 方法。
3. **列表渲染**: 使用 `v-for` 遍历从服务器获取的 `articleList` 数据，并将其显示在表格中。
4. **生命周期钩子**: 在 `mounted` 钩子函数中，使用 `axios` 发送 GET 请求，在页面加载完成后立即获取所有文章数据。
5. **异步请求**: `search` 方法同样使用 `axios` 根据用户输入的条件向服务器发送请求，然后更新 `articleList` 数据，从而实现页面的动态更新。

这个案例很好地模拟了一个真实的前端应用场景。

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>

  <body>
    <div id="app">
      文章分类: <input type="text" v-model="searchConditions.category" />

      发布状态: <input type="text" v-model="searchConditions.state" />

      <button v-on:click="search">搜索</button>

      <br />
      <br />
      <table border="1 solid" colspa="0" cellspacing="0">
        <tr>
          <th>文章标题</th>
          <th>分类</th>
          <th>发表时间</th>
          <th>状态</th>
          <th>操作</th>
        </tr>
        <tr v-for="(article,index) in articleList">
          <td>{{article.title}}</td>
          <td>{{article.category}}</td>
          <td>{{article.time}}</td>
          <td>{{article.state}}</td>
          <td>
            <button>编辑</button>
            <button>删除</button>
          </td>
        </tr>
        <!-- <tr>
                <td>标题2</td>
                <td>分类2</td>
                <td>2000-01-01</td>
                <td>已发布</td>
                <td>
                    <button>编辑</button>
                    <button>删除</button>
                </td>
            </tr>
            <tr>
                <td>标题3</td>
                <td>分类3</td>
                <td>2000-01-01</td>
                <td>已发布</td>
                <td>
                    <button>编辑</button>
                    <button>删除</button>
                </td>
            </tr> -->
      </table>
    </div>
    <!-- 导入axios的js文件 -->
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
    <script type="module">
      //导入vue模块
      import { createApp } from "https://unpkg.com/vue@3/dist/vue.esm-browser.js";
      //创建vue应用实例
      createApp({
        data() {
          return {
            articleList: [],
            searchConditions: {
              category: "",
              state: "",
            },
          };
        },
        methods: {
          //声明方法
          search: function () {
            //发送请求,完成搜索,携带搜索条件
            axios
              .get(
                "http://localhost:8080/article/search?category=" +
                  this.searchConditions.category +
                  "&state=" +
                  this.searchConditions.state
              )
              .then((result) => {
                //成功回调 result.data
                //把得到的数据赋值给articleList
                this.articleList = result.data;
              })
              .catch((err) => {
                console.log(err);
              });
          },
        },
        //钩子函数mounted中,获取所有文章数据
        mounted: function () {
          //发送异步请求  axios
          axios
            .get("http://localhost:8080/article/getAll")
            .then((result) => {
              //成功回调
              //console.log(result.data);
              this.articleList = result.data;
            })
            .catch((err) => {
              //失败回调
              console.log(err);
            });
        },
      }).mount("#app"); //控制html元素
    </script>
  </body>
</html>
```

## 9. message.html

这个文件和 `showMessage.js` 一起，演示了 JavaScript 的 ES6 模块系统。这是构建大型、可维护应用的基础。

1. `<script type="module">` 告诉浏览器这段脚本将使用 ES6 模块。
2. `import messageMethods from "./showMessage.js";` 从 `showMessage.js` 文件中导入了 `default` 导出的对象。
3. 然后，可以通过 `messageMethods.complexMessage(...)` 来调用导入模块中的方法。
4. 这展示了如何将功能拆分到不同文件中，并通过 `import`/`export` 来组织代码。

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>js导入导出</title>
  </head>

  <body>
    <div id="app">
      <button id="btn">点我展示信息</button>
    </div>

    <script type="module">
      //import  {complexMessage} from  './showMessage.js';

      import messageMethods from "./showMessage.js";
      document.getElementById("btn").onclick = function () {
        //complexMessage('我被点击了...');
        messageMethods.complexMessage("我还是被点击了...");
      };

      let msg = "hello vue3";
      document.getElementById("元素的id属性值").innerHTML = msg;
    </script>
  </body>
</html>
```

## 10. showMessage.js

这个文件作为 `message.html` 的模块，演示了如何从一个文件中导出功能，供其他文件使用。

1. 文件中定义了 `simpleMessage` 和 `complexMessage` 两个函数。
2. `export default { complexMessage, simpleMessage }` 是默认导出的语法。它将一个包含了两个方法 `{}`的对象作为模块的默认输出。
3. 当其他模块使用 `import someName from './showMessage.js'` 时，`someName` 就会得到这个导出的对象。
4. 文件中还注释了命名导出 `export { ... }` 的示例，这是另一种模块导出的方式。

```javascript
//简单的展示信息
/* export  */ function simpleMessage(msg) {
  console.log(msg);
}

//复杂的展示信息
/* export */ function complexMessage(msg) {
  console.log(new Date() + ": " + msg);
}

//批量导出
//export {complexMessage as cm,simpleMessage as sm}

//默认导出
export default { complexMessage, simpleMessage };
```
