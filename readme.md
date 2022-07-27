### 使用vite搭建项目

执行以下指令（本项目只用pnpm包管理工具）,然后根据提示选择就可以了

```
使用pnpm
pnpm create vite

使用yarn
yarn create vite

使用npm
 npm create vite@latest
```

### Eslint

##### 安装Eslint及相应的插件

```
pnpm i -D eslint eslint-config-airbnb eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-react eslint-plugin-react-hooks

```

为了避免我们自己按照 Eslint 的规则一个一个来个性化定制规则，可以引用可以使用[Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)规范来定义规则。这就需要安装如下插件,详情看[npm安装说明](https://www.npmjs.com/package/eslint-config-airbnb)

```
eslint-plugin-import, eslint-plugin-react, eslint-plugin-react-hooks, and eslint-plugin-jsx-a11y
```

##### 创建eslint 配置文件

执行一下代码，然后根据项目选择你想要的配置就可以了，最后会生成.eslintrc.json文件

```
pnpm create @eslint/config
```

在.eslintrc.json文件中可以添加一些配置

```
//设置react版本自动检测
settings: {
    react: {
      version: 'detect'
    }
  },
```

```
//定义检查规则
rules:{
   'prettier/prettier': 'off',
    quotes: ['error', 'single'],
    'react/react-in-jsx-scope': 'off',
    'react/prop-types': 'off',
    '@typescript-eslint/no-empty-function': 'error',
    '@typescript-eslint/no-empty-interface': 'error',
    '@typescript-eslint/no-explicit-any': 'error',
    '@typescript-eslint/no-inferrable-types': 'error',
    '@typescript-eslint/no-misused-new': 'error',
    '@typescript-eslint/no-unused-vars': 'error',
    '@typescript-eslint/no-unsafe-assignment': 'off',
    '@typescript-eslint/await-thenable': 'warn',
    '@typescript-eslint/no-floating-promises': 'warn',
    '@typescript-eslint/no-unnecessary-type-assertion': 'error',
    '@typescript-eslint/no-unsafe-argument': 'error',
    '@typescript-eslint/no-unsafe-call': 'off',
    '@typescript-eslint/explicit-function-return-type': 'off',
    '@typescript-eslint/member-delimiter-style': 'off',
    '@typescript-eslint/strict-boolean-expressions': 'off',
    '@typescript-eslint/no-misused-promises': 'off',
    '@typescript-eslint/space-before-function-paren': 'off',
    '@typescript-eslint/restrict-template-expressions': 'off',
    '@typescript-eslint/no-extraneous-class': 'off'
}
```

在写jsx时会要求导入react，报错'React' must be in scope when using JSX，为了避免未导入react报错，可以在extends上加一下配置, 当然不嫌麻烦的话可以自己导入一下。

```
"extends":[
"plugin:react/jsx-runtime"
]
```

##### 忽略不必要的文件检查

在根目录下新建`.eslintignore`文件，加入需要忽略检查的文件

```
.vscode
dist
node_modules/
.editorconfig
.eslintignore
.eslintrc
.gitignore
.prettierrc
index.html
```

## prettier

```
pnpm install prettier --save-dev --save-exact
```

最外层文件夹下新增.prettierrc文件，配置一些常用属性：

```
{
 printWidth: 120, //一行的字符数，如果超过会进行换行，默认为80
  tabWidth: 4, // 一个 tab 代表几个空格数，默认为 2 个
  useTabs: false, //是否使用 tab 进行缩进，默认为false，表示用空格进行缩减
  singleQuote: true, // 字符串是否使用单引号，默认为 false，使用双引号
  trailingComma: "none", // 是否使用尾逗号
}
```

##### 添加**.prettierignore**忽略无需检查的文件

```
build
```

##### 解决prettier会和eslint冲突

prettier会和eslint规则产生冲突 ，需添加以下配置

```
pnpm install eslint-config-prettier eslint-plugin-prettier --save-dev
```

并且在`.eslintrc.json`文件里添加以下配置：

```
extends: [
	...
    'prettier',
    'plugin:prettier/recommended'
    ...
  ]
```

# stylelint

```
pnpm add stylelint stylelint-config-standard -D
```

在根目录下生成stylelint.js文件，初始化配置规则

```
module.exports = {
    // 注册 stylelint 的 prettier 插件
    plugins: ['stylelint-prettier'],
    // 继承一系列规则集合
    extends: [
      // standard 规则集合
      'stylelint-config-standard',
      // 样式属性顺序规则
      'stylelint-config-recess-order',
      // 接入 Prettier 规则
      'stylelint-config-prettier',
      'stylelint-prettier/recommended'
    ],
    // 配置 rules
    rules: {
      // 开启 Prettier 自动格式化功能
      'prettier/prettier': true
    }
  };

```

