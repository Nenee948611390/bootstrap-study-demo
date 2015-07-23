# 简介
模态框经过了优化，更加灵活，以弹出对话框的形式出现，具有最小和最实用的功能集，参考[modal](http://v3.bootcss.com/javascript/#modals)。

---

# 用法
## HTML结构
- div[class=modal[fade]][id]
    - div[class=modal-dialog[modal-lg|modal-md|modal-sm]]
        - div[class=modal-content]
            - div[class=modal-header]
                - h1/h2/h3/h4/h5/h6[class=modal-title]
            - div[class=modal-body]
            - div[class=modal-footer]

示例：
```
<div class="modal fade" id="myModal">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
            <span aria-hidden="true">&times;</span>
        </button>
        <h4 class="modal-title">Modal title</h4>
      </div>
      <div class="modal-body">
        ...
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary">Save changes</button>
      </div>
    </div>
  </div>
</div>
```

## 调用模态框
通过 data 属性或 JavaScript 调用模态框插件，可以根据需要动态展示隐藏的内容。模态框弹出时还会为 <body> 元素添加 .modal-open 类，从而覆盖页面默认的滚动行为，并且还会自动生成一个 .modal-backdrop 元素用于提供一个可点击的区域，点击此区域就即可关闭模态框。

### 通过 data 属性
不需写 JavaScript 代码也可激活模态框。通过在一个起控制器作用的元素（例如：按钮）上添加 data-toggle="modal" 属性和data-target="#foo" 属性，以及 href="#foo" 属性，用于指向被控制的模态框。例如：`<button type="button" data-toggle="modal" data-target="#myModal">Launch modal</button>`，完整示例参考[dynamic-demo.html](https://github.com/zhbhun/bootstrap-study-demo/blob/master/modal/dynamic-demo.html).

### 通过 JavaScript 调用
需一行 JavaScript 代码，即可通过元素的 id myModal 调用模态框：`$('#myModal').modal(options)`，完整示例参考[dynamic-by-javascript-demo.html](https://github.com/zhbhun/bootstrap-study-demo/blob/master/modal/dynamic-by-javascript-demo.html)。modal参数：
- backdrop boolean/'static' 默认值为true，Includes a modal-backdrop element. Alternatively, specify static for a backdrop which doesn't close the modal on click.
- keyboard boolean 默认值为true，键盘上的 esc 键被按下时关闭模态框。
- show boolean 默认值为true，模态框初始化之后就立即显示出来。
- remote path 默认值为false，如果提供的是 URL，将利用 jQuery 的 load 方法从此 URL 地址加载要展示的内容（只加载一次）并插入 .modal-content 内。如果使用的是 data 属性 API，还可以利用 href 属性指定内容来源地址。下面是一个实例：`<a data-toggle="modal" href="remote.html" data-target="#modal">Click me</a>`

modal方法的更多使用方式：
- .modal(options): 将页面中的某块内容作为模态框激活, 接受可选参数 object。
- .modal('toggle'): 手动打开或关闭模态框，在模态框显示或隐藏之前返回到主调函数中（触发 shown.bs.modal 或 hidden.bs.modal 事件之前）
- .modal('show'): 手动打开模态框, 在模态框显示之前返回到主调函数中（也就是，在触发 shown.bs.modal 事件之前）
- .modal('hide'): 手动隐藏模态框, 在模态框隐藏之前返回到主调函数中（也就是，在触发 hidden.bs.modal 事件之前）。
- .modal('handleUpdate'): ???

## 模态框事件
Bootstrap 的模态框类提供了一些事件用于监听并执行你自己的代码，具体如下所示：
- show.bs.modal: show 方法调用之后立即触发该事件。如果是通过点击某个作为触发器的元素，则此元素可以通过事件的 relatedTarget 属性进行访问。
- shown.bs.modal: 此事件在模态框已经显示出来（并且同时在 CSS 过渡效果完成）之后被触发。如果是通过点击某个作为触发器的元素，则此元素可以通过事件的 relatedTarget 属性进行访问。
- hide.bs.modal: hide 方法调用之后立即触发该事件。
- hidden.bs.modal: 此事件在模态框被隐藏（并且同时在 CSS 过渡效果完成）之后被触发。
- loaded.bs.modal: 从远端的数据源加载完数据之后触发该事件。

简单示例：
```
$('#myModal').on('hidden.bs.modal', function (e) {
  // do something...
})
```
完整实例参考[event-demo.html](https://github.com/zhbhun/bootstrap-study-demo/blob/master/modal/event-demo.html)

---

## 样式
- 可选尺寸
    - div.modal-dialog.modal-lg
    - div.modal-dialog.modal-md，默认
    - div.modal-dialog.modal-sm
- 动画
    - div.modal.fade
    - div.modal

---

## 高级配置
- 增强模态框的可访问性
.modal 添加 role="dialog" 和 aria-labelledby="..." 属性，用于指向模态框的标题栏；为 .modal-dialog 添加 aria-hidden="true" 属性。另外，还应该通过 aria-describedby属性为模态框 .modal 添加描述性信息。示例如下：
```
<div class="modal fade" id="myModal" role="dialog" aria-labelledby="myModalLabel" aria-describedby="this is a modal!">
  <div class="modal-dialog" role="document" aria-hidden="true">
    <div class="modal-content">
      <div class="modal-header">
        <h4 class="modal-title" id="myModalLabel">Modal title</h4>
      </div>
      <div class="modal-body">
        ...
      </div>
      <div class="modal-footer">
        ...
      </div>
    </div>
  </div>
</div>
```

# 混合组件
## 使用栅格系统
```
<div class="modal fade" role="dialog" aria-labelledby="gridSystemModalLabel">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
        <h4 class="modal-title" id="gridSystemModalLabel">Modal title</h4>
      </div>
      <div class="modal-body">
        <div class="container-fluid">
          <div class="row">
            <div class="col-md-4">.col-md-4</div>
            <div class="col-md-4 col-md-offset-4">.col-md-4 .col-md-offset-4</div>
          </div>
          <div class="row">
            <div class="col-md-3 col-md-offset-3">.col-md-3 .col-md-offset-3</div>
            <div class="col-md-2 col-md-offset-4">.col-md-2 .col-md-offset-4</div>
          </div>
          <div class="row">
            <div class="col-md-6 col-md-offset-3">.col-md-6 .col-md-offset-3</div>
          </div>
          <div class="row">
            <div class="col-sm-9">
              Level 1: .col-sm-9
              <div class="row">
                <div class="col-xs-8 col-sm-6">
                  Level 2: .col-xs-8 .col-sm-6
                </div>
                <div class="col-xs-4 col-sm-6">
                  Level 2: .col-xs-4 .col-sm-6
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary">Save changes</button>
      </div>
    </div><!-- /.modal-content -->
  </div><!-- /.modal-dialog -->
</div><!-- /.modal -->
```

---

# 源码分析
## body
```
.modal-open {
  overflow: hidden;
}
```

## modal
```
.modal {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 1050;
  display: none;
  overflow: hidden;
  -webkit-overflow-scrolling: touch;
  outline: 0;
}
.modal.fade .modal-dialog {
  -webkit-transition: -webkit-transform .3s ease-out;
       -o-transition:      -o-transform .3s ease-out;
          transition:         transform .3s ease-out;
  -webkit-transform: translate(0, -25%);
      -ms-transform: translate(0, -25%);
       -o-transform: translate(0, -25%);
          transform: translate(0, -25%);
}
.modal.in .modal-dialog {
  -webkit-transform: translate(0, 0);
      -ms-transform: translate(0, 0);
       -o-transform: translate(0, 0);
          transform: translate(0, 0);
}
.modal-open .modal {
  overflow-x: hidden;
  overflow-y: auto;
}
```

## modal-dialog
``` 
.modal-dialog {
  position: relative;
  width: auto;
  margin: 10px;
}
```

## modal-content
```
.modal-content {
  position: relative;
  background-color: #fff;
  -webkit-background-clip: padding-box;
          background-clip: padding-box;
  border: 1px solid #999;
  border: 1px solid rgba(0, 0, 0, .2);
  border-radius: 6px;
  outline: 0;
  -webkit-box-shadow: 0 3px 9px rgba(0, 0, 0, .5);
          box-shadow: 0 3px 9px rgba(0, 0, 0, .5);
}
```

## modal-backdrop
```
.modal-backdrop {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 1040;
  background-color: #000;
}
.modal-backdrop.fade {
  filter: alpha(opacity=0);
  opacity: 0;
}
.modal-backdrop.in {
  filter: alpha(opacity=50);
  opacity: .5;
}
```

## modal-header
```
.modal-header {
  min-height: 16.42857143px;
  padding: 15px;
  border-bottom: 1px solid #e5e5e5;
}
.modal-header .close {
  margin-top: -2px;
}
```

## modal-title
```
.modal-title {
  margin: 0;
  line-height: 1.42857143;
}
```

## modal-body
```
.modal-body {
  position: relative;
  padding: 15px;
}
```

## modal-footer
```
.modal-footer {
  padding: 15px;
  text-align: right;
  border-top: 1px solid #e5e5e5;
}
.modal-footer .btn + .btn {
  margin-bottom: 0;
  margin-left: 5px;
}
.modal-footer .btn-group .btn + .btn {
  margin-left: -1px;
}
.modal-footer .btn-block + .btn-block {
  margin-left: 0;
}
.modal-footer:before,
.modal-footer:after {
  display: table;
  content: " ";
}

.modal-footer:after {
  clear: both;
}
```

## 响应式
```
@media (min-width: 768px) {
  .modal-dialog {
    width: 600px;
    margin: 30px auto;
  }
  .modal-content {
    -webkit-box-shadow: 0 5px 15px rgba(0, 0, 0, .5);
            box-shadow: 0 5px 15px rgba(0, 0, 0, .5);
  }
  .modal-sm {
    width: 300px;
  }
}
@media (min-width: 992px) {
  .modal-lg {
    width: 900px;
  }
}
```

## 其他
```
.modal-scrollbar-measure {
  position: absolute;
  top: -9999px;
  width: 50px;
  height: 50px;
  overflow: scroll;
}
```

---

# 问题
1. 模态框不支持同时打开多个模态框
    千万不要在一个模态框上重叠另一个模态框。要想同时支持多个模态框，需要自己写额外的代码来实现。参考实例[wrong-multi-modal-demo.html](https://github.com/zhbhun/bootstrap-study-demo/blob/master/modal/wrong-multi-modal-demo.html)和[multi-modal-demo.html](https://github.com/zhbhun/bootstrap-study-demo/blob/master/modal/multi-modal-demo.html)

2. 模态框的HTML代码放置的位置
    务必将模态框的 HTML 代码放在文档的最高层级内（也就是说，尽量作为 body 标签的直接子元素），以避免其他组件影响模态框的展现和/或功能，参考实例[wrong-multi-modal-demo.html](https://github.com/zhbhun/bootstrap-study-demo/blob/master/modal/wrong-multi-modal-demo.html)。

3. Due to how HTML5 defines its semantics, the autofocus HTML attribute has no effect in Bootstrap modals. To achieve the same effect, use some custom JavaScript:

```
$('#myModal').on('shown.bs.modal', function () {
  $('#myInput').focus()
})
```

4. 嵌入视频
在模态框中嵌入 YouTube 视频需要增加一些额外的 JavaScript 代码，用于自动停止重放等功能，这些代码并没有在 Bootstrap 中提供。请参考这份[发布在 Stack Overflow 上的文章](https://stackoverflow.com/questions/18622508/bootstrap-3-and-youtube-in-modal)。

---

# Todo
1. bootstrap是如何通过data属性开闭模态框的？
2. “增强模态框的可访问性 ”是做什么用的？
3. ...