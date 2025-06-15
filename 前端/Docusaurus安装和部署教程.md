# Docusaurus 安装与 GitHub Pages 部署完全指南

Docusaurus 是一个由 Facebook 开源的、用于轻松构建、部署和维护开源项目文档网站的静态站点生成器。本教程将引导您完成从安装 Docusaurus 到最终将其部署到 GitHub Pages 的全过程。

## 1. 环境准备

在开始之前，请确保您的开发环境中已安装 **Node.js**。Docusaurus 要求 Node.js 版本为 **18.0 或更高**。

您可以在终端中运行以下命令来检查您的 Node.js 版本：

```bash
node -v
```

如果未安装或版本过低，请访问 [Node.js 官网](https://nodejs.org/) 下载并安装最新稳定版。

## 2. 安装 Docusaurus

安装 Docusaurus 最简单的方式是使用官方提供的脚手架命令。该命令会自动创建一个包含基本结构和示例内容的网站目录。

打开终端，执行以下命令：

```bash
npx create-docusaurus@latest my-website classic
```

- `my-website` 是您的项目目录名，您可以替换成任何您喜欢的名字。
- `classic` 是官方推荐的模板，它包含了文档、博客、自定义页面和 CSS 框架（支持暗黑模式）等常用功能，非常适合快速上手。

命令执行完毕后，您的项目目录 `my-website` 就创建好了。

## 3. 本地运行开发服务器

进入项目目录，并启动本地开发服务器来预览您的网站。

```bash
cd my-website
npm run start
```

该命令会启动一个本地服务器（通常在 `http://localhost:3000`），并自动在浏览器中打开。当您修改项目中的文件时，网站会自动刷新，非常便于开发和调试。

恭喜！您已经成功在本地运行了您的第一个 Docusaurus 网站。

## 4. 部署到 GitHub Pages

现在，我们将把这个网站部署到互联网上，以便任何人都可以访问。我们将使用 GitHub 提供的免费静态托管服务——GitHub Pages。

### 步骤 4.1: 创建 GitHub 仓库

1.  登录您的 GitHub 账号。
2.  创建一个新的**公共**（Public）仓库。仓库名可以任意，但为了方便，推荐使用 `your-username.github.io` 或者 `project-name` 这样的格式。

### 步骤 4.2: 将本地项目推送到 GitHub

首先，将您的 Docusaurus 项目代码推送到刚刚创建的 GitHub 仓库。

在您的项目根目录（例如 `my-website`）下执行以下命令：

```bash
git init
git add .
git commit -m "Initial commit: Docusaurus site setup"
git branch -M main
git remote add origin https://github.com/your-username/your-repository.git
git push -u origin main
```

**请务必将 `your-username` 和 `your-repository` 替换为您自己的 GitHub 用户名和仓库名。**

### 步骤 4.3: 配置 `docusaurus.config.js`

为了让 Docusaurus 知道要部署到哪里，您需要修改项目根目录下的 `docusaurus.config.js` 文件。

打开该文件，找到并修改以下几个关键配置项：

```javascript
// docusaurus.config.js

const config = {
  // ... 其他配置

  // -- 为部署到 GitHub Pages 修改以下字段 --

  // 1. 设置您网站的 URL
  url: 'https://your-username.github.io', 
  // 2. 设置 Base URL
  //    如果您的仓库是 your-username.github.io, baseUrl 保持 '/'
  //    如果您的仓库名是 project-name, baseUrl 应为 '/project-name/'
  baseUrl: '/your-repository/',

  // 3. 部署配置
  organizationName: 'your-username', // 您的 GitHub 用户名
  projectName: 'your-repository', // 您的仓库名
  trailingSlash: false, // 建议为 GitHub Pages 设置

  // ... 其他配置
};
```

**配置说明:**

-   `url`: 您的 GitHub Pages 站点的根 URL。例如 `https://facebook.github.io`。
-   `baseUrl`: 您网站的路径。
    -   如果您的仓库是专门的用户/组织站点（`your-username.github.io`），则 `baseUrl` 设置为 `/`。
    -   如果您的仓库是项目站点（例如 `my-project`），则 `baseUrl` 设置为 `/'my-project/'`。
-   `organizationName`: 拥有该仓库的 GitHub 用户或组织名。
-   `projectName`: 您的 GitHub 仓库名。

### 步骤 4.4: 添加 `.nojekyll` 文件

GitHub Pages 默认会使用 Jekyll 来处理文件。为了防止它忽略以下划线 `_` 开头的文件（Docusaurus 构建后会生成此类文件），您需要在 `static` 目录下创建一个名为 `.nojekyll` 的空文件。

```bash
touch static/.nojekyll
```

然后将这个改动也提交到 GitHub。

```bash
git add static/.nojekyll
git commit -m "Add .nojekyll to disable Jekyll"
git push
```

### 步骤 4.5: 执行部署命令

Docusaurus 提供了一个便捷的部署命令，它可以自动完成构建网站、创建 `gh-pages` 分支并推送文件的所有操作。

在项目根目录下运行：

```bash
GIT_USER=your-username npm run deploy
```

-   将 `your-username` 替换为您的 GitHub 用户名。
-   此命令会创建一个名为 `gh-pages` 的新分支，该分支仅包含构建好的静态网站文件（位于 `build` 目录）。

### 步骤 4.6: 设置 GitHub Pages 源

最后一步是在您的 GitHub 仓库设置中启用 GitHub Pages。

1.  打开您的 GitHub 仓库页面。
2.  点击 `Settings` (设置)。
3.  在左侧导航栏中，选择 `Pages`。
4.  在 `Build and deployment` -> `Source` 部分，选择 `Deploy from a branch`。
5.  在 `Branch` 部分，将分支从 `main` 切换到 `gh-pages`，并将文件夹保持为 `/(root)`。
6.  点击 `Save`。

![img](https://secure2.wostatic.cn/static/9tg6hPsGSM5qLWcX2DhgKc/image.png?auth_key=1749978233-2MoeqEwbBKngGznfCDVVHn-0-452f03f25be6e43f16c2cfec3183fd85)

![img](https://secure2.wostatic.cn/static/9tg6hPsGSM5qLWcX2DhgKc/image.png?auth_key=1749978241-jYPugmNxZPPCgqga23VkHr-0-c74b1f4ac90692a8a2f6c3d5636e67d5)

1.  ![img](https://yx0zcbyal4l.feishu.cn/space/api/box/stream/download/asynccode/?code=YjAwYWRkYjlkOTUyMGEzOTdjNWIxZjIzNGVjMmEwZGNfbVVFcWlBZmcydUprOW1IR1lveElhVnhBMWZ6U3ZyTGtfVG9rZW46T0RoSmJ4Q0Jpb3ZzOUR4b0t5RmNWc3ZVbkxlXzE3NDk5Nzc0OTI6MTc0OTk4MTA5Ml9WNA)

    ![img](https://x0zcbyal4l.feishu.cn/space/api/box/stream/download/asynccode/?code=MTVjZGI5ZGE4ZDQ0MGIwNTZjZDZkOGYwYzE3OWI4MjJfc0JXUzZ3TjRDczdGbVp1MTdGVFV1QjhmdGRlZUlKQmxfVG9rZW46V3hwcWJjaERYb0Z0ek14c3hEVGNyNFRBblhnXzE3NDk5Nzc0OTI6MTc0OTk4MTA5Ml9WNA)

等待几分钟，GitHub Pages 完成部署后，您就可以通过 `https://your-username.github.io/your-repository/` 访问您的网站了！

## 5. (可选) 使用 GitHub Actions 自动化部署

每次更新网站后都手动运行 `deploy` 命令比较繁琐。我们可以使用 GitHub Actions 来实现自动化：每当 `main` 分支有新的提交时，就自动执行部署流程。

1.  在您的项目根目录下，创建 `.github/workflows` 目录：

    ```bash
    mkdir -p .github/workflows
    ```

2.  在该目录下创建一个名为 `deploy.yml` 的文件，并添加以下内容：

    ```yaml
    # .github/workflows/deploy.yml
    name: Deploy to GitHub Pages

    on:
      push:
        branches:
          - main
      pull_request:
        branches:
          - main

    jobs:
      build:
        name: Build Docusaurus
        runs-on: ubuntu-latest
        steps:
          - uses: actions/checkout@v4
            with:
              fetch-depth: 0
          - uses: actions/setup-node@v4
            with:
              node-version: 18
              cache: npm

          - name: Install dependencies
            run: npm ci
          - name: Build website
            run: npm run build

          - name: Upload Build Artifact
            uses: actions/upload-pages-artifact@v3
            with:
              path: build

      deploy:
        name: Deploy to GitHub Pages
        if: github.event_name == 'push' # 只在 push 事件时执行部署
        needs: build
        permissions:
          pages: write
          id-token: write
        environment:
          name: github-pages
          url: ${{ steps.deployment.outputs.page_url }}
        runs-on: ubuntu-latest
        steps:
          - name: Deploy to GitHub Pages
            id: deployment
            uses: actions/deploy-pages@v4
    ```

3.  将这两个新文件提交到您的 GitHub 仓库。

    ```bash
    git add .github/workflows/deploy.yml
    git commit -m "Add GitHub Actions workflow for deployment"
    git push
    ```

现在，每当您向 `main` 分支推送新的提交时，GitHub Actions 都会自动构建和部署您的 Docusaurus 网站。您可以在仓库的 `Actions` 标签页查看部署进度。

---

至此，您已经掌握了 Docusaurus 的安装、本地��发和自动化部署到 GitHub Pages 的完整流程。祝您使用愉快！

```vue
	<!-- <script>
  //写数据
  export default{
    data(){
      return {
        msg:'上海'
      }
    }
  }
</script> -->
<script setup>
  import {ref} from 'vue';
  //调用ref函数,定义响应式数据
  const msg = ref('西安');

  //导入 Api.vue文件
  import ApiVue from './Api.vue'
  //导入Article.vue文件
  import ArticleVue from './Article.vue'
</script>

<template>
  <!-- html -->
  <!-- <h1>北京</h1> -->
  <!-- <h1>{{ msg }}</h1>
  <br>
  <ApiVue/> -->

  <ArticleVue/>
</template>

<style scoped>
  /* 样式 */
  h1{
    color: red;
  }
</style>
```
![](assets/Pasted%20image%2020250615171501.png)