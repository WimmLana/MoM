# Git入門3　githubの初期設定〜基本的な使い方まで

* * *

#### gitの利用について、基礎的な知識が固まったら実際にgitとgithubを利用してみよう。

<br>

## Index:

1. 環境構築
2. ローカルレポジトリの作成
3. リモートレポジトリの構築
4. リモートレポジトリの更新
5. ローカルレポジトリの更新
6. ステータスなどの各種確認
7. 作業中のブランチを切り替える

<br>

## 0\. Immediate Actions

* * *

<br>

### **github推奨のファーストステップ**

### **…or create a new repository on the command line**

```
echo "# MoM" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/WimmLana/MoM.git
git push -u origin main

```

<br>

### …or push an existing repository from the command line

```
git remote add origin https://github.com/WimmLana/MoM.git
git branch -M main
git push -u origin main
```

<br>

`git branch -M main`  

A command used to forcefully rename the current active branch to "main", ensuring that the primary branch matches the modern standard naming convention.

masterで初期ブランチが作られる可能性があるが、master/slave or servantという言葉の使用を更新するため、mainという使用を行うことが慣習として、定着した

<br>

## 1\. 環境構築

* * *

<br>

`git config`  

Gitをインストールした直後や、新しい環境を構築した際に必ず行う設定です。**誰が変更したのか、履歴を残す＝commitした時の「名前」と「アドレス」を設定します。**  

<br>

```
git config --[scope] user.name "name"
git config --[scope] user.email "email"

git config --global user.name "To Your Sea"
git config --global user.email "iwltbtowccpos@gmail.com"

```

<br>

自分の今の設定を確認するには

```
git config --list

```

<br>

`git config` には設定の「有効範囲（スコープ）」が主に3種類あり、これらをオプションで使い分けるのが最大のポイントです。

#### 3つの有効範囲（スコープ）

|     |     |     |
| --- | --- | --- |
| **オプション** | **有効範囲（スコープ）** | **説明** |
| **`--system`** | **PC全ユーザー** | パソコン内のすべてのユーザー、すべてのプロジェクトに適用（管理者権限が必要で、あまり使いません）。 |
| **`--global`** | **ログインユーザー** | PC内の**すべてのGitリポジトリ（プロジェクト）に共通**で適用される設定です。<br> |
| **`--local`** | **現在のプロジェクト** | **今開いている特定のプロジェクト（フォルダ）だけ**に適用。<br>仕事用とプライベート用でアカウントを分けたいときに便利です。（省略すると自動的にこれになります） |

<br>

<br>

## 2\. ローカルレポジトリの作成

* * *

<br>

### Initilize

レポジトリの作成を行うコマンドです。管理したいフォルダに移動して、以下のコマンドを実行しましょう。

```
git init

```

initとは、initilizeのabbreviationです。これにより、フォルダに`.git`という隠しフォルダが作成されます。

これが、==ローカルレポジトリの正体==です。

<br>

つまり、”sourcecode\_feature\_…”のようなソースファイルが（ワークツリーに）あるとして、これを編集し（ステージング後）コミットすると、`.git` という隠しフォルダの中に、そのソースファイルの内容が反映されると考えるといいでしょう。

<br>

### staging

つまり、add = です！

全ての変更をステージングエリアに追加するには、以下のコマンドを使います。

```
git add .
```

特定のファイルだけを追加したい場合は、ファイル名を指定します。

```
git add ファイル名

```

<br>

### ステージング（`add`）の打ち消し

```
$ git reset HEAD <ファイル名>

```

<br>

<br>

`git commit`

* * *

<br>

==コミットするとき==は、「どんな変更をしたか」が後から見ても分かるように、==必ずメッセージを一緒に記録する==のがルールです。

```
git commit -m "ここにコミットメッセージを書く（例：最初のコミット）"

```

<br>

### コミットメッセージの例（慣習）

- **feat :** 投稿機能を開発しました
- **fix :** 投稿ができないバグを修正しました

他にもいくつかあります。詳細は、[操作時の注意点](%E6%93%8D%E4%BD%9C%E6%99%82%E3%81%AE%E6%B3%A8%E6%84%8F%E7%82%B9.md)を必ずチェック！

<br>

### コミットの打ち消し

```
$ git reset --hard HEAD^

```

<br>

<br>

## 3. リモートレポジトリの構築

* * *

<br>

リモート（外部サーバー）に関する設定を行うコマンド。

<br>

```
git remote add origin https://github.com/ユーザー名/リポジトリ名.git

```

※originは、ローカルレポジトリです。

<br>

### メインブランチ

- origin main = remote repository
- main = local repository

<br>

![](Files/image%204.png)

<br>

## ブランチの種類（概念的なもの）

- oursブランチ：自分が作業中のブランチ
- theirsブランチ：自分が作業していないブランチ

![](Files/image%205.png)

<br>

<br>

## 4. リモートレポジトリの更新

* * *

<br>

`push`  

<br>

```
git push origin <リモートリポジトリのブランチ名>

```

<br>

<br>

## 5\. ローカルレポジトリの更新

* * *

<br>

pull = fetch + mergeである。

<br>

### fetch 

更新情報の覗き見。「`git fetch` はリモートの最新履歴を『追跡ブランチ』という手元の隠しエリアにダウンロードするコマンド」

<br>

<br>

### merge

```
git merge <ブランチ名>⁠
git merge origin/<ブランチ名>
```

git fetchでリモートから取得したブランチをローカルブランチにマージするときは、「origin/」の追加が必須。

<br>

<br>

## 6\. ステータスの確認

* * *

<br>

### 移動

`cd <gitで管理したいフォルダ>`

<br>

### ローカルレポジトリの変更を見る

`git status`

<br>

### コミットの履歴をを見る

`log`

> これまでにそのリポジトリで行われた変更の記録（コミット履歴）を、過去から現在に向かってタイムライン順に一覧表示するコマンドです。  
> 「誰が」「いつ」「どんな目的で（コミットメッセージ）」変更したのか、またそれぞれの変更に割り振られた固有の識別番号（コミットハッシュ）を確認できます。  

<br>

### リモートとローカルの差分を見る

`diff`  

> 2つの状態を比較して、具体的に「どのファイルの、どの行が、どう書き換わったか（追加/削除されたか）」の差分を行単位で表示するコマンドです。  
> ファイルを編集した後、ステージングエリアに上げる前に自分の変更点を確認したり、ブランチ同士のコードの違いを比較したりする際に重宝します。

<br>

## 7\. 作業中のブランチの変更

* * *

<br>

ours : 今自分の作業中のブランチ <> theirs : 非作業中のブランチ

```
git checkout <Oursにしたいブランチ名>

```

<br>