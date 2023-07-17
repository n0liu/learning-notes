```js
<button id="btn">按钮</button>
var btn = document.getElementById("btn");
// 防抖函数
/**
  * @param {Function} func 传入函数
  * @param {Number} wait 等待时间
  * @param {Boolean} immediate 是否立即执行
  * @return {Function}
*/
function debounce (func, wait, immediate) {
  // 判断 func 是否为一个函数
  if (typeof func !== 'function') throw new TypeError('debounce func must be a function')
  // 判断 wait 是否存在
  if (typeof wait === 'undefined') wait = 300
  // 判断 immediate 是否存在
  if (typeof immediate === 'undefined') immediate = false
  // 判断 wait 是否为 boolean
  if (typeof wait === 'boolean') {
    immediate = wait
    wait = 300
  }
  // 防抖函数 -> 开启一个延时器, 让 func 函数在规定时间内执行
  // 采用高阶函数中的函数作为返回值, 利用闭包的特性存储 timer
  var timer;
  return function (...args) {
    const that = this
    // 每次执行函数之前我们需要清除延时器, 目的：清除每次触发事情多余的次数
    timer && clearTimeout(timer)
    // 判断 immediate 是否为真 并且 timer 为假 才执行函数
    immediate && !timer ? func.apply(that, args) : null
    // 开启延时器
    // 在 setTimeout this 指向的 window 
    timer = setTimeout(function(){
      timer = null;
      // 如果 immediate 立即执行 延时器结束后不需要执行
      !immediate ? func.apply(that, args) : null
    }, wait)
  }
}

// btn.onclick = function() {
//   console.log("btn clicked")
// }
function click (ev) {
  console.log(ev)
  console.log(this)
  console.log("btn clicked")
}
// btn.onclick = debounce(click, 1000, false);
btn.onclick = debounce(click, 1000, true);
