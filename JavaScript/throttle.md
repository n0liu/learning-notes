```js
// 节流函数规定的时间触发,只要有触发就会执行
/**
 *  @param {Function} func 执行的函数
 *  @param {Number}  wait 等待时间
*/
function myThrottle (func, wait) {
  if (typeof func !== "function") throw new Error(`${func} is not a function`)
  if (typeof wait === "undefined") wait = 500
  // 记录上一次执行结束的时间
  let previous = 0
  let timer = null;
  return function (...args) {
    // 存储this
    const that = this
    // 记录当前触发的时间
    const now = new Date()
    // 判断当前的触发频率
    const interval = wait - (now - previous)
    // 低频触发 立即执行
    if (interval <= 0) {
      func.call(that, ...args)
      // 保存当前函数执行的时间
      previous = new Date()
      clearTimeout(timer) // 清空延时器的操作，不能将timer值重置
      // 手动重置
      timer = null
    } else if (!timer){
      timer = setTimeout(function () {
        clearTimeout(timer) // 清空延时器的操作，不能将timer值重置
        // 手动重置
        timer = null
        func.call(that, ...args)
        previous = new Date()
      }, interval)
    }
  }
}
// document.onscroll = function () {
//   console.log(1)
// }
function scroll () {
  console.log(1)
}
document.onscroll = myThrottle(scroll, 1000)
