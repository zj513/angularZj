## 设置快捷键模板
file--settings--live template -->javascript--添加快捷键--define

## 创建指定的文件后缀
--new-->edit file template-->+ -->设置文件扩展名和文件的名字即可

## 安装markdown插件
file--settings--plugin--browser responstory(下面第二个)--markdown navigator

## 框架和类库
什么是框什么是库？一个是提供房子的，一个只是给你提供方法，放东西的
框架：提供房子
库：只是提供一些方法

## MVC MVVM(双向数据绑定)
model-->数据 view:视图  controller:控制图 

MVVM   model:数据 view  viewModel:视图模型
命名空间的缺点   调用过长 ，不能完全避免不冲突
seajs(cmd)  requireJs(amd)  nodeJs(commonJs)

## AngularJS安装
  npm表示node package manager   我们安装node就会提供一个包管理器
  安装软件是名字不能叫同名
```
npm install angular
```
  
## 使用angular
1.引入angularJs
2.设置ng-app
3.ng-model实现双向绑定
4.将数据显示在页面中通过{{}}
{{}}表达式运算

## 防止闪烁
ng-bind
ng-bind-template
ng-clock

## 模块化
声明模块
```
var app = angular.model('appName',[],fn);
//参数的位置可以改变，但是名字不能变
app.run(['$rootScope',function(){}]);
app.controller('ctrlName',['$rootScope','$scope',function($rootScope,$scope){ //$scope实现双向绑定的桥梁viewModel

}]);
```
在标签上增加ng-controller指定控制器的作用范围

## ng-click
```
<button ng-click="fn(1,2,3)"></button>
$scope.fn = function(a,b,c){}
```

## 绑定对象类型的数据
数组和对象
```
<div ng-repeat="(key,value) in arrs track by $index" ng-init>
    {{$index}}{{$last}}....
<div>
```


## bootstrap
样式的框架提供了美丽的样式，还封装了很多产检基于jQuery的
```
npm i bootstrap
```

## ng-disabled禁用
所有表单元素向双向绑定必须增加ng-model属性

## 数组的方法
filter 为false过滤掉
find 找到为true的那一项
forEach 遍历
map 映射新的数组