---
description: 本文记录一次搭建angular项目的过程，
---

# angular项目搭建

前置条件，已安装 node 和 git 

## 创建项目

1. 全局安装 angular-cli： `npm install -g @angular/cli`  安装成功用  `ng version` 查看版本；
2. 创建项目： `ng new project-name`；  
3. 运行项目：  `ng serve --open` 直接在浏览器打开项目  `ng serve --port 4000` 更改端口号，用于多个 angular 项目同时在本地运行  `ng serve --host 192.168.31.203` 用本机 IP 运行项目，使同事可以在局域网内访问你的本地项目

## 常用命令

| 命令 | 描述 |
| :--- | :--- |
| ng new  \[ name \]  --style=scss | 新建项目且样式文件使用 scss  |
| ng g c  modules/home \[ name \] | 在指定目录下新建组件，根目录是 app 文件夹 |
| ng g c  \[ name \]  --no-spec | 新建不带单元测试文件的组件 |
| ng g c  \[ name \]  --style=scss | 新建样式组件为 scss 的组件 |
| ng g m \[ name \]  --routing | 新建带路由的module |
| ng g  s  \[ name \] | 新建服务 |
| ng g  p  \[ name \] | 新建管道 |
| ng g  d  \[ name \] | 新建指令 |
| ng g  e  \[ name \] | 新建枚举 |

## 目录架构

```c
📦src
 ┣ 📂app
 ┃ ┣ 📂modules
 ┃ ┣ 📂scss
 ┃ ┃ ┣ 📜main.scss
 ┃ ┃ ┗ 📜_common-values.scss
 ┃ ┣ 📂services
 ┃ ┃ ┗ 📜request.service.ts
 ┃ ┣ 📂shared
 ┃ ┃ ┣ 📂components
 ┃ ┃ ┣ 📂modals
 ┃ ┃ ┣ 📂pipes
 ┃ ┃ ┗ 📜shared.module.ts
 ┃ ┣ 📜app-routing.module.ts
 ┃ ┣ 📜app.component.html
 ┃ ┣ 📜app.component.scss
 ┃ ┣ 📜app.component.ts
 ┃ ┗ 📜app.module.ts
 ┣ 📂assets
 ┃ ┣ 📂fonts
 ┃ ┗ 📂images
 ┗ 📜index.html
```

## 引入三方库

### 引入 sass

新建项目时直接指定样式为 scss， `ng new project --style=scss`

公共的 scss 文件可以全部导入到一个 main.scss 文件中，然后在 angular.json 中引入

```javascript
// angular.json
"architect": {
  "build": {
  "builder": "@angular-devkit/build-angular:browser",
  "options": {
      "styles": [
          "src/styles.scss",
          "src/app/scss/main.scss"
        ]
      }
    }
  }
```

引入 angular-bootstrap

1. 在项目中安装 bootstrap： npm install bootstrap;
2. 安装 angular-bootstrap：npm install ngx-bootstrap;
3. 
在 angular 中引入 angular-bootstrap 样式库

引入 icon-font

引入 echarts

如果你的项目中不需要单元测试，那么可以在

