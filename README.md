# 学习 Ant Design Pro V5

##项目搭建

1.创建脚手架/选择

    ant-design-pro 模板
    npm/yarn create umi

2.创建本地仓库

    git init

3.添加到 code .是所有的意思

    git add .

4.描述信息

    git commit -m "描述"

5.链接远程仓库

    git remote add origin 你的远程库地址

6.更新分支记录

    git pull origin main --allow-unrelated-histories

7.推送远程仓库

    git push -u origin main -f

8.安装模块

    npm/yarn isntall

9.项目启动

    npm run start

10.代理服务

    npm run start:test

##官网文档

UmiJavaScript - https://umijs.org/zh-CN/docs

ant-design.pro - https://pro.ant.design/index-cn

Ant.design.pro V5 - https://beta-pro.ant.design/docs/overview-cn

ProComponents - https://procomponents.ant.design/

##项目目录

    ├── config                   # umi 配置，包含路由，构建等配置
    ├── mock                     # 本地模拟数据
    ├── public
    │   └── favicon.png          # Favicon
    ├── src
    │   ├── assets               # 本地静态资源
    │   ├── components           # 业务通用组件
    │   ├── e2e                  # 集成测试用例
    │   ├── layouts              # 通用布局
    │   ├── models               # 全局 dva model
    │   ├── pages                # 业务页面入口和常用模板
    │   ├── services             # 后台接口服务
    │   ├── utils                # 工具库
    │   ├── locales              # 国际化资源
    │   ├── global.less          # 全局样式
    │   └── global.ts            # 全局 JS
    ├── tests                    # 测试工具
    ├── README.md
    └── package.json

##项目配置-config 项目的路由,打包,服务,都是在这里配置

      配置目录
      ├── config.dev.ts            # webpack配置
      ├── config.ts                # 项目配置
      ├── defaultSettings.ts       # 主题UI配置
      ├── routes.ts                # 路由配置
      ├── proxy.ts                 # 代理服务配置

###路由-routes

配置式路由:配置路由通过配置生成对应的路由, 详情配置：https://umijs.org/zh-CN/docs/routing

```js
[
  {
    path: '/user', //路由URL
    layout: false, //关闭布局
    routes: [
      //二级路由
      {
        path: '/user', //路由URL
        routes: [
          {
            name: 'login', //页面标题名称
            path: '/user/login', //
            component: './user/Login', //页面相对路径
          },
        ],
      },
    ],
  },
];
```

约定式路由:约定式路由也叫文件路由，就是不需要手写配置，文件系统即路由，通过目录和文件及其命名分析出路由配置， 如果没有 routes 配置，Umi 会进入约定式路由模式，然后分析 src/pages 目录拿到路由配置。 ###代理配置-proxy

使用 npm run start:代理名称,只会在生成环境有效 详情配置：https://umijs.org/zh-CN/docs/routing

```js
export default {
  dev: {
    //代理名称
    '/api/': {
      //如果是 api 就转发到下面这个地址
      target: 'https://preview.pro.ant.design',
      changeOrigin: true,
      pathRewrite: { '^': '' },
    },
  },
  test: {
    //代理名称
    '/api/': {
      target: 'https://preview.pro.ant.design',
      changeOrigin: true,
      pathRewrite: { '^': '' },
    },
  },
  pre: {
    //代理名称
    '/api/': {
      target: 'your pre url',
      changeOrigin: true,
      pathRewrite: { '^': '' },
    },
  },
};
```

###项目主题项目的主题色,布局,网站标题配置

```js
import { Settings as LayoutSettings } from '@ant-design/pro-layout';

const Settings: LayoutSettings & {
  pwa?: boolean,
  logo?: string,
} = {
  navTheme: 'light',
  // 拂晓蓝
  primaryColor: '#1890ff',
  //布局类型
  layout: 'mix',
  contentWidth: 'Fluid',
  fixedHeader: false,
  fixSiderbar: true,
  colorWeak: false,
  title: 'Ant Design Pro',
  pwa: false,
  //logoURL
  logo: 'https://gw.alipayobjects.com/zos/rmsportal/KDpgvguMpGfqaHPjicRK.svg',
  iconfontUrl: '',
};

export default Settings;
```

###配置

##伪数据-MOCK 能够开启一个小的 web 服务,如 POST,GET 的请求 详情：https://umijs.org/zh-CN/docs/mock

```js
export default {
  // 支持值为 Object 和 Array
  'GET /api/users': { users: [1, 2] },

  // GET 可忽略
  '/api/users/1': { id: 1 },

  // 支持自定义函数，API 参考 express@4
  'POST /api/users/create': (req, res) => {
    // 添加跨域请求头
    res.setHeader('Access-Control-Allow-Origin', '*');
    res.end('ok');
  },
};
```
