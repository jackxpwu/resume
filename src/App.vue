<template>
  <div id="app">
    <StyleEditor ref="styleEditor" :code="currentStyle"></StyleEditor>
    <ResumeEditor ref="resumeEditor" :markdown="currentMarkdown" :enableHtml="enableHtml"></ResumeEditor>
  </div>
</template>

<script>
  import StyleEditor from './components/StyleEditor'
  import ResumeEditor from './components/ResumeEditor'
  import './assets/reset.css'

  export default {
    name: 'app',
    components: {
      StyleEditor,
      ResumeEditor
    },
    data() {
      return {
        interval: 50,
        currentStyle: '',
        enableHtml: false,
        fullStyle: [
          `/*
* Hi!，你们好，先让我做个简单的自我介绍，
* 我叫吴新平，你们也可以叫我Jack，
* 江西师范大学软件学院2017届毕业生，
* 又是一年毕业季，希望能够找到一份满意的工作，
* 说做就做，让我我也来写一份简历吧！
*/

/* 首先给所有元素加上一个过渡效果 */
* {
  -webkit-transition: all .3s;
  transition: all .3s;
}
/* 白色背景似乎有点太单调了，让我们来点背景吧 */
html {
  color: rgb(222,222,222); background: rgb(0,43,54);
}
/* 文字看起来离边框有点太近了，我们来调整一下 */
.styleEditor {
  padding: .5em;
  border: 1px solid;
  margin: .5em;
  overflow: auto;
  width: 45vw; height: 90vh;
}
/* 代码看着不舒服？高亮处理一下或许会好一点 */
.token.selector{ color: rgb(133,153,0); }
.token.property{ color: rgb(187,137,0); }
.token.punctuation{ color: yellow; }
.token.function{ color: rgb(42,161,152); }

/* 再加点 3D 效果呗 */
html{
  -webkit-perspective: 1000px;
          perspective: 1000px;
}
.styleEditor {
  position: fixed; left: 0; top: 0;
  -webkit-transition: none;
  transition: none;
  -webkit-transform: rotateY(10deg) translateZ(-100px) ;
          transform: rotateY(10deg) translateZ(-100px) ;
}

/* 接下来我在右边给自己准备一个编辑器 */
.resumeEditor{
  position: fixed; right: 0; top: 0;
  padding: .5em;  margin: .5em;
  width: 48vw; height: 90vh;
  border: 1px solid;
  background: white; color: #222;
  overflow: auto;
}
/* 好了，我开始写简历了 */


`,
          `
/* 这个简历好像差点什么
 * 对了，这是 Markdown 格式的，我需要变成对 HR 更友好的格式
 * 简单，用开源工具翻译成 HTML 就行了
 */
`
          ,
          `
/* 再对 HTML 加点样式 */
.resumeEditor{
  padding: 2em;
}
.resumeEditor h2{
  display: inline-block;
  border-bottom: 1px solid;
  margin: 1em 0 .5em;
}
.resumeEditor ul,.resumeEditor ol{
  list-style: none;
}
.resumeEditor ul> li::before{
  content: '•';
  margin-right: .5em;
}
.resumeEditor ol {
  counter-reset: section;
}
.resumeEditor ol li::before {
  counter-increment: section;
  content: counters(section, ".") " ";
  margin-right: .5em;
}
.resumeEditor blockquote {
  margin: 1em;
  padding: .5em;
  background: #ddd;
}
`],
        currentMarkdown: '',
        fullMarkdown: `个人信息
姓名：吴新平 出生年月：1994年 04月
性别：男 政治面貌：中共党员
电话：131-3380-38182  邮箱：2315697257@qq.com
学历：本科 工作年限：1年

教育背景
2013.09–2017.06 江西师范大学 软件工程（本科）
主修课程：算法与数据结构、离散数学、数据库原理与设计、计算机网络、JavaScript程序设计

工作经历
麦肯光明广告有限公司（上海）
前端开发工程师 2017.03-2017.06
1、根据 UI 设计稿（psd/AI）进行页面制作（H5/Css3/Jquery/TweenmaxJs）; 2、配合程序进行代码调试、
bug 修复、浏览器兼容性调优（IE8+/Firefox/Chrome/Safari）; 3、使用 git 版本控制工具实现项目的多人
协作;
威比网络科技（上海）有限公司
前端开发工程师 2016.10-2017.03
vipabc 是全球首创全年365天、24小时在线英语教学机构。由美国硅谷核心科技团队研发，是一个优质且高
效的真人在线互动语言学习平台。高强度的工作经历让我抗压能力更强大，在公司，我主要负责：
1，负责公司 vipabc、vipjr、TutorABC 的 LandingPage 的制作、修改、上线，并且负责部分 Japan 的 LP 制
作。
2，EDM 制作
3，参与新品牌 vipjr 官网上线
4，参与公司新系统 LPGS（LP 自动生成系统）开发，负责部分 Component 开发

项目经验
s Vue.js  高仿饿了么外卖  App
项目开发 2017.05-2017.06
使用 Vue.js 结合 es6和 webpack 开发一款高仿饿了么外卖 app，使用 vue-resource 进行后端数据交互，使
用 vue-router 做前端路由，实现单页面应用，第三方 js 库 better- scroll 实现页面滚动，开发过程中采用
了 h5的 localstorge，图标字体的应用，移动端1像素边框，css sticky footer 布局，flex 弹性布局等
等，项目已上传至 github 主页。
基于 s Angular Js  的阅读类  Web app
前端页面开发，登录注册 2017.03-2017.05
本项目作为校答辩项目，基于 AngularJs 开发了一个移动阅读类 WebApp。项目分浏览、写作、登录三个模
块，我负责前端页面开发，使用了 Gulp+Bower 工具管理项目。使用 AngularJs+Less 语言，使用 Ajax+Json
模拟数据完成应用，项目已上传至 github 主页。
立顿 --- 茶觉奇遇 D 3D  世界
3D 场景搭建以及页面制作 2017.03-2017.03
本项目为立顿集团推出的赠饮活动，采用 C3D 构建 3D 场景，Orienter 横竖屏感应器打造重力感应效果。项
目成员共 4人，我负责 3D 场景的搭建以及页面制作，运用 js+css3模拟页面滑动效果。以下为项目链接：
http://craftww.cn/lipton_3d5h/debug.htm
基于 y Jquery  实现添加删除类清单小应用
项目开发实现 2017.01-2017.02
基于 Jquery 实现添加删除类清单小应用，采用 locastorage 存储数据，实现新增清单，删除清单以及清单
详情的修改和时间提醒功能，项目已上传至 github 主页。

技能清单
1、Web开发：
H5/Css3/JavaScript/AngularJs/Ajax/Jquery/Json/Bootstrap/TweenmaxJs/Xml/Less/Gulp/Bower
2、前端工具：phpStorm/sublime/nodepad++
3、切图工具：AI/PS
4、版本管理工具：Git/SourceTree

自我描述
朋友都說我是一個有干劲有好学的人。我有作为技术人员的傲气，也有一股"拼"的精神。我从来不怕遇到技
术上的难题,也不怕自己跟不上技术的潮流。我热爱技术，渴望技术，我的 Js 基础扎实,不仅掌握 VueJs 等
新技术，还会继续学习 Node.js 等服务器端语言。細心和耐心是我的优点，如果貴公司也想要功底扎实的
我，我很荣幸收到您的面试邀请。

`
      }
    },
    created() {
      this.makeResume()
    },

    methods: {
      makeResume: async function () {
        await this.progressivelyShowStyle(0)
        await this.progressivelyShowResume()
        await this.progressivelyShowStyle(1)
        await this.showHtml()
        await this.progressivelyShowStyle(2)
      },
      showHtml: function () {
        return new Promise((resolve, reject) => {
          this.enableHtml = true
          resolve()
        })
      },
      progressivelyShowStyle(n) {
        return new Promise((resolve, reject) => {
          let interval = this.interval
          let showStyle = (async function () {
            let style = this.fullStyle[n]
            if (!style) { return }
            // 计算前 n 个 style 的字符总数
            let length = this.fullStyle.filter((_, index) => index <= n).map((item) => item.length).reduce((p, c) => p + c, 0)
            let prefixLength = length - style.length
            if (this.currentStyle.length < length) {
              let l = this.currentStyle.length - prefixLength
              let char = style.substring(l, l + 1) || ' '
              this.currentStyle += char
              if (style.substring(l - 1, l) === '\n' && this.$refs.styleEditor) {
                this.$nextTick(() => {
                  this.$refs.styleEditor.goBottom()
                })
              }
              setTimeout(showStyle, interval)
            } else {
              resolve()
            }
          }).bind(this)
          showStyle()
        })
      },
      progressivelyShowResume() {
        return new Promise((resolve, reject) => {
          let length = this.fullMarkdown.length
          let interval = this.interval
          let showResume = () => {
            if (this.currentMarkdown.length < length) {
              this.currentMarkdown = this.fullMarkdown.substring(0, this.currentMarkdown.length + 1)
              let lastChar = this.currentMarkdown[this.currentMarkdown.length - 1]
              let prevChar = this.currentMarkdown[this.currentMarkdown.length - 2]
              console.log(prevChar)
              if (prevChar === '\n' && this.$refs.resumeEditor) {
                this.$nextTick(() => this.$refs.resumeEditor.goBottom())
              }
              setTimeout(showResume, interval)
            } else {
              resolve()
            }
          }
          showResume()
        })
      }
    }
  }

</script>

<style scoped>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  html {
    min-height: 100vh;
  }

  * {
    -webkit-transition: all .3s;
    transition: all .3s;
  }
</style>
