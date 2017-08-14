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
The template syntax in React is called JSX. It is allowed in JSX to put HTML tags directly into JavaScript codes. ReactDOM.render() is the method which translates JSX into HTML, and renders it into the specified DOM node.
```
 ReactDOM.render(
    <h1>Hello World!</h1>,
    document.getElementById('example')
);
```
Attention, you have to use < script type="text/babel" > to indicate JSX codes, and include browser.min.js, which is a browser version of Babel and could be get inside a babel-core@5 npm release, to actually perform the transformation in the browser.

Before v0.14, React use JSTransform.js to translate < script type="text/jsx">. It has been deprecated (more info).

## demo2 Use JavaScript in JSX
It takes angle brackets (<) as the beginning of HTML syntax, and curly brackets ({) as the beginning of JavaScript syntax.
```
var names = ['lai', 'hua', 'min'];
ReactDOM.render(
    <div>{
        names.map((name) => <div>hello, {name}!</div>)
    }</div>,
    document.getElementById('example')
);
```


