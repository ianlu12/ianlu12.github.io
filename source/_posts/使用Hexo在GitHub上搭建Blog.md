---
title: 使用Hexo在GitHub上搭建Blog
date: 2020-10-13 17:08:30
categories: Hexo
tags: [Hexo,Git]
---
# 安裝環境

- node.js
- git

## 安裝Hexo建立Blog

安裝 hexo

安裝hexo
```
npm install -g hexo-cli
```

查詢當前hexo版本
```
hexo -v
```

## 初始化Blog

建立一個要存放Blog檔案的資料夾
```
mkdir <Blog資料夾>
cd <Blog資料夾>
```

初始化Blog，生成檔案
```
hexo init
```

啟動Blog
```
hexo s
```
開啟瀏覽器至http://localhost:4000/可以看到你的BLOG
發表文章

## 建立文章
```
hexo n "<文章標題>"
```

使用編輯器修改source/_post/<文章標題>.md的文章內容

生成靜態網頁
```
hexo g
```

接者在啟動Blog就可以看到你的文章更新到Blog裡囉!
```
hexo s
```

## 修改主題

這邊使用NexT主題為例

下載主題的檔案
```bash
git clone https://github.com/iissnan/hexo-theme-next themes/next
```

啟用主題
修改_config.yml
```yml
theme: next
```
新增留言功能

這邊以Disqus留言評論功能為例，首先要去Disqus官網創建一個帳號，接著把相對應的資料填入主題配置當中。
修改themes/next/_config.yml，填入你建立的Disqus shortname
```yml
# Disqus 
disqus: 
  enable: true 
  shortname: <your_disqus_short_name>
  count: true
```
# 新增文章分類(Categories)

建立分類頁面
```bat
hexo new page categories
```

修改產生的 source/categories/inex.md 成下面的樣子
```markdown
--- 
title: categories 
date: 2019-04-01 22:52:41 
type: "categories" 
---
```

讓文章增加分類，只要在 categories 後面加入類別就可以了
```markdown
--- 
title: 新的文章 
date: 2017-05-26 12:12:57 
categories: 文章類別 
---
```
# 增加標籤 (tags)

```
hexo new page tags
```

接著修改剛剛產生的 source/tags/inex.md 成下面的樣子並儲存。
```
--- 
title: categories 
date: 2019-04-01 22:55:41 
type: "tags" 
---
```

讓文章增加分類，只要在 tags 後面加入標籤就可以了，一樣記得要空格！
```
--- 
title: 新的文章 
date: 2017-05-26 12:12:57 
categories: 文章類別 
tags: 標籤_1 標籤_2 
---
```
一篇文章只可以有一個類別，但是可以同時有很多個標籤，不同的標籤要用空格來分開。

# 修改文章鷹架

修改文章的鷹架文章自動生成categories和tags，不用再手動輸入

修改scaffolds/post.md為
```yml
title: {{ title }} 
date: {{ date }} 
categories: {{ categories }} 
tags: {{ tags }}
```
這樣每次產生新的文章就會自動帶入 categories 跟 tags 了。

以上修改完後，記得還要去主題配置的 menu 中把 categories 跟 tags 打開，這樣才能在側欄中看到喔！

部屬到GitHub

新增GitHub repository

至github新增一個repository
Repository name取名為<帳號名稱>.github.io
安裝Git部屬插件

回到Blog資料夾
```bash
cd <Blog資料夾>
npm install --save hexo-deployer-git
```

修改hexo的設定檔_config.yml
```yml
# Deployment 
## Docs: https://hexo.io/docs/one-command-deployment 
deploy: 
  type: git 
  repo: https://github.com/<帳戶名稱>/<帳戶名稱>.github.io.git 
  branch: master
```

# 部屬到遠端
```bat
hexo d
```

要同時生成並部屬的話可使用下列兩種指令
```sh
hexo d -g
hexo g -d
```

# 參考

- https://hexo.io/zh-tw/docs/
- https://theme-next.iissnan.com/