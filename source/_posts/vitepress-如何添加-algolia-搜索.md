---
title: vitepress 如何开启 algolia 全文搜索
categories:
  - 未分类
date: 2022-11-01 18:05:41
tags:
---
> 此文章发表时，官方文档关于搜索部分还未更新。

## algolia 工作原理

你把你的网站数据上传到 algolia, 当你在你的网站上进行搜索时，会向 algolia 发送一个请求，algolia 在你上传的数据中进行搜索，然后把结果返回给你，你在你的网站上进行展示。

那么最关键的就是申请一个 algolia 账号，然后把你的数据上传上去。

上传数据有这么几种方法
1. 手动上传，algolia 支持 json 数据上传。
2. 使用官方提供的工具上传。（本文主要介绍）
3. 使用官方提供的 crawler 爬虫自动爬取。（需要拥有 crawler 权限）

## DocSearch

[DocSearch](https://docsearch.algolia.com/) 是 algolia 旗下的一款产品，主要做技术文档和技术博客的搜索，免费，但是申请条件比较严苛，需要人工审核。  
申请通过后可以使用官方提供的 crawler。官方也提供了 vitepress config template，操作比较简单。具体可参考[这篇文章](https://juejin.cn/post/7070109475419455519#heading-2)或官方文档。

DocSearch 申请条件
1. 你的网站可以公开访问
2. 你的网站是开源项目的技术文档或技术博客
3. 你是此网站的所有者
   
## 注册 algolia 账号
[algolia 官网](https://www.algolia.com/)

## 在 algolia 创建 index

下一步要用到

## 配置中开启 algolia

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
### appId 

setting -> Team and Access -> API keys -> Application ID

### apiKey

> 请勿使用 Admin API Key

setting -> Team and Access -> API keys -> `Search-Only API Key`

### indexName

上一步创建的 index 的名称


到这一步你的 vitepress 页面中应该能看到搜索框了，但是还无法搜索到结果，因为你还没上传数据到 algolia。

## 上传数据到 algolia

algolia 官方提供了 [crawler(爬虫)](https://docsearch.algolia.com/docs/manage-your-crawls/) 来爬取你网站的数据，直接在网站上操作，简单方便，但是需要 crawler 权限。

algolia 也提供了免费的方法，运行官方提供的 docker image 上传数据到 algolia。

> 此方法已进入 legacy 阶段，后期可能会失效。

[Run the crawl from the Docker image](https://docsearch.algolia.com/docs/legacy/run-your-own/#run-the-crawl-from-the-docker-image)

> docker 安装使用请自行查询  
> [install jq, a lightweight command-line JSON processor](https://github.com/stedolan/jq/wiki/Installation)

```bash
docker run -it --env-file=.env -e "CONFIG=$(cat /path/to/your/config.json | jq -r tostring)" algolia/docsearch-scraper
```
config.json 模板
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

