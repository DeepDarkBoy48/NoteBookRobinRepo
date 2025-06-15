# 1. 安装



https://vuejs.org/guide/quick-start.html

```bash
npm create vue@latest
```

选项

```bash
✔ Project name: … <your-project-name>
✔ Add TypeScript? … No / Yes
✔ Add JSX Support? … No / Yes
✔ Add Vue Router for Single Page Application development? … No / Yes
✔ Add Pinia for state management? … No / Yes
✔ Add Vitest for Unit testing? … No / Yes
✔ Add an End-to-End Testing Solution? … No / Cypress / Nightwatch / Playwright
✔ Add ESLint for code quality? … No / Yes
✔ Add Prettier for code formatting? … No / Yes
✔ Add Vue DevTools 7 extension for debugging? (experimental) … No / Yes

Scaffolding project in ./<your-project-name>...
Done.
```

安装package.json依赖

```bash
cd <your-project-name>
npm install
```

启动服务

```bash
npm run dev
```



# 2. 部署



```dockerfile
# 构建阶段 (builder stage)
FROM node:18 AS builder

# 设置工作目录
WORKDIR /vue

# 复制 package.json 和 package-lock.json (或 yarn.lock)
COPY . .

# 安装依赖
RUN npm install

# 构建项目
RUN npm run build

# 运行阶段 (runner stage)
FROM nginx:alpine

# 删除默认的 html 文件
RUN rm -rf /usr/share/nginx/html/*

# 从 builder 阶段复制构建产物到 Nginx 目录
COPY --from=builder /vue/dist /usr/share/nginx/html

# 复制 Nginx 配置文件 (可选，如果需要自定义 Nginx 配置)
COPY nginx.conf /etc/nginx/conf.d/default.conf

# 暴露 80 端口
EXPOSE 80

# 启动 Nginx
CMD ["nginx", "-g", "daemon off;"]
```

构建镜像

```bash
sudo docker build -t vue .
```

构建容器

```bash
sudo docker run -d --name vuelearn -p 110:110 vue
```

* [ ] 修改nginx配置

# 3. js导入导出

![](https://yx0zcbyal4l.feishu.cn/space/api/box/stream/download/asynccode/?code=NzQ1MTI5N2U3ZDc3OGIxM2Y0MWFiMDQyZDI4OTA5M2VfQ3Bpd2pObThBMVRZRERkZHZEM1ZEdUZQWXdZMzF6SzFfVG9rZW46SmJaNmJkZjlvbzJmcUF4OVhIbGNZZ004bnhnXzE3NDk1NjgzMTY6MTc0OTU3MTkxNl9WNA)

![](https://yx0zcbyal4l.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDljNDZkMjM3YTU0YzlmZWEwZDA3OTNhOWI4ZDU3NmZfb2JXajg5dlJlNVYxODVHb20wUHdTbnpYdVdYZEdqdVlfVG9rZW46SzBoUGJiOG1Hb1J0ZkF4dTMyWWNBUzZVbkplXzE3NDk1NjgzMTY6MTc0OTU3MTkxNl9WNA)

记住script的type选module

# 4. 单文件导入vue

![](https://yx0zcbyal4l.feishu.cn/space/api/box/stream/download/asynccode/?code=OTRlNTY1ZGIzMjRkMGRhYmQzODE3Yzk1YTA5YTUwMjlfVzhQbnJCRE91MmNEdzd5WkM3eHlpbHRtZnVLMnV0UXVfVG9rZW46QTNvRWI5ZDlsb0Vta0N4RGtLbGN5cHNabktiXzE3NDk1NjgzMTY6MTc0OTU3MTkxNl9WNA)

script的type，选module，在填数据数据



# 5. 常用指令

![](https://yx0zcbyal4l.feishu.cn/space/api/box/stream/download/asynccode/?code=YWQ2NTA1MGJkMzJkMjM2ZWJiOGQ4NTBmYjlkYWY5ZWZfQ0lYeUJTRE5sT0ZKUEV5aGdVQ1RCYTZ5bVVObTBYWUdfVG9rZW46WUtTdWJCbE03b1doVjd4Y2pmd2NKblVzbnVoXzE3NDk1NjgzMTY6MTc0OTU3MTkxNl9WNA)

## 5.1 V-for

![](https://yx0zcbyal4l.feishu.cn/space/api/box/stream/download/asynccode/?code=ZTM1YTAzNzA3OTZhMjkwY2I3MTc5NzA0NDZjN2EwYWZfUEp6WW1tMHR5c01oa3RCajhOb1hNZkQ1ZkF1SG5GdFlfVG9rZW46SWpOQWJnQ3V6b2t3Umx4VW9vYWMwWXkxbm1kXzE3NDk1NjgzMTY6MTc0OTU3MTkxNl9WNA)



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
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
        import { createApp} from 
                'https://unpkg.com/vue@3/dist/vue.esm-browser.js'
        //创建应用实例
        createApp({
            data() {
                return {
                  //定义数据
                    articleList:[{
                                title:"医疗反腐绝非砍医护收入",
                                category:"时事",
                                time:"2023-09-5",
                                state:"已发布"
                            },
                            {
                                title:"中国男篮缘何一败涂地？",
                                category:"篮球",
                                time:"2023-09-5",
                                state:"草稿"
                            },
                            {
                                title:"华山景区已受大风影响阵风达7-8级，未来24小时将持续",
                                category:"旅游",
                                time:"2023-09-5",
                                state:"已发布"
                            }]  
                }
            }
        }).mount("#app")//控制页面元素
        
    </script>
</body>
</html>
```

## 5.2 V-bind

![](https://yx0zcbyal4l.feishu.cn/space/api/box/stream/download/asynccode/?code=OTg2NzE2NDkyM2ViYWYwMmI5MjgwYWFjZTQyMzA2ZGVfQ016OVZCWVpHU2MxRW1OZm1IZTJQRDNMODNaRVpxT3VfVG9rZW46UTlFY2JjWllGb3JEUWV4Z2F4RWNLbnl3bkNoXzE3NDk1NjgzMTY6MTc0OTU3MTkxNl9WNA)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app">
        <!-- <a v-bind:href="url">黑马官网</a> -->
        <a :href="url">黑马官网</a>
    </div>

    <script type="module">
        //引入vue模块
        import { createApp} from 
                'https://unpkg.com/vue@3/dist/vue.esm-browser.js'
        //创建vue应用实例
        createApp({
            data() {
                return {
                    url: 'https://www.itheima.com'
                }
            }
        }).mount("#app")//控制html元素
    </script>
</body>
</html>
```


