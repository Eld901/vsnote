# a6_03_DOC_Docsify  
`Created on 20240725 | Updated on 20240725`  
#### Docsify  
##### URL  
Docsify：https://docsify.js.org/#/zh-cn/  
Docsify教程：https://www.bilibili.com/video/BV1kT4y1T7wY/  
##### (1)安装和初始化  
1. 安装node.js  
npm环境  
2. 安装docsify  
`npm i docsify-cli -g`  
3. 初始化docsify  
`docsify init`  
4. 运行docsify  
`docsify serve`  
5. 创建文件  
`docsify init docsname`  
6. 本地预览  
`docsify serve docsname`  
http://localhost:3000  
##### (2)页面路径格式  
```js
* [首页](/)
* [指南](guide.md)

* 目录
  * [js](01/js/js.md)
  * [ec](01/ec/ec.md)

// 路径：01文件夹下，js文件夹下的，js.md文件  
// 提示：如果文件夹下只有一个README.md文件，则可以省略js.md文件，直接写js文件夹即可  
```
##### (3)预制页和属性  
```html
<!-- index.html 

  普通页面：`xxx.md`  
  封面页：`coverpage.md`  
  侧边栏：`_sidebar.md`  
  导航栏：`_navbar.md`  
  
  侧边栏：`loadSidebar:true`  
  导航栏：`loadNavbar:true`  
  封面页：`coverpage: true`  
  独立封面：`onlyCover:false`  
  目录层级：`subMaxLevel: 3`   
-->
<script>
    window.$docsify = {
      name: '',
      repo: '',
      loadSidebar:true,
      loadNavbar:true,
      subMaxLevel: 3
    }
</script>
```
##### (4)文档发布流程  
1. 密钥连接  
在本地生成一对密钥，公钥和私钥；公钥配置到github，私钥本地存储在.ssh文件夹；  
验证链接，本地仓库和github仓库建立连接后，clone和push操作就不用每次登录验证密码。  
(1)生成密钥`ssh-keygen -t rsa -C "<email>"`  
(2)查看密钥`cat id_rsa.pub`  
(3)验证链接`ssh -T git@github.com`  
2. 发布流程  
(1)新建仓库，仓库命名"name.github.io"；  
(2)克隆仓库`git clone <path>`，复制docsify文件到仓库根目录；  
(3)`git add .` `git commit -m xxx` `git push`提交到github  

