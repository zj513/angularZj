## 控制器的特点
1.创建控制器会有一个$scope，我们把数据挂载在$scope就可以实现数据的双向绑定(在控制器申明的属性元素，可以在当前的作用域下获取到)
2.依赖注入
3.DOM控制器的作用是平行的
4.控制器可以嵌套使用，注意嵌套的是DOM标签
5.控制器不能复用，而且作用的不仅是控制（不要操作DOM）中的唯一操作的地方是link函数

## 指令(directive)
指令是不依赖控制器的（一般是依赖控制器的）
```
<my-hello></my-hello>
app.directive('myHello',function(){
        return{
            /*
            *es6语法提供的模板语法，可以帮我们快速的拼字符串
            * `template:"<h1>hello</h1><p>every</p>"`
            * */
            template:"<div></div>"   //静态模板
            templateUrl:"panel.html",  //模板的引用路径
            restrict:"ECMA",           //限制使用范围
            link:function(scope,element,attrs){
                //scope当前作用域
                //element当前元素
                //attrs属性集合
                //声明了一个title属性，将内容声明在当前作用域上
                 scope.title = attrs["title"];   //这样写会定义在根作用域下
           },
           replace:true,  //将我们的指令标签替换掉，替换我们的template
           transclude:true,   //将内容插入到模板中，想插入到哪里就给那个标签上加一个ng-transclude
           scope:true/scope:{}
        }
    })
```
扩展功能 封装插件
装饰指令（美化，增加功能）
组件指令（编译出代码片段实现例如弹框，表格）

## 指令依赖与控制器吗？
指令可以完全不依赖于控制器
通过模块来创建指令即可

## 命名规范
```
<text></text>
<margin-top></margin-top>
```

通过模块来创建指令（驼峰命名法）
第一个参数代表指令的名字
第二个参数指令的定义默认返回对象
```
app.directive('myHello',function(){
        return{
            /*
            *es6语法提供的模板语法，可以帮我们快速的拼字符串
            * `template:"<h1>hello</h1><p>every</p>"`
            * */
            template:"<h1>hello</h1><p>every</p>"
        }
    })
```

## 四种可以限制范围restrict：EAMC
E：element   A：attribute
```
<my-hello></my-hello>
<div my-hello></div>
<div class="my-hello"></div>
<!--directive：my-hello-->
```

##指令中的scope
->scope独立作用域 
scope:{}      //断绝关系，无法继承作用域上的任何东西--完全断绝需要数据，只能通过指令的标签上的属性进行传递
-引用的是字符串 @（取到的是attr对应的字符串）
-引用的是变量  #(取到的是当前指令所在的作用域的变量)
-引用函数     & 传递参数的时候使用对象格式
scope:true,   //这个叫不断绝关系
```
<div ng-controller="myCtrl">
    <!--<hello title="这是标题"></hello>-->
    <hello title="{{name}}"></hello>
</div>

//指令和控制器之间的交互，指令中需要使用控制器中的数据
    var app = angular.module("appModule",[]);
    app.controller('myCtrl',function($scope){
        $scope.name = 112;
    });
    app.directive("hello",function(){
        return {
            template:'<div>{{title}}</div>',
           // scope:true,  //保留一下
            /*link:function(scope,element,attrs){
                //scope.title = attrs['title']
            },*/
            scope:{
                title:'@'  //引用的是title属性的字符串，如果名字相同后面的可以省略,如果不相同不能省略
            }   //完全断绝关系
        }
    })
```

##引用函数(&)
```
<body ng-controller="myCtrl">
<hello s="say()"></hello>  <!--引用的是当前作用域上的函数-->
<script type="text/javascript" src="../../node_modules/angular/angular.js"></script>
<script type="text/javascript">
    var app = angular.module("appModule",[]);
    app.controller("myCtrl",function($scope){
        $scope.say = function(){
            alert(123);
        }
    });
    app.directive("hello",function(){
        return {
            template:'<button ng-click="n()">click me</button>',
            scope:{
                //要在自己家声明一个函数
                n:'&s'   //获取传递的那个函数，然后声明在自己的函数上，让其执行
            }
        }
    })
</script>
</body>
```

## API文档
ng-show ng-hide只是简单的操作样式 会强制执行所有的代码
ng-if 如果不满足条件则内部代码都不运行
频繁切换使用ng-show ng-hide 第一次消耗比较大
ng-if如果不满足内部指令不执行，但是频繁切换时性能消耗较大，搭配ng-repeat判断数据是否存在
