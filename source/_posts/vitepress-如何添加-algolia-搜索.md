---
title: vitepress 如何添加 algolia 搜索
categories:
  - 未分类
date: 2022-11-01 18:05:41
tags:
---

## 注册 algolia 账号
[algolia 官网](https://www.algolia.com/)

## 创建 index

下一步要用到

## 配置中开启 algolia

### appId 

setting -> Team and Access -> API keys -> Application ID

### apiKey

> 请勿使用 Admin API Key

setting -> Team and Access -> API keys -> Search-Only API Key

### indexName

上一步创建的 index 的名称

```js
// docs/.vitepress/config.js

export default defineConfig({
  title: "xxx",
  description: "Just playing around.",
  themeConfig: {
    algolia: {
      appId: 'xxx',
      apiKey: 'xxxx',
      indexName: 'xxx'
    },
  },
});
```

## 上传数据到 algolia

到这一步你的 vitepress 页面中应该能看到搜索框了，但是还无法搜索到结果，因为你还没上传数据到 algolia。

algolia 官方提供了 crawler(爬虫) 来爬取你网站的数据，但是好像是收费的。

algolia 也提供了免费的方法，通过官方提供的 docker 上传数据到 algolia。

[Run the crawl from the Docker image](https://docsearch.algolia.com/docs/legacy/run-your-own/#run-the-crawl-from-the-docker-image)

```bash
docker run -it --env-file=.env -e "CONFIG=$(cat /path/to/your/config.json | jq -r tostring)" algolia/docsearch-scraper
```
> docker 安装使用和 jq 的安装请自行查询

config.json 示例
```json
{
  "index_name": "test",
  "start_urls": ["https://test.com/docs/"], // 此链接是你最终部署文档的地址
  "selectors": {
    "lvl0": "",
    "lvl1": ".content h1",
    "lvl2": ".content h2",
    "lvl3": ".content h3",
    "lvl4": ".content h4",
    "lvl5": ".content h5",
    "content": ".content p, .content li"
  }
}

```

