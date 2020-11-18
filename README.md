# HZZ-React_Base

React 构建用户界面的JavaScript库,主要用于构建UI界面, facebook出品 
特点 :
1.声明式的设计 
2.高效 ,采用虚拟 DOM 来实现 DOM的 渲染 ,最大限度地减少 DOM 的操作  
3.灵活 ,跟其他库灵活搭配使用
4.JSX ,俗称JS 里面写HTML  
5.组件化 ,模块化 ,代码容易服用 ,2016年之前大型项目喜欢使用 
6.单向数据流,没有实现双向数据流 ,数据 -》视图 -》事件-》数据 

1.创建项目 :
官网 :https://react.docschina.org/
 
1.通过 script 引入使用 
<script crossorigin src="https://unpkg.com/react@16/umd/react.development.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>

2.通过react脚手架 .创建项目 开发 部署 
 安装脚手架 Create React App (cnpm/npm install -g create-react-app)
 创建项目 create-react-app my-app

2.React元素渲染 
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

3.React_JSX
1.jsx执行更快 ,编译为javascript代码时进行优化 
2.类型更安全 ,编译过程如果出错就不能编译 ,及时发现错误 

注意 :
1.jsx必须要有根节点  
2.正常的普通 HTML 元素要小写 ,如果大写默认为组件 

JSX表达式 

1.由HTML元素构成 
2.中间如果需要插入变量用{}
3.{}中间可以使用表达式 
4.{}中间表达式中可以使用 JSX 对象 
5.属性和 html 内容一样都是可以用{}插入内容 

4.JSX  style样式 

1.class,style中 ,不可以存在多个 class 属性
2.style样式中,如果存在多个单词的属性,第二个字母之后首字母大写 或者 用引号引起来
3.多个类共存
let classStr2 = ['abc2', 'redbg2'].join(" ")
let element2 = (
  <div>
    <h1 className={classStr2}>helloworld</h1>
  </div>
)
或者 
let exampleStyle = {
  background: "blue",
  borderBottom: "1px solid red"
}
let element = (
  <div>
    <h1 style={'abc2'+exampleStyle}>helloworld</h1>
  </div>
)

  
5.React组件 

函数式组件与类组件的区别和使用 ,函数式比较简单 ,一般用于静态没有交互事件内容的组件页面 .类组件 ,一般又称为动态组件 ,那么会有交互或者数据修改操作 .
 
1.函数式组件 (数据定死的使用静态组件函数组件  )
1).不含参
function Childcom() {
  let title = <h2>我是副标题</h2>
  let weather = 24
  // 条件判断
  let isGo = weather > 23 ? '出门' : '不出门'
  // return 构造函数
  return (
    <div>
      <h1>hello,world</h1>
      {/* 变量 */}
      {title}
      <div>
        是否出门?
        <span>{isGo}</span>
      </div>
    </div>
  )
}
ReactDOM.render(<Childcom />, document.getElementById('root'))

2).带参数
function Childcom(props) {
  console.log(props)
  let title = <h2>我是副标题</h2>
  let weather = props.weather
  // 条件判断
  let isGo = weather > 23 ? '出门' : '不出门'
  // return 构造函数
  return (
    <div>
      <h1>hello,world</h1>
      {/* 变量 */}
      {title}
      <div>
        是否出门?
        <span>{isGo}</span>
      </div>
    </div>
  )
}
ReactDOM.render(<Childcom weather='22' />, document.getElementById('root'))
2.类组件定义 (如果有点击事件/触发事件等有动态修改数据的使用类组件)
1).不含参
class HelloWord extends React.Component {
  // 继承
  // 类组件渲染需要用render方法
  render() {
    return (
      <div>
        <h1>类组件定义</h1>
      </div>
    )
  }
}
ReactDOM.render(<HelloWord />, document.getElementById('root'))
 类组件中嵌套组件+传值(复合组件:既可以有类组件 又可以有函数组件  )
class HelloWord extends React.Component {
  // 继承
  // 类组件渲染需要用render方法
  render() {
    console.log(this)
    return (
      <div>
        <h1>类组件定义HELLOWORLD</h1>
        <Childcom weather={this.props.weather} />
        <h2>{this.props.test}</h2>
      </div>
    )
  }
}
ReactDOM.render(<HelloWord test='这是一个自己添加的参数' weather='25' />, document.getElementById('root'))

6.React State状态 
相当于 vue的 Data,使用方式与vue不一样 
class ClockClass extends React.Component {
  // 构造函数
  constructor(props) {
    // 这样会将传递过来的props数据一直传到继承的React.Component类
    super(props)
    // 状态(数据)-->决定view(视图)
    // 构造函数初始化内容,将需要改变的内容初始到state中
    this.state = {
      time: new Date().toLocaleTimeString()
    }
  }
  //生命周期函数 ,组件渲染完成时的函数
  componentDidMount() {
    setInterval(() => {
      // this.setState修改time对象的值渲染对象和微信小程序语法类似
      // 通过this.setState修改完数据后,并不会修改DOM里面的内容,react会在,这个函数内容所有设置状态改变后,统一对比虚拟DOM对象,然后再统一修改,提升性能
      this.setState({
        time: new Date().toLocaleTimeString()
      })
    }, 1000)
  }
  //  视图部分渲染
  render() {
    // this.state.time = new Date().toLocaleTimeString()
    return (
      <div>
        <h1>当前时间:{this.state.time}</h1>
      </div>
    )
  }
}
ReactDOM.render(<ClockClass />, document.getElementById('root'));
案例 :绑定按钮事件
class Tab extends React.Component {
  constructor(props) {
    super(props)
    // 设置状态,数据
    this.state = {
      c1: 'content active',
      c2: 'content'
    }
    this.clickEvent = this.clickEvent.bind(this)
  }
  clickEvent(e) {
    console.log('内容1')
    console.log(e.target)
    let index = e.target.dataset.index
    if (index == 1) {
      this.setState = ({
        c1: 'content active',
        c2: 'content'
      })
    } else {
      this.setState = ({
        c1: 'content ',
        c2: 'content active'
      })
    }
  }
  render() {
    return (
      <div>
        <button data-index='1' onClick={this.clickEvent}>按钮1</button>
        <button data-index='2' onClick={this.clickEvent}>按钮2</button>
        <div className={this.state.c1}>
          <h1>内容1</h1>
        </div>
        <div className={this.state.c2} >
          <h1>内容2</h1>
        </div>
      </div>
    )
  }
}
ReactDOM.render(<Tab />, document.getElementById('root')) 
7.React父传子组件数据 
props
父传递给子组件数据 ,单向流动 ,不能子 传递给父
props的传值  ,可以是任意的类型   
// 在父元素中使用state去控制子元素props的从而达到父元素数据传递给子元素
class ParentCom extends React.Component {
  constructor(props) {
    super(props)
    this.state = {
      isActive: true
    }
    this.changeShow = this.changeShow.bind(this)
  }
  changeShow() {
    this.setState({
      isActive: !this.state.isActive
    })
  }
  render() {
    return (
      <div>
        <button onClick={this.changeShow}>控制子组件显示</button>
        <ChildCom isActive={this.state.isActive} />
      </div>
    )
  }
}
class ChildCom extends React.Component {
  constructor(props) {
    super(props)
  }
  render() {
    let strClass = ''
    if (this.props.isActive) {
      strClass = 'active'
    } else {
      strClass = ''
    }
    return (
      <div className={'content' + strClass}>
        <h1>我是子元素</h1>
      </div>
    )
  }
}
ReactDOM.render(<ParentCom />, document.getElementById('root'))

8.React数据传递子传父
class ParentCom extends React.Component {
  constructor(props) {
    super(props)
    this.state = {
      childenData: null
    }
  }
  render() {
    return (
      <div>
        <h1>子元素传递给父元素的数据:{this.state.childenData}</h1>
        <ChildCom setChildData={this.setChildData} />
      </div>
    )
  }
  setChildData = (data) => {
    this.setState({
      childenData: data
    })
  }
}
class ChildCom extends React.Component {
  constructor(props) {
    super(props)
    this.state = {
      msg: 'hellworld'
    }
  }
  render() {
    return (
      <div>
        <button onClick={this.sendData}>  传递helloworld给父元素</button>
        {/* () =>  匿名箭头函数直接传递 */}
        <button onClick={() => this.props.setChildData('直接调用props的函数')}>  传递helloworld给父元素</button>
      </div>
    )
  }
  sendData = () => {
    // 将子元素传递给父元素,实际就是调用父元素传递进来的父元素函数
    this.props.setChildData(this.state.msg)
  }
}
ReactDOM.render(
  <ParentCom />,
  document.querySelector('#root')
)
9.React事件传递 
class ParentCom extends React.Component {
  constructor(props) {
    super(props)
  }
  render() {
    return (
      <div >
        <form action='http://www.baidu.com'>
          <div className="child" >
            <h1>helloword</h1>
          </div>
          <button onClick={this.parentEvent}>提交</button>
        </form>
        {/* 使用ES6箭头函数传递产数 */}
        <button onClick={(e) => { this.parentEvent1('msg:hello'), e }}>箭头函数产数传值</button>
        {/* 使用匿名函数方式传递产数 */}
        <button onClick={function (e) { this.parentEvent1('msg:hello'), e }.bind(this)}>匿名函数产数传值</button>
      </div>
    )
  }
  parentEvent = (e) => {
    console.log(e)
    e.preventDefault()
  }
  parentEvent1 = (msg) => {
    console.log(msg)
  }
}
ReactDOM.render(
  <ParentCom />,
  document.querySelector('#root')
)
10.React条件渲染+列表渲染  
条件渲染 
function UserGreet(props) {
  return (
    <h1>欢迎登陆</h1>
  )
}
function UserLogin() {
  return (
    <h1>请先登录</h1>
  )
}
class ParentCom extends React.Component {
  constructor(props) {
    super(props)
    this.state = {
      isLogin: false
    }
  }
  render() {
    let element = null
    if (this.state.isLogin) {
      element = (<UserGreet></UserGreet>)
    } else {
      element = (<UserLogin></UserLogin>)
    }
    return (
      <div>
        <h1>这是头部</h1>
        {/* 要将element插入到这里,这里类似插槽 */}
        {element}
        <h1>这是三元运算符的操作:</h1>
        {this.state.isLogin ? <UserGreet /> : <UserLogin />}
        <h2>这是尾部</h2>
      </div>
    )
  }
}
ReactDOM.render(
  <ParentCom />,
  document.querySelector('#root')
)

列表渲染  
function ListItem(props) {
  return (
    <li>
      <h3>{props.index}+1:listItem:{props.data.title}</h3>
      <p>{props.data.content}</p>
    </li>
  )
}
class ListItem2 extends React.Component {
  constructor(props) {
    super(props)
  }
  render() {
    return (
      <li onClick={(event) => this.clickEvent(this.props.index, this.props.data.title, event)}>
        <h3>{this.props.index}+1:listItem:{this.props.data.title}</h3>
        <p>{this.props.data.content}</p>
      </li>
    )
  }
  clickEvent = (title, index, event) => {
    alert(index + '-' + title)
  }
}
class Welcom extends React.Component {
  constructor(props) {
    super(props)
    //可以做ajax请求
    this.state = {
      list: [{
        title: '第一节 React事件',
        content: '事件内容'
      }, {
        title: '第二节 React数据',
        content: '数据内容'
      }, {
        title: '第三节 React渲染',
        content: '渲染内容'
      }]
    }
  }
  render() {
    let listArr = this.state.list.map((item, index) => {
      return (
        // <ListItem key={index} data={item} index={index}></ListItem>
        <ListItem2 key={index} data={item} index={index}></ListItem2>
      )
    })
    // let listArr = this.state.list.map((item, index) => {
    //   return (
    //     <li key={index}>
    //       <h3>{index}:{item.title}</h3>
    //       <p>{item.content}</p>
    //     </li>
    //   )
    // })
    return (
      <div>
        <h1>课程内容</h1>
        <ul>
          {listArr}
        </ul>
        <h2>这是尾部</h2>
        <h1>复杂没有用组件完成列表</h1>
        {
          this.state.list.map((item, index) => {
            return (
              <li key={index} onClick={(event) => { this.clickFn(index, item.title, event) }}>
                <h3>{index}:{item.title}</h3>
                <p>{item.content}</p>
              </li>
            )
          })
        }
      </div >
    )
  }
  clickFn = (title, index, event) => {
    alert(index + '-' + title)
  }
}
ReactDOM.render(
  <Welcom />,
  document.querySelector('#root')
)

10.React循环 
循环:arr.forEach返回空;arr.map返回数组;arr.filter通过return true/false过滤true的数组;arr.reduce讲数组中的所有的内容整合 


  
11.React生命周期 
生命周期即使是组件从实力化到渲染到最终从页面中销毁 ,整个过程就是生命周期,在这生命周期中 ,我们有许多可以调用的事件 ,也俗称为钩子函数 
 生命周期的3个状态 :
Mounting :讲组件插入到页面(DOM对象 )中
Updating : 将数据更新到页面(DOM对象 )中
Unmounting :讲组件移除页面(DOM对象 )中

生命周期中的钩子函数(方法 ,事件 )
componentWillMount:组件将要渲染 :AJAX请求数据 /添加动画前的类 
componentDidMount:组件渲染完毕 :添加动画 
componentWillReceive:组件将要接收props数据 :查看接收props的数据是什么 
shouldComponentUpdate:在组件接收到新的state或者props,判断是否要更新.返回bool 
componentWillUpdate:组件将要更新 
componentDidUpdate:组件已经更新(完毕 ) 
componentWillUnmount:组件将要卸载 :提交数据,保留数据什么的操作  

12.ECharts

13.React的ajax请求 

14.React插槽  
组件中写入内容 ,这些内容可以被识别和控制 ,React需要自己开发支持插槽功能 
原理:
组件中写入 HTML ,可以传入到props中.
组件中 的 HTML 内容直接全部插入 
组件中根据HTML的 内容不同,插入的 位置 不同  
class ParentCom extends React.Component {
  render() {
    console.log(this.props)
    return (
      <div>
        <h1>组件插槽</h1>
        {this.props.children}
        <ChildenCom>
          <h1 data-position='header'> 这是放置到头部的内容</h1>
          <h1 data-position='main'>这是主要的内容</h1>
          <h1 data-position='footer'>这是放置到尾部的内容</h1>
        </ChildenCom>
      </div>
    )
  }
}
class RootCom extends React.Component {
  constructor(props) {
    super(props)
    // console.log(props)
    this.state = {
      arr: [1, 2, 3]
    }
  }
  render() {
    return (
      <ParentCom>
        <h2 data-name='a' data-index={this.state.arr[0]}>子组件1</h2>
        <h2 data-name='b' data-index={this.state.arr[1]} > 子组件2</h2>
        <h2 data-name='c' data-index={this.state.arr[2]} > 子组件3</h2>
      </ParentCom>
    )
  }
}
class ChildenCom extends React.Component {
  render() {
    let headerCom, mainCom, footerCom;
    this.props.children.forEach((item, index) => {
      if (item.props['data-position'] == 'header') {
        headerCom = item
      } else if (item.props['data-position'] == 'main') {
        mainCom = item
      } else {
        footerCom = item
      }
    })
    return (
      <div>
        <div className='header'>
          {headerCom}
        </div>
        <div className='header'>
          {mainCom}
        </div>
        <div className='header'>
          {footerCom}
        </div>
      </div>
    )
  }
}
ReactDOM.render(
  <RootCom></RootCom>,
  document.querySelector('#root')
)

15.React路由 
根据不同的路径显示不同的内容(组件 ):React使用库 react-router-dom
安装 :
npm/cnpm/yarn install react-router-dom-save

ReactRouter三大组件 
Router:所有路由组件的根组件(底层组件 ),包裹路由规则最外层容器
属性 :basename->设置跟此路由根路径 ,router可以在1个 组件中 写多个 
Route:路由规则匹配组件,显示当前规则对应的组件  
Link:路由跳转的组件

注意 :如果要精准匹配 ,那么可以在 route上设置exact属性     
Router使用案例 :
class App extends React.Component {
  render() {
    return (
      <div id='app'>
        <div>所有页面普通内容</div>
        <Router>
          <Route path='/' exact component={() => (<div>首页</div>)}></Route>
          <Route path='/me' component={() => (<div>me</div>)}></Route>
          <Route path='/product' component={() => (<div>product</div>)}></Route>
        </Router>
        <Router>
          {/* <div className='nav'>
            <Link to='/'>Home</Link>
            <Link to='/product'>Product</Link>
            <Link to='/me'>个人中心</Link>
          </div> */}
          <Route path='/admin/' exact component={Home}></Route>
          <Route path='/admin/product' component={Product}></Route>
          <Route path='/admin/me' component={Me}></Route>
        </Router>
      </div>
    )
  }
}
export default App;

Link组件可以设置 to属性来进行页面的跳转 ,to属性 可以直接写路径的字符串,也可以通过1个对象 ,金星路的设置,如 :
class App extends React.Component {
    render() {
        let meObj = {
            pathname: '/me', //跳转的路径
            search: '?username=admin', //get请求的产数
            hash: '#abc', //设置的hash值
            state: { msg: 'helloworld' } //传入组件的数据
        };
        return (
            <div id='app'>
                <div>所有页面普通内容</div>
                <Router>
                    <div className='nav'>
                        <Link to='/'>Home</Link>
                        <Link to='/product'>Product</Link>
                        <Link to={meObj}>个人中心</Link>
                    </div>
                    <Route path='/' exact component={Home}></Route>
                    <Route path='/product' component={Product}></Route>
                    <Route path='/me' component={Me}></Route>
                </Router>
            </div>
        )
    }
}
Link的replace属性 :点击链接后 ,将新地址替换成历史访问记录的原地址     

动态路由的实现 :


重定向组件 
如果访问某个组件时,如果有重定向组件 ,那么就会修改页面路径 ,使得页面内容显示为所以定向路径的内容 
案例 :
import React from 'react'
import { Redirect, BrowserRouter as Router, Route, Link } from 'react-router-dom'
// 登陆信息组件
function LoginInfo(props) {
    // props.loginState = 'success'
    // props.loginState = 'fail'
    console.log(props)
    if (props.location.state.loginState === 'success') {
        return <Redirect to='/admin'></Redirect>
    }
    return <Redirect to='/login'></Redirect>
}
let FormCom = () => {
    let pashObj = {
        pathname: '/logininfo',
        state: {
            loginState: 'success'
        }
    }
    return (
        <div>
            <h1>表单验证</h1>
            <Link to={pashObj}>登陆验证后页面</Link>
        </div>
    )
}
class App extends React.Component {
    render() {
        return (
            <div>
                <Router>
                    <Route path='/' exact component={() => (<div>首页</div>)}></Route>
                    <Route path='/form' exact component={FormCom}></Route>
                    <Route path='/login' exact component={() => (<div>登陆页</div>)}></Route>
                    <Route path='/logininfo' exact component={LoginInfo}>admin登陆成功</Route>
                </Router>
            </div>
        )
    }
}
export default App
Switch组件 
让 switch组件内容的 route只匹配一个 ,只要匹配到了 ,剩余的路由规则将不再匹配 

返回 ,前进 ,传旨



15.Redux
解决React数据管理(状态管理 ),用于中大型 ,数据比较庞大 ,组件之间数据交互多 的情况下使用 .如果你不知道是否需要使用 Redux,那么就不需要用它 
1/解决组件的数据通信 
2/解决数据和交互较多的应用
Redux只是一种状态管理的解决方案 

Store:数据仓库 ,保存数据的地方 .
State:state是一个对象 ,数据仓库里的所有数据都放到一个state里
Action:1个动作 ,触发数据改变的方法 
(Store.)Dispatch:将动作触发成方法
Reducer:是一个函数,通过获取动作 ,改变数据 ,生成一个新的 state.从而改变页面 

安装 :
npm/cnpm install redux -save

初始化数据 (reduce有两个 作用 ,1初始化数据 ,2通过获取动作 ,改变数据 )
import { createStore } from 'redux'

// createStore创建仓库
const store = createStore(reducer)

// 用于创建新的state
const reducer = function (state = { num: 0 }, action) {
  switch (action.type) {
    case 'add':
      state.num++;
      break;
    case 'decrement':
      state.num--;
      break;
    default:
      break;
  }
  return { ...state } //相当于对象的copy
}
获取数据 
// 函数式计数器
const Counter = function (props) {
  let state = store.getState() //获取数据 
  return (
    <div>
      <h1>计数数量:{state.num}</h1>
      <button onClick={add}>计数+1</button>
      <button onClick={decrement}>计数-1</button>
    </div>
  )
}
修改数据 (通过 动作修改数据 )
function add() {
  // 通过仓库的方法dispatch进行修改数据
  store.dispatch({ type: 'add', content: { id: 1, msg: 'hello_aaa' } })
  console.log(store.getState())
}
function decrement() {
  // 通过仓库的方法dispatch进行修改数据
  store.dispatch({ type: 'decrement' })
  console.log(store.getState())
}
修改视图 (监听数据的变化重新渲染内容 )
ReactDOM.render(
  <Counter />,
  document.getElementById('root')
);
// 监听状态变化渲染也页面
store.subscribe(() => {
  ReactDOM.render(
    <Counter />,
    document.getElementById('root')
  );
})

React-redux
安装 :
npm/cnpm install react-redux 
概念 :
Provider组件 ,自动的将store里的 state和 组件进行关联 
mapStateToProps:将数据仓库的state和修改state的方法映射到组件上,形成新组件
mapDispatchToProps:将修改state数据的方法,映射到props,默认会传入store里的dispatch方法,实现 方法 共享 
connect 方法 :将组件和数据(方法 )进行连接  

使用 :
初始化数据,实力化store
// 用于创建新的state
function reducer(state = { num: 0 }, action) {
  switch (action.type) {
    case 'add':
      state.num++;
      break;
    default:
      break;
  }
  return { ...state } //相当于对象的copy
}
// createStore创建仓库
const store = createStore(reducer)
console.log(store)
数据的获取 ,数据的修改 
将 state映射到数组中 ,将修改数据的方法映射到组件的 props中 
// 将state映射到props函数
function mapStateToProps(state) {
  return {
    value: state.num
  }
}
// 将修改state数据的方法,映射到props,默认会传入store里的dispatch方法
function mapDispatchToProps(dispatch) {
  return {
    onAddCkick: () => { dispatch(addAction) }
  }
}
// 将上面2个方法,将数据仓库的state和修改state的方法映射到组件上,形成新组件
const App = connect(
  mapStateToProps,
  mapDispatchToProps
)(Counter)

class Counter extends React.Component {
  render() {
    // 计数,通过store的state传给props,直接通过props就可以将state的数据获取
    const value = this.props.value;
    // 将修改数据的时间或者方法传入到props
    const onAddClick = this.props.onAddClick;
    // 上面过程等同于vuex的mapMutation mapState
    return (
      <div>
        <h1>计数数量:{value}</h1>
        <button onClick={onAddClick}>计数+1</button>
      </div>
    )
  }
}
const addAction = {
  type: 'add'
}

15.React_Ant_UI蚂蚁框架 (https://mobile.ant.design/docs/react/introduce-cn)

1.安装 :
npm install antd-mobile --save
2.配置 npm install  babel-plugin-import --save
    npm run eject  (获取所有的配置  )

3.组件使用实例：
import { Button } from 'antd-mobile';
ReactDOM.render(<Button>Start</Button>, document.querySelector('#root'));







