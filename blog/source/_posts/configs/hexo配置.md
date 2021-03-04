---
title: hexo 配置
top: 0
date: 2020-01-22 17:04:37
tags: configs
---

- 文章置顶
- 添加阅读统计

<!-- more -->

> https://susreal.com/article/2019/hexo-theme-icarus-2/

## 文章置顶

博客默认按照创建【时间倒序】排列，如果项置顶一些文章，icarus 没有提供这个功能，需要进行一些改造。

实现的效果是：写文章的时候在 front-matter 区域  定义文章的权重（top），如果 top 的数值大于 0，则将该文章置顶，并展示置顶标签。

1、添加 top 属性在根目录的 config 文件中

```javascript
/_config.yml

index_generator:
  path: ''
  per_page: 10
  order_by:
    top: -1
    date: -1
```

2、修改 generator.js，主要是在生成 html 代码时优先按照 top 排序

```javascript
/⁨node_modules⁩/hexo-generator-index⁩/lib⁩/generator.js

var paginationDir = config.pagination_dir || 'page';

// added code
posts.data = posts.data.sort(function(a, b) {
if(a.top && b.top) {
    if(a.top == b.top) return b.date - a.date;
    else return b.top - a.top;
}
else if(a.top && !b.top) {
    return -1;
}
else if(!a.top && b.top) {
    return 1;
}
else return b.date - a.date;
});
// end

var path = config.index_generator.path || '';
```

3、修改模板中的 post.md，添加 top 属性并设置默认值为 0

```javascript
/scaffolds/post.md
---
title: {{ title }}
date: {{ date }}
tags:
top: 0
---
```

4、在目标文章中添加 top: 1

```javascript
---
title: yue'qian | 生活探险家
date: 2018-01-01 00:00:01
tags: life
categories: 人生旅途
top: 1
---
```

5、根据喜好在前端添加标签

```javascript
/themes/icarus/layout/common/article.ejs

<% if (post.top>0) { %>
<i class="fas fa-arrow-alt-circle-up" style="color:#3273dc"></i>
<span class="level-item" style="color:#3273dc">&nbsp;置顶</span>
<% } %>
```

## 添加阅读统计

valine 插件在 1.2.0 版本之后提供了文章阅读量统计的功能，好处是可以通过 leancloud 后台的可视化界面看到数据。目前只支持文章 PV 的统计，添加方式非常简单：

在 config 文件中添加 valine 的 visitor 属性
修改 valine 的加载文件 valine.ejs，添加 visitor 字段的加载
根据想添加统计的展示位置，例如文章尾部，添加前端代码
具体的操作可以参考 valine 官方文档，这里不多介绍了。我用的是更加简单方便的 busuanzi 进行统计：

1、在 icarus 主题的 head.ejs 中添加脚本

```javascript
/themes/icarus/layout/common/head.ejs

<% if (has_config('visit')) { %>
<script async="" src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>
<% } %>
```

2、在网页 footer 里面统计站点的 UV 和 PV

```javascript
/themes/icarus/layout/common/footer.ejs

<span id="busuanzi_container_site_uv">
    ❤️ 感谢
    <span id="busuanzi_value_site_uv">0</span>
    位小伙伴的
</span>
<span id="busuanzi_container_site_pv">
    <span id="busuanzi_value_site_pv">0</span>
    次陪伴
</span>
```

3、在每篇文章 article 里面统计阅读量 PV，主页不显示

```javascript
/themes/icarus/layout/common/article.ejs

<div class="level is-size-7 has-text-grey">
    <div class="level-left">
        <i class="far fa-eye"></i>
        <span>&nbsp;</span>
        <span id="busuanzi_container_page_pv" style="display: inline;">
            <span id="busuanzi_value_page_pv">0</span>
        </span>
    </div>
</div>
```

需要注意的是：busuanzi 统计 UV 的逻辑是根据浏览器请求的 cookie，不是严格意义上的设备唯一标识。
