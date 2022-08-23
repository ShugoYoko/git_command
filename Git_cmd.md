# Git を使う

## 注目すべき点
リポジトリ（場所）、ブランチ（分岐点）、コミット（変更点）を意識する


## Git の基本
1)用語
-リポジトリ：ファイルやディレクトリをためる場所。ローカルとリモートが存在
-ブランチ：リポジトリの開発経路
-ヘッド：作業しているブランチ
-ステージングエリア（インデックスエリア）：Gitでインデックスされた変更
-ワーキングツリー：作業領域のファイル
-リビジョン：コミットした際に生成されるハッシュ値


## Git を使う
---<ワーキングツリーにおける操作>---
〇　Gitリポジトリの登録(.git ディレクトリを生成し管理用のメタデータを生成)
1)対象フォルダまで cd で移動
2)git init

〇　ファイルへの変更の取り消し
git restore <ファイル名> or <.>

〇　差分を比較する
git diff <ブランチ名>　<ブランチ名> <ファイル名>
git diff <ブランチ名>　<ブランチ名> 

〇　ファイルの変更内容の履歴
git blame (ファイル名)

〇　空のディレクトをgit管理するときは .gitkeep ファイルを作成して add → commit

〇　特定のファイルやフォルダをgit管理しない
.gitignore =* [ab] フォルダ名　を1行づつ記載

〇　git コマンドにエイリアスを付ける
git config --global alias.(短縮コマンド)　(gitコマンド)
.gitconfig ファイルに直接書く

〇　コミットやコピーをすることなく変更を保存し、ブランチを移動できるようにする
git stash

---<ワーキングツリー ⇄ インデックスエリア>---
〇　ステージングする（変更をステージングエリアに登録する）
git add ファイル名     若しくは
git add . (カレントディレクトリ内のファイル全て)

〇　ワーキングツリーとインデックスエリアの差分確認
git diff

〇　ステージングした変更を取り消す
git reset HEAD/git reset/git reset -- <ファイル名>

〇　ファイル・フォルダを削除しステージング
git rm (ファイル名)
git rm -r (フォルダ名)

〇　ファイル・フォルダを変更しステージング
git mv (元パス) (変更後パス)


---<インデックスエリア ⇄ ローカルリポジトリ>---
〇　コミットする（変更をローカルリポジトリに登録する）
git commit -m "メッセージ" (-mオプションはエディターなしでコミットするオプション)

〇　直前のコミットを修正
git commit --amend -m <メッセージ>

〇　コミットログの確認
git log --oneline (省略表示) -<表示数>

〇　他のブランチに特定のコミットを取り込む
git cherry-pick <コミットID:7桁以上=git log --oneline でコピー>　
                ,<取り込みたいコミットIDの1つ前>..<コミットID>
git cherry-pick --abort　(コミットの取り込みを中止)

〇　状態を確認する
git status

〇　インデックスエリアとローカルリポジトリの差分確認
git diff --cached

〇　コミットをインデックスエリアまで戻す
git reset --soft HEAD^

〇　HEAD,INDEX,ワーキングツリーを変更前に戻す
git reset --hard HEAD^ <or コミットID>

〇　コミット履歴の中身の確認
git show (コミットID) --oneline
git show (コミットID):(ファイル名)

〇　コミットの作業履歴、ブランチの切り替え作業、マージ作業の確認
git reflog -(表示数)

〇　指定したコミットをタグづけする
軽量タグ：git tag (タグ名) HEAD^ <1個前のコミットをベースにタグを付ける>
注釈タグ：git tag (タグ名) HEAD^^ -a -m "メッセージ"

リモートリポジトリにタグを反映
タグ全て：git push origin --tag
特定のタグ：git push origin (タグ名)

タグを確認:git show (タグ名)
タグを削除：git tag -d (タグ名)


---<ブランチ>---
〇　ブランチ名変更
git branch -m main 

〇　現在のブランチの全体像の確認(アスタリスクが現在いるブランチ)
git branch
git branch <ブランチ名> (ブランチの生成)
git branch -r(リモートブランチの確認)　-a(ローカルも含めたブランチの確認)　--merge(マージされているブランチの確認)

〇　コミットからブランチを作る
git branch <ブランチ名> <コミットID>
git switch -c <ブランチ名> <コミットID>

〇　ブランチの削除
git branch -d <ブランチ名>(ブランチの削除) -D  <ブランチ名>(マージされていないブランチの削除)

〇　ブランチの移動
git switch <ブランチ名>
git switch -c <ブランチ名> 「作成と同時に移動」

〇　ブランチ名の変更
git branch -m <変更前（省略可）> <変更後> 
　　　　　　-M<強制上書き>

〇　マージ(現在 HEAD が存在するブランチに他のブランチの変更を取り込む)
git merge <コミットしたいブランチ:dev>
マージはFast-Forwardで行われるため、分岐があれば取り込まれ、分岐が無ければ最新のコミットに移動
分岐が無い場合に取り組んだコミットにするためには --no-ff を使用

〇　別のブランチのコミットを取り組む(mergeと近い)=分岐がないイメージ
git rebase (ブランチ名)

〇　コミットを整理する=コミットの歴史修正になるので push 前に実施
git rebase -i (コミットID)

〇　コンフリクト(競合)が発生したら矛盾か所を修正して add →commit →merge

〇　detached HEAD:ブランチを参照することなく直接コミットを参照している状態
git switch でコミットを参照した際に発生しやすいが、ブランチを作って移動することで解消

---<リモートリポジトリ>---
〇　リモートブランチの登録(origin はリモートリポジトリのエイリアス)
git remote add origin (URL)

〇　リポジトリ名を変更したさいに、設定しなおす
git remote set-url origin <URL>
確認するコマンド: git remote -v

〇　ローカルのコミットのリモートリポジトリへの反映
1) git push origin (ローカルの反映したいブランチ)
2) push 後、Git Hub だと「pull Request」→「Compare pull request」
   →コメント 「Merge pull request」→「Confirm merge」

〇　前回と差異が出る等の際に無理やりリモートへ反映
git push -f origin main

〇　リモートリポジトリからローカルに持ってくる
git clone (URL)

〇　リモートの情報をローカル(origin/main)にコピー
1) git fetch origin main (リモート情報をコピー) / git fetch (リモート情報をフルコピー)
その後mainブランチにリモートリポジトリをマージ 
2) git merge origin/main
フェッチとマージを同時に行う場合
git pull origin main

〇　リモートリポジトリが進んでいてpushできない場合
git pull
コンフリクトが発生している場合は、git pull --rebase (中断するとき--abort)
解消できた場合、git pull --rebase --continue





## Git Hub
1) Setting → branch でデフォルトブランチの変更可能
2) File changed 「内容確認可能」
　Add single comment :コメントのやり取りが可能
　Start a review :レビュアーのみが変更可能
3) イシュー：Labels でラベリング可能
4) 他の Git Hub への貢献
Git Hub 上でフォーク、Fetch upstream でフォーク元のリポジトリ変更をマージ可能
(流れ)ローカルで変更→ git push →プルリクエスト
フォーク先と同期：git remote add upstream (URL)
リモートの情報をローカルにコピー: git fetch upstream
その後マージ： git merge upstream/main
5)　GitHub Actions:CI/CD をサポート
6)　フォースプッシュを防ぐ設定可能：「Setting」→「Branches」 →プロテクションルール作成可能

