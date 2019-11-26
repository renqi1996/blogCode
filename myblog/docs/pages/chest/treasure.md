# 哆啦A梦的口袋
> 高效，神奇，有用的资源

## 如何使用vuepress搭建个人博客
https://www.qiufeihong.top/technical-summary/vuepress/

## 如何使用vuepress构建类似element-ui文档(即如何引用element-ui)
http://www.cppcns.com/wangluo/javascript/252192.html

## nginx一键配置
https://nginxconfig.io/

![](/egg.png)

## lodash按需加载
https://www.jianshu.com/p/f03ff4f3a8b3

## threeJs 
#### 中文教程

::: warning
This is a warning
:::

``` js

/**
 * Promise 实现 遵循promise/A+规范
 * Promise/A+规范译文:
 * https://malcolmyu.github.io/2015/06/12/Promises-A-Plus/#note-4
 */

// promise 三个状态
const PENDING = "pending";
const FULFILLED = "fulfilled";
const REJECTED = "rejected";

function Promise(excutor) {
    let that = this; // 缓存当前promise实例对象
    that.status = PENDING; // 初始状态
    that.value = undefined; // fulfilled状态时 返回的信息
    that.reason = undefined; // rejected状态时 拒绝的原因
    that.onFulfilledCallbacks = []; // 存储fulfilled状态对应的onFulfilled函数
    that.onRejectedCallbacks = []; // 存储rejected状态对应的onRejected函数

    function resolve(value) { // value成功态时接收的终值
        if(value instanceof Promise) {
            return value.then(resolve, reject);
        }

        // 为什么resolve 加setTimeout?
        // 2.2.4规范 onFulfilled 和 onRejected 只允许在 execution context 栈仅包含平台代码时运行.

        setTimeout(() => {
            // 调用resolve 回调对应onFulfilled函数
            if (that.status === PENDING) {
                // 只能由pending状态 => fulfilled状态 (避免调用多次resolve reject)
                that.status = FULFILLED;
                that.value = value;
                that.onFulfilledCallbacks.forEach(cb => cb(that.value));
            }
        });
    }

    function reject(reason) { // reason失败态时接收的拒因
        setTimeout(() => {
            // 调用reject 回调对应onRejected函数
            if (that.status === PENDING) {
                // 只能由pending状态 => rejected状态 (避免调用多次resolve reject)
                that.status = REJECTED;
                that.reason = reason;
                that.onRejectedCallbacks.forEach(cb => cb(that.reason));
            }
        });
    }

    // 捕获在excutor执行器中抛出的异常
    // new Promise((resolve, reject) => {
    //     throw new Error('error in excutor')
    // })
    try {
        excutor(resolve, reject);
    } catch (e) {
        reject(e);
    }
    function buddleSort (data) {
        for (let i = 0; i < data.length; i++) {
            for (let j = 0; j < data.length - i;j++) {
                if (data[j] > data[j+1]) {
                    let temp = data[j+1]
                    data[j+1] = data[j]
                    data[j] = temp
                }
            }
        }
        return data
    }
    function buddleSortV2 (data) {
        let i = data.length - 1
        while (i > 0) {
            let pos = 0
            for (let j = 0; j < i;j++) {
                if (data[j] > data[j+1]) {
                    pos = j
                    let temp = data[j+1]
                    data[j+1] = data[j]
                    data[j] = temp
                }
            }
            i = pos
        }
        return data
    }
    function monthAcc (obj) {
        let obj = {1:222, 2:123, 5:888};
        let result = new Array(12).map((item, index) => {
            if (item === undefined) {
                item = obj[index+1] || null
            }
        })
    }
    class LazyManClass: {
        constructor (name) {
            super(this)
        }
    }
}

```