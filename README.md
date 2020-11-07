# 开发所需 ESLint等配置&Git 提交检验流

## 旧项目如何接入

1. 复制文件到项目根目录
    - .vscode vscode 的配置
    - .daojia-eslint-base.js
    - .eslintrc.js
    - .eslintignore.js
    - .editorconfig
    - .huskyrc
    - .lintstagedrc
2. 安装 npm 模块
    - eslint（如果项目已安装，注意更新版本，有些规则在某些低版本不存在会导致报错）
    - babel-eslint
    - vue-eslint-parser
    - eslint-plugin-vue
    - husky（node 版本必须为 8.6.0 以上，推荐安装 nvm 控制 node 版本）
    - lint-staged
3. VsCode 推荐安装以下插件

    - ESLint
    - Vetur
    - Prettier
    - EditorConfig

    ```json
    /**
     * VsCode 配置项
     *
     */
    {
        "editor.tabSize": 4, //制表符符号大小
        "eslint.autoFixOnSave": true, // 每次保存的时候将代码按eslint格式进行修复
        "prettier.eslintIntegration": true, //让prettier使用eslint的代码格式进行校验
        "prettier.semi": false, //去掉代码结尾的分号
        "prettier.printWidth": 200,
        "prettier.tabWidth": 4,
        "prettier.singleQuote": true, //使用单引号替代双引号
        "javascript.format.insertSpaceBeforeFunctionParenthesis": true, //让函数(名)和后面的括号之间加个空格
        "vetur.format.defaultFormatter.html": "js-beautify-html", //格式化.vue中html
        "vetur.format.defaultFormatter.js": "vscode-typescript", //让vue中的js按编辑器自带的ts格式进行格式化
        "vetur.validation.template": false,
        "vetur.format.defaultFormatterOptions": {
            "js-beautify-html": {
                "wrap_attributes": "force-aligned" //属性强制折行对齐
            }
        },
        // 错误高亮显示
        "eslint.validate": [
            "javascript",
            "javascriptreact",
            {
                "language": "html",
                "autoFix": true
            },
            {
                "language": "vue",
                "autoFix": true
            }
        ]
    }
    ```

## 新项目接入注意事项

项目最好先初始化为 git 项目，否则安装 husky 插件时，husky 无法找到.git/hooks 目录，导致 git 钩子添加失败，发生这种情况，请先把项目初始化为 git 项目后，再重新安装 husky 插件

## 文件介绍

### .daojia-eslint-base

eslint 通用规则配置

### .eslintrc.js

利用 eslint-plugin-vue 插件对 vue 语法进行规则限制

如果不需要 vue 配置，拷贝.daojia-eslint-base 文件到项目根目录，更名为.eslintrc.js

### .eslintignore

规避 eslint 检测某些文件夹或文件

### .editorconfig

编辑器配置，如果不想使用 eslint 的代码风格约束，可以使用此文件来格式化代码，编辑器需要安装 EditorConfig 插件

### .huskyrc

husky 会在.git/hooks 下添加钩子脚本，在进行 git 操作时，会触发相应的 git 钩子，然后执行配置的命令

### .lintstagedrc

只对暂存区的文件进行命令操作
问题：如果一个旧项目接入，之前已经 commit 的代码无法被检测到

## 说明文档

1. [ESLint 配置](http://confluence.daojia-inc.com/pages/viewpage.action?pageId=80924453)
2. [Git 检验流](http://confluence.daojia-inc.com/pages/viewpage.action?pageId=81353388)

## 参考文档

1. [ESLint 配置项](https://cn.eslint.org/docs/rules/)
2. [ESLint for Vue 配置项](https://github.com/vuejs/eslint-plugin-vue)
3. [EditorConfig 配置项](https://EditorConfig.org)
4. [Git 钩子](https://git-scm.com/book/zh/v2/%E8%87%AA%E5%AE%9A%E4%B9%89-Git-Git-%E9%92%A9%E5%AD%90)
5. [husky](https://github.com/typicode/husky)
6. [lint-staged](https://github.com/okonet/lint-staged)
7. [用 husky 和 lint-staged 构建超溜的代码检查工作流](https://zhuanlan.zhihu.com/p/27094880)

## tip

此规范只是个基础，如果需要的话可以自行修改配置（不建议修改等级为 error 的规则）
