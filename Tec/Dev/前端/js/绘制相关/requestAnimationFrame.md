##   requestAnimationFrame  
h5中新增的取代计时器的动画函数
1. requestAnimationFrame 会把每一帧中的所有 DOM 操作集中起来，在一次重绘或回流中就完成，并且重绘或回流的时间间隔紧紧跟随浏览器的刷新频率  
2. 在隐藏或不可见的元素中，requestAnimationFrame 将不会进行重绘或回流，这当然就意味着更少的 CPU、GPU 和内存使用量  
3. requestAnimationFrame 是由浏览器专门为动画提供的 API，在运行时浏览器会自动优化方法的调用，并且如果页面不是激活状态下的话，动画会自动暂停，有效节省了 CPU 开销  
## 使用  
```  
// 简单使用
function counter() {
  let count = 0;
  function animate(time) {
    if (count < 50) {
      count++;
      console.log(count);
      requestAnimationFrame(animate);
    }
  }
  requestAnimationFrame(animate);
}
btn.addEventListener("click", counter, false);  

// 大数据量填充表格，相当于按帧分布渲染，防止卡顿  
var total = 10000;
var size = 100;
var count = total / size;
var done = 0;
var ul = document.getElementById('list');

function addItems() {
    var li = null;
    var fg = document.createDocumentFragment();

    for (var i = 0; i < size; i++) {
        li = document.createElement('li');
        li.innerText = 'item ' + (done * size + i);
        fg.appendChild(li);
    }

    ul.appendChild(fg);
    done++;

    if (done < count) {
        requestAnimationFrame(addItems);
    }
};

requestAnimationFrame(addItems);
```  
递归循环调用