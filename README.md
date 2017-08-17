## 以下文件的HTML主体部分
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="../build/react.js"></script>
    <script src="../build/react-dom.js"></script>
    <script src="../build/browser.min.js"></script>
</head>
<body>
    <div id="example"></div>
    <script type="text/babel">
       ... //此处加代码
    </script>
</body>
</html>
```

## demo1 Render JSX
这样的格式被叫做JSX，JSX中可以允许HTML标签，ReactDOM.render()方法可以解析jsx中的html。
```
 ReactDOM.render(
    <h1>Hello World!</h1>,
    document.getElementById('example')
);
```
另外，我们使用< script type="text/babel" >去解析jsx的代码。

## demo2 Use JavaScript in JSX
在HTML格式前加(<),在js代码之前加（{)
```
var names = ['lai', 'hua', 'min'];
ReactDOM.render(
    <div>{
        names.map((name) => <div>hello, {name}!</div>)
    }</div>,
    document.getElementById('example')
);
```
## demo3 Use Array in JSX
如果是一个可用的js数组，JSX会讲里面所有成员都解析
```
var arr = [
    <h1>hello,lai!</h1>,
    <h1>hello,hua!</h1>,
    <h1>hello,min!</h1>
]
ReactDOM.render(
    <div>{arr}</div>,
    document.getElementById('example')
);
```
## demo4 react components
定义一个react的组件
```
<script type="text/babel">
    //ES6
    class MyComponent extends React.Component {
        render() {
            return <h1>Hello Min</h1>
        }
    };
    //ES5
    var HelloMessage = React.createClass({
        render: function() {
            return <h1>Hello Lai</h1>;
        }
    });
    ReactDOM.render(
        <MyComponent/>,
        document.getElementById('example')
    );
</script>
```
## demo5 components props
组件可以从外部传入参数，然后内部用this.props获取
```
class Mytitle extends React.Component {
    render () {
        return <h1>Hello {this.props.name}!</h1>;           
    }
}
ReactDOM.render(
    <Mytitle name="lai"/>,
    document.getElementById('example')
);
```
## demo6 components state
组件状态是用components的state，先代码一段一段来看
```
class MyTitle extends React.Component {
    constructor(...args) {
      super(...args);
      this.state = {
        name: '访问者'
      };
    }
```
constructor代表组件的构造函数，...args代表组件的一些参数,super(...args)是ES6的写法，this.state对象储存的是组件状态
```
handleChange(e) {
    let name = e.target.value;
    this.setState({
        name: name
    });
}
```
这个方法是用来改变组件状态的，this.setState()方法去改变state的状态
```
render(){
    return <div>
            <input
                type="text"
                onChange={this.handleChange.bind(this)}
            />
            <p>你好，{this.state.name}</p>
        </div>;
}
```
这里用bind方法绑定state。

## demo7 this.props.child
```
class Mytitle extends React.Component {
    render () {
        return<ol>
            {
                React.Children.map(this.props.children, function (child) {
                    return <li>{child}</li>
                })
            }
        </ol>
    }
}
ReactDOM.render(
    <Mytitle>
        <span>Hello</span>
        <span>World</span>
    </Mytitle>,
    document.getElementById('example')
)
```

## demo8 react-lifecycle
```
class Mytitle extends React.Component {
    constructor(...args){
        super(...args);
        this.state = {
            loading: true,
            error: null,
            data: null
        };
    }
```
这里先定义一个组件以及她的状态，然后在接下来的生命周期中获取数据
```
componentDidMount() {
    const url = 'https://api.github.com/search/repositories?q=javascript&sort=stars';
    $.getJSON(url).done(
        (value) => this.setState({
            loading: false,
            data: value
        })
    ).fail(
        (jqXHR, textStatus) => this.setState({
            loading: false,
            error: jqXHR.status
        })
    );
}
```
获取到的数据存在组件的状态之中，在这个状态的里面我们可以在一下对数据进行操作
```
render() {
    if(this.state.loading){
        return <div>Loading...</div>
    }else if(this.state.error !== null){
        return <span>Error: {this.state.rror}</span>
    }else {
        const program = this.state.data.items;
        console.log(program);
        const result = [];
        program.forEach((item) => {
            var p = <li>{item.name}</li>
            result.push(p);
        });
        return <div>
            <ul>{result}</ul>
        </div>
    }
}
```
在这边一共分三部分，第一部分是正在加载过程中，第二部分是加载错误，第三部分是当加载出数据了之后，展示的页面。