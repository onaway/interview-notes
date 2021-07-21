### 一、DOM 事件级别

DOM级别一共可以分为四个级别：DOM0级、DOM1级、DOM2级和DOM3级。而**DOM事件分为3个级别：DOM 0级事件处理，DOM 2级事件处理和DOM 3级事件处理**。由于DOM 1级中没有事件的相关内容，所以没有DOM 1级事件



#### 1、DOM 0级事件

**el.onclick=function(){}**



#### 2、DOM 2级事件

**el.addEventListener(event-name, callback, useCapture)**

- event-name: 事件名称，可以是标准的 DOM 事件
- callback: 回调函数，当事件触发时，函数会被注入一个参数为当前的事件对象 event
- **useCapture：默认是 false，代表事件句柄在冒泡阶段执行**



#### 3、DOM 3级事件

- UI事件，当用户与页面上的元素交互时触发，如：load、scroll
- 焦点事件，当元素获得或失去焦点时触发，如：blur、focus
- 鼠标事件，当用户通过鼠标在页面执行操作时触发如：dblclick、mouseup
- 滚轮事件，当使用鼠标滚轮或类似设备时触发，如：mousewheel
- 文本事件，当在文档中输入文本时触发，如：textInput
- 键盘事件，当用户通过键盘在页面上执行操作时触发，如：keydown、keypress
- 合成事件，当为 IME（输入法编辑器）输入字符时触发，如：compositionstart
- 变动事件，当底层 DOM 结构发生变化时触发，如：DOMsubtreeModified
- 同时 DOM3级事件也允许使用者自定义一些事件



### 二、DOM 事件模型和事件流

**DOM 事件模型分为捕获和冒泡**。一个事件发生后，会在子元素和父元素之间传播（propagation）。这种传播分成三个阶段：

（1）捕获阶段：事件从 window 对象自上而下向目标节点传播的阶段；

（2）目标阶段：真正的目标节点正在处理事件的阶段；

（3）冒泡阶段：事件从目标节点自下而上向 window 对象传播的阶段。



### 三、事件代理(事件委托)

由于事件会在冒泡阶段向上传播到父节点，因此可以把子节点的监听函数定义在父节点上，由父节点的监听函数统一处理多个子元素的事件。这种方法叫做事件的代理

- 减少内存消耗，提高性能
- 动态绑定事件



### 四、Event对象常见的应用

- event. preventDefault()：阻止默认行为
- event.stopPropagation()：阻止事件冒泡
- event.stopImmediatePropagation()：既能阻止事件冒泡，也能阻止元素同事件类型的其它监听器被触发
- event.currentTarget：始终是监听事件者
- event.target：是事件的真正发出者

