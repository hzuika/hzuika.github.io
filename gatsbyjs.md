# GitHub pages を Gatsby で作成する

[The Fastest Frontend for the Modern Web | Gatsby](https://www.gatsbyjs.com/)

```powershell
scoop install nodejs
```

```posershell
npm --version
7.11.1
```

```powershell
node --version
v16.0.0
```

```powershell
scoop install git
```

```powershell
npm install -g gatsby-cli

npm WARN ERESOLVE overriding peer dependency
npm WARN Found: graphql@15.5.0
npm WARN node_modules/gatsby-cli/node_modules/graphql
npm WARN   graphql@"^15.4.0" from gatsby-recipes@0.14.0
npm WARN   node_modules/gatsby-cli/node_modules/gatsby-recipes
npm WARN     gatsby-recipes@"^0.14.0" from gatsby-cli@3.3.0
npm WARN     node_modules/gatsby-cli
npm WARN   2 more (@graphql-tools/schema, @graphql-tools/utils)
npm WARN
npm WARN Could not resolve dependency:
npm WARN peer graphql@"^14.4.1" from express-graphql@0.9.0
npm WARN node_modules/gatsby-cli/node_modules/express-graphql
npm WARN   express-graphql@"^0.9.0" from gatsby-recipes@0.14.0
npm WARN   node_modules/gatsby-cli/node_modules/gatsby-recipes
npm WARN deprecated @hapi/topo@3.1.6: This version has been deprecated and is no longer supported or maintained
npm WARN deprecated @hapi/bourne@1.3.2: This version has been deprecated and is no longer supported or maintained
npm WARN deprecated @hapi/address@2.1.4: Moved to 'npm install @sideway/address'
npm WARN deprecated @hapi/hoek@8.5.1: This version has been deprecated and is no longer supported or maintained
npm WARN deprecated @hapi/joi@15.1.1: Switch to 'npm install joi'

added 575 packages, and audited 576 packages in 24s

105 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
```

```powershell
gatsby -v
╔════════════════════════════════════════════════════════════════════════╗
║                                                                        ║
║   Gatsby collects anonymous usage analytics                            ║
║   to help improve Gatsby for all users.                                ║
║                                                                        ║
║   If you'd like to opt-out, you can use `gatsby telemetry --disable`   ║
║   To learn more, checkout https://gatsby.dev/telemetry                 ║
║                                                                        ║
╚════════════════════════════════════════════════════════════════════════╝
Gatsby CLI version: 3.3.0
```

```powershell
git branch -m "dev"
```

```powershell
gatsby new hello-world https://github.com/gatsbyjs/gatsby-starter-hello-world

info Creating new site from git: https://github.com/gatsbyjs/gatsby-starter-hello-world.git

Cloning into 'hello-world'...
remote: Enumerating objects: 16, done.
remote: Counting objects: 100% (16/16), done.
remote: Compressing objects: 100% (11/11), done.
remote: Total 16 (delta 0), reused 9 (delta 0), pack-reused 0
success Created starter directory layout
info Installing packages...
info Preferred package manager set to "npm"


added 1963 packages, and audited 1964 packages in 2m

info
Your new Gatsby site has been successfully bootstrapped. Start developing it by running:

  cd hello-world
  gatsby develop
```

```powershell
cd hello-world
gatsby develop
```

Nodejs Firewall Private Access ON

```powershell
gatsby develop

success open and validate gatsby-configs - 0.083s
success load plugins - 0.281s
success onPreInit - 0.047s
success initialize cache - 0.011s
success copy gatsby files - 0.792s
success onPreBootstrap - 0.046s
success createSchemaCustomization - 0.001s
success Checking for changed pages - 0.001s
success source and transform nodes - 0.020s
success building schema - 0.211s
info Total nodes: 18, SitePage nodes: 1 (use --verbose for breakdown)
success createPages - 0.003s
success Checking for changed pages - 0.002s
success createPagesStatefully - 0.037s
success update schema - 0.031s
success write out redirect data - 0.003s
success onPostBootstrap - 0.001s
info bootstrap finished - 14.863s
success onPreExtractQueries - 0.001s
success extract queries from components - 0.082s
success write out requires - 0.007s
success run page queries - 0.023s - 2/2 85.90/s

 ERROR 

(node:8924) [DEP0148] DeprecationWarning: Use of deprecated folder mapping "./" in the "exports" field module resolution of the package at
d:\Documents\GitHub\hzuika.github.io\hello-world\node_modules\css-loader\node_modules\postcss\package.json.
Update this package.json to use a subpath pattern like "./*".
(Use `node --trace-deprecation ...` to show where the warning was created)


 ERROR 

(node:8924) [DEP0148] DeprecationWarning: Use of deprecated folder mapping "./" in the "exports" field module resolution of the package at d:\Documents\GitHub\hzuika.github.io\hello-world\node_modules\postcss\package.json.   
Update this package.json to use a subpath pattern like "./*".

⠀
You can now view gatsby-starter-hello-world in the browser.
⠀
  http://localhost:8000/
⠀
View GraphiQL, an in-browser IDE, to explore your site's data and schema
⠀
  http://localhost:8000/___graphql
⠀
Note that the development build is not optimized.
To create a production build, use gatsby build
⠀
success Building development bundle - 19.026s
```

```
cmd
```

```cmd
gatsby develop

success open and validate gatsby-configs - 0.076s
success load plugins - 0.053s
success onPreInit - 0.032s
success initialize cache - 0.006s
success copy gatsby files - 0.593s
success onPreBootstrap - 0.013s
success createSchemaCustomization - 0.001s
success Checking for changed pages - 0.002s
success source and transform nodes - 0.024s
success building schema - 0.182s
info Total nodes: 18, SitePage nodes: 1 (use --verbose for breakdown)
success createPages - 0.003s
success Checking for changed pages - 0.001s
success createPagesStatefully - 0.031s
success update schema - 0.031s
success write out redirect data - 0.003s
success onPostBootstrap - 0.001s
info bootstrap finished - 3.334s
success onPreExtractQueries - 0.001s
success extract queries from components - 0.086s
success write out requires - 0.007s
success run page queries - 0.033s - 1/1 30.17/s

 ERROR 

(node:25560) [DEP0148] DeprecationWarning: Use of deprecated folder mapping "./" in the "exports" field module resolution of the package at
d:\Documents\GitHub\hzuika.github.io\hello-world\node_modules\css-loader\node_modules\postcss\package.json.
Update this package.json to use a subpath pattern like "./*".
(Use `node --trace-deprecation ...` to show where the warning was created)


 ERROR 

(node:25560) [DEP0148] DeprecationWarning: Use of deprecated folder mapping "./" in the "exports" field module resolution of the package at d:\Documents\GitHub\hzuika.github.io\hello-world\node_modules\postcss\package.json.  
Update this package.json to use a subpath pattern like "./*".

⠀
You can now view gatsby-starter-hello-world in the browser.
⠀
  http://localhost:8000/
⠀
View GraphiQL, an in-browser IDE, to explore your site's data and schema
⠀
  http://localhost:8000/___graphql
⠀
Note that the development build is not optimized.
To create a production build, use gatsby build
⠀
success Building development bundle - 3.291s

```

```diff
-    "./": "./"
+    "./*": "./*"
```

https://localhost:8000
Hello World!

---

```powershell
npm init gatsby

Need to install the following packages:
  create-gatsby
Ok to proceed? (y) y
create-gatsby version 1.3.0



                                                                                                        Welcome to Gatsby!



This command will generate a new Gatsby site for you in C:\Users\hashi\Documents\GitHub with the setup you select. Let's answer some questions:


What would you like to call your site?
√ · My Gatsby Site
What would you like to name the folder where your site will be created?
√ GitHub/ my-gatsby-site
√ Will you be using a CMS?
· No (or I'll add it later)
√ Would you like to install a styling system?
· No (or I'll add it later)
√ Would you like to install additional features with other plugins?No items were selected


Thanks! Here's what we'll now do:

    Create a new Gatsby site in the folder my-gatsby-site

√ Shall we do this? (Y/n) · Yes
√ Created site from template
√ Installed Gatsby
√ Installed plugins
√ Created site in my-gatsby-site
Your new Gatsby site My Gatsby Site has been successfully created
at C:\Users\hashi\Documents\GitHub\my-gatsby-site.
Start by going to the directory with

  cd my-gatsby-site

Start the local development server with

  npm run develop

See all commands at

  https://www.gatsbyjs.com/docs/gatsby-cli/
```

---

```powershell
gatsby new gatsby-starter-blog https://github.com/gatsbyjs/gatsby-starter-blog
cd gatsby-starter-blog
gatsby develop
```

---

2021-05-01 01:59:58
[Set Up Your Development Environment | Gatsby](https://www.gatsbyjs.com/docs/tutorial/part-zero/)

```
npm --version
7.11.1
gatsby --version
Gatsby CLI version: 3.3.0
```

拡張機能のインストール
```
code --install-extension esbenp.prettier-vscode
```

[Gatsby + Markdownでブログを作り直しました](https://diff001a.netlify.app/gatsby-blog-with-markdown/)

cd .\gatsby-starter-blog\
gatsby develop
http://localhost:8000/
npm install --save gatsby-remark-prismjs prismjs gatsby-remark-katex katex

[Test Site - GatsbyJSでブログを作った時のメモ](https://brainvader.github.io/brain-space/blog/2019/04/post-001/)

gatsby new gatsby-starter-lumen https://github.com/alxshelepenok/gatsby-starter-lumen


---

2021-05-01 09:36:29
katex が表示されないのでチュートリアルから始めていく．

2021-05-01 09:36:00

`gatsby new gatsby-hello-world https://github.com/gatsbyjs/gatsby-starter-hello-world`
`cd gatsby-hello-world`
`gatsby develop`

```
(node:19316) [DEP0148] DeprecationWarning: Use of deprecated folder mapping "./" in the "exports" field module resolution of the package at
D:\src\gatsby-hello-world\node_modules\postcss\package.json.
Update this package.json to use a subpath pattern like "./*".
(Use `node --trace-deprecation ...` to show where the warning was created)
```

```diff
-   "./": "./"
+   "./*": "./*"
```

`src/pages/index.js`の`Home()`の戻り値のHTMLを変更することで，コンテンツを変えられる．

index.jsはjsxの書き方

新規ページは`src/pages`の中に作る．

使いまわす部分は`src/components`を新規作成し，その中に関数とともに入れる．
使いたいところでは`import`したのち，HTMLタグのように書く．

使いまわす関数は，引数を使うことで，タグのプロパティ値を使って変更が可能．

リンクを使うためには `Link` をインポートして，`Link`タグを使う．

[Introduction to Styling in Gatsby | Gatsby](https://www.gatsbyjs.com/docs/tutorial/part-two/)

`./gatsby-browser.js`でインポートしたcssファイルはすべてのページに適用される．

component-scoped CSSを使用して，特定のページにのみcssを適用する

[Creating Nested Layout Components | Gatsby](https://www.gatsbyjs.com/docs/tutorial/part-three/)

インストールパッケージがサポートしているバージョンとプロジェクトのバージョンの対応
最新版reactだとエラーになる．
`--save --legacy-peer-deps`オプションを使うか，reactのバージョンを下げる．

```
npm install gatsby-plugin-typography react-typography typography typography-theme-fairy-gates --save --legacy-peer-deps
```

`gatsby-config.js`を編集する．

typographyプラグインは Configuration File を必要とする．

`components/layout.js` でテンプレートを作る．

---

[Data in Gatsby | Gatsby](https://www.gatsbyjs.com/docs/tutorial/part-four/)

```powershell
npm install gatsby-plugin-typography typography react-typography typography-theme-kirkham gatsby-plugin-emotion @emotion/react --save --legacy-peer-deps
```

---

[Source Plugins | Gatsby](https://www.gatsbyjs.com/docs/tutorial/part-five/)

npm install gatsby-source-filesystem

gatsby-config.js を編集

graphqlのqueryでdataとして取得できる．

---

2021-05-01 18:13:54

[Transformer plugins | Gatsby](https://www.gatsbyjs.com/docs/tutorial/part-six/)

markdown ファイルを作成

npm install gatsby-transformer-remark

GraphQLのオートコンプリートが確認できる．

追加したmarkdownファイルをGraphQLのqueryで取得できる．

---

[Programmatically create pages from data | Gatsby](https://www.gatsbyjs.com/docs/tutorial/part-seven/)

一番上の階層に作成した`./gatsby-node.js`で，スラグ(URLの識別部分)を作成

`./src/templates/blog-post.js`でmarkdownをどのようにhtmlに変換するか記述

---

[gatsby-remark-katex | Gatsby](https://www.gatsbyjs.com/plugins/gatsby-remark-katex/)


`npm install gatsby-transformer-remark gatsby-remark-katex katex`

数式が表示されなかった．