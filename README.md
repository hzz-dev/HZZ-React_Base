# HZZ-React_Base

    React 构建用户界面的JavaScript库,主要用于构建UI界面, facebook出品 
      特点 :
       a. 声明式的设计 
       b. 高效 ,采用虚拟 DOM 来实现 DOM的 渲染 ,最大限度地减少 DOM 的操作  
       c. 灵活 ,跟其他库灵活搭配使用
       d. JSX ,俗称JS 里面写HTML  
       e. 组件化 ,模块化 ,代码容易服用 ,2016年之前大型项目喜欢使用 
       f. 单向数据流,没有实现双向数据流 ,数据 -》视图 -》事件-》数据 
        

一.创建项目 :
     官网 :https://react.docschina.org/

     1.通过 script 引入使用 
       <script crossorigin src="https://unpkg.com/react@16/umd/react.development.js"></script>
       <script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>

     2.通过react脚手架 .创建项目 开发 部署 
       安装脚手架 Create React App (cnpm/npm install -g create-react-app)
       创建项目 create-react-app my-app

二.React元素渲染 
    程序入口函数 
    ReactDOM.render(<App/>,document.getElementById('root')) //渲染 方法 ,函数 调用 (app组件(<App/>js对象 ) +元素的对象即最终渲染到的地方 )
      
     let h1 = <h1>helloworld</h1>
     使用 JPX的写法 .可以创建 JS元素对象
     案例使用:
        // react函数式组件开发
          function Clock(props) {
            return (
              <div>
                <h1>现在的时间是:{props.date.toLocaleTimeString()}</h1>
                <h2>这里是测试小标题</h2>
              </div>
            )
          }
          function run() {
            ReactDOM.render(
              <Clock date={new Date()} />,
              document.getElementById('root')
            )
          }
          setInterval(run, 1000)


