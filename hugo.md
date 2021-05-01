gatsbyjs の katex 数式表示がうまくいかなかったので hugo を使ってみる．

[Install Hugo | Hugo](https://gohugo.io/getting-started/installing/)

scoop install hugo

[HUGOでMarkdownを使った技術ドキュメントの管理が良い - karakaram-blog](https://www.karakaram.com/hugo-usage/)

cd D:\src

hugo new site hugo-hello-docs
cd hugo-hello-docs
git init

テーマを追加
git submodule add https://github.com/matcornic/hugo-theme-learn.git themes/learn

`config.toml` を編集してテーマを追加

hugo new posts/my-first-post.md

hugo server -D

katex はうまくいかなかった．
[Hugo で KaTeX | Atusy's blog](https://blog.atusy.net/2019/05/09/katex-in-hugo/)

---

hugo new site hugo-hello-katex
cd hugo-hello-katex
git init
git submodule add https://github.com/zzossig/hugo-theme-zzo.git themes/zzo

config.toml
```toml
theme = "zzo"
```

[HugoのテーマをZzoに変更した – sakojunblog](https://sakojun.work/posts/20200606_hugo%E3%81%AE%E3%83%86%E3%83%BC%E3%83%9E%E3%82%92zzo%E3%81%AB%E5%A4%89%E6%9B%B4%E3%81%97%E3%81%9F/#)

scoop install hugo-extended

[Hugo + GithubPages でブログを構築する – BAMBi's Blog](https://www.anypalette.com/ja/posts/1012_first_post/)