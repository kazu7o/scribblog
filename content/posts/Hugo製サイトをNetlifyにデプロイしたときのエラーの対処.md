---
title: "Hugo製サイトをNetlifyにデプロイしたときのエラーの対処"
date: 2020-02-12T17:57:23+09:00
author: ""
cover: ""
tags:
    - hugo
    - netlify
description: "Hugoで作成したサイトをNetlifyにデプロイしたらエラーが出た"
showFullContent: false
draft: false
---
Hugoで作成したサイトをNetlifyにデプロイしたらエラーが出たからメモしておく。

# 環境
Hugo v0.64.1
```bash
$ hugo version
Hugo Static Site Generator v0.64.1/extended linux/amd64 BuildDate: unknown
```

# 経緯
Hugoで作ったサイトをGithubにPush。

Netlifyから"New site from Git"でPushしたサイトをデプロイ。  
Build commandに"hugo"、Publish directoryに"public"を設定しデプロイを行ったところ、

![error-log](/posts/img/2020-02-12/netlify-error.png)  

"failed during stage 'building site': Build script returned non-zero exit code: 255"
そして、以下がデプロイログ。

```bash
8:10:03 PM: ERROR 2020/02/11 11:10:03 TERMINAL theme does not support Hugo version 0.54.0. Minimum version required is 0.57
```

# 解決
原因はNetlifyがインストールするHugoのバージョンを、使用しているHugoのテーマがサポートしていないことだった。
なので、Netlifyの方でインストールするHugoのバージョンを指定する。Settings -> Build & deploy -> EnvironmentからEdit variablesを選択し、次のように指定する。

![environment-variables](/posts/img/2020-02-12/environment-variables.png)

Valueの部分はローカルで使用しているHugoのバージョンを指定する。
最後にSaveをして、再度デプロイして終了。
