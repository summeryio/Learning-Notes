##### 路由跳转

- `navigateTo`, `redirectTo` 只能打开非 tabBar 页面。
- `switchTab` 只能打开 tabBar 页面。
- `reLaunch` 可以打开任意页面。



##### navigator 打开tabBar 页面

```
<navigator url="/pages/house/house?city={{ item.id }}" open-type="switchTab"></navigator>
```



##### 每次进去都请求数据，使用 onShow()



##### vant weapp Toast引用

```
import Toast from '../../miniprogram_npm/@vant/weapp/toast/toast';
```



##### 自定义导航组件

```
https://github.com/lingxiaoyi/navigation-bar
```



##### 小程序date ios下需要转化一下

```
.replace(/\-/g, "/")
```



##### 使用catchtap阻止子元素事件冒泡