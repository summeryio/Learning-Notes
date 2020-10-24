##### 标签中引入图片

```
<div class="login-container" :style="{'background-image': `url(${require('@/assets/images/login_bg.png')})`}">
```



##### 关闭热更新

```
{
  devServer: {
    hot: false,
    liveReload: false
  }
}
```



##### 动态渲染路由代码保存

```
import Layout from '@/layout'

export function traverseRoutes(menus){
  let routers = []
  
  menus.forEach((m, i) => {
    if (m.parentId == 0) {
        m.fullPath = m.route
        let module = {
            parentId: m.parentId,
            id: m.id,
            name: m.path,
            path: '/' + m.path,
            component: Layout,
            meta: m.meta,
            alwaysShow: false,
            children: [{
              path: m.path,
              name: m.path,
              component: (resolve) => require(['@/views/' + m.component], resolve), // '@/views/' 必须在外面
              meta: m.meta
            }]
        }
        routers.push(module)
    }
  })

  convertTree(routers, menus)

  return routers
}

export function convertTree(routers, menus) {
  routers.forEach(r => {
      menus.forEach((m, i) => {
          if (m.parentId > 0 && m.parentId == r.id) {
              r.alwaysShow = true
              if (!r.children) r.children = []
              let menu = {
                  id: m.id,
                  name: m.path,
                  path: m.path,
                  component: (resolve) => require(['@/views/' + m.component], resolve),
                  meta: m.meta
              }
              
              r.children = [menu]
          }
      })

      if (r.children && r.children.length) {
        convertTree(r.children, menus)
      }
  })
}
```

