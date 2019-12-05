### popstate实现history路由拦截

#### popstate事件
在支持H5的浏览器中，有一个window.onpopstate事件，该事件可以监听如下操作：
1. 点击浏览器的前进按钮/后退按钮
2. 执行js代码: `history.go(n)`; `history.forward()`

> 不同的浏览器在加载页面时处理popstate事件的形式存在差异。页面加载时Chrome和Safari通常会触发(emit )popstate事件，但Firefox则不会。
需要注意的是调用history.pushState()或history.replaceState()不会触发popstate事件。只有在做出浏览器动作时，才会触发该事件，如用户点击浏览器的回退按钮（或者在Javascript代码中调用history.back()）

#### history.pushState
1. history.pushState()只会改变当前地址栏的路径，并不会更新页面内容
2. 它会修改当前历史记录
```bash
window.history.pushState({target:  "mobile"}, "", 'https://www.jd.com');
```

#### history.replaceState
1. history.replaceState()会把当前的历史记录改成目标路径，并不会刷新页面,页面内容不变,只是地址发生了变化
2. 它会修改当前历史记录
```bash
window.history.replaceState({target:  "mobile"}, "", 'https://www.jd.com');
```

#### 通过popstate实现路由拦截
仅仅是思路, 实际还要考虑各个浏览器兼容性
```bash
function add() {
    history.pushState('a', '');
}
function replace() {
    history.replaceState('replace', '');
}
window.addEventListener("popstate", function () {
    if (history.state === 'a') {
        //弹窗,用户确认
        if (!userConfirm) {
            history.pushState('a', '');
        }
    }
});
```

