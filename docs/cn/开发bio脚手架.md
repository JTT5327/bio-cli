# 开发bio脚手架

## 原理

+   bio 通过 npm 获取脚手架及拉取更新。
+   bio 会将业务目录的文件同步到脚手架目录的 `workspace` 目录。

    这样做的目的是保证业务代码始终位于脚手架目录的子级（[为什么要保证父子关系?](https://github.com/hoperyy/deep-webpack/issues/8)）。

## 从零创建一个脚手架

使用命令：`bio scaffold create`

该命令会初始化一个脚手架 demo 供后续开发。

## 查看安装过的脚手架

使用命令：`bio scaffold show <脚手架名称>`

此命令用于查看脚手架。
    
例如：`bio scaffold show xxx` 命令会帮你打开 `xxx` 脚手架目录，并在终端展示该目录路径。

## 脚手架对接 BIO

+   第一步：创建文件 `bio-entry.js`

    bio 通过 `bio-entry.js` 启动脚手架，规范格式如下：

    `context` 为 `bio` 回传的参数对象，上面挂载了几个参数。
        
    ```javascript
    require('bio-helper')(process)((context) => {
        /* 
         * context: {Object}
         * context.userDir: {String} 业务目录路径
         * context.srcDir: {String} 业务目录在脚手架副本里的路径（bio 会将当前目录文件同步到脚手架目录内，用于编译）
         * context.distDir: {String} 当前项目编译结果的目录路径
         * context.taskName: {String} 用户启动脚手架的任务，例如 bio run daily 命令运行后，context.taskName 即为 daily
         * context.port: {Number} bio 提供的调试端口号，默认 9000，如该端口被占用，会自增 1 直到找到空闲的端口号
         */
        
         // 代码
         switch(context.taskName) {
            case 'daily':
                break;
            case 'pre':
                break;
            case 'prod':
                break;
            default:
                console.log(`${content.taskName} is not supported!`);
                break;
         }
    });
    ```

+   第二步：创建项目 demo 模板 `project-template`

    该目录是 bio 初始化项目时拉取的 demo 模板目录，支持多个模板，写法如下：

    +   只支持一个模板

        `project-template/default/...`

    +   支持 mobile 和 pc 两种模板

        +   `project-template/mobile/...`
        +   `project-template/pc/...`