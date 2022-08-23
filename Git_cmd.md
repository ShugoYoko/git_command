# Git を使う

## 注目すべき点
リポジトリ（場所）、ブランチ（分岐点）、コミット（変更点）を意識する


## Git の基本
1)用語<br>
-リポジトリ：ファイルやディレクトリをためる場所。ローカルとリモートが存在<br>
-ブランチ：リポジトリの開発経路<br>
-ヘッド：作業しているブランチ<br>
-ステージングエリア（インデックスエリア）：Gitでインデックスされた変更<br>
-ワーキングツリー：作業領域のファイル<br>
-リビジョン：コミットした際に生成されるハッシュ値<br>


## Git を使う
---<ワーキングツリーにおける操作>---<br>
〇　Gitリポジトリの登録(.git ディレクトリを生成し管理用のメタデータを生成)<br>
1)対象フォルダまで cd で移動<br>
2)git init<br>
<br>
〇　ファイルへの変更の取り消し<br>
git restore <ファイル名> or <.><br>
<br>
〇　差分を比較する<br>
git diff <ブランチ名>　<ブランチ名> <ファイル名><br>
git diff <ブランチ名>　<ブランチ名> <br>
<br>
〇　ファイルの変更内容の履歴<br>
git blame (ファイル名)<br>
<br>
〇　空のディレクトをgit管理するときは .gitkeep ファイルを作成して add → commit<br>
<br>
〇　特定のファイルやフォルダをgit管理しない<br>
.gitignore =* [ab] フォルダ名　を1行づつ記載<br>
<br>
〇　git コマンドにエイリアスを付ける<br>
git config --global alias.(短縮コマンド)　(gitコマンド)<br>
.gitconfig ファイルに直接書く<br>
<br>
〇　コミットやコピーをすることなく変更を保存し、ブランチを移動できるようにする<br>
git stash<br>
<br>
---<ワーキングツリー ⇄ インデックスエリア>---<br>
〇　ステージングする（変更をステージングエリアに登録する）<br>
git add ファイル名     若しくは<br>
git add . (カレントディレクトリ内のファイル全て)<br>
<br>
〇　ワーキングツリーとインデックスエリアの差分確認<br>
git diff<br>
<br>
〇　ステージングした変更を取り消す<br>
git reset HEAD/git reset/git reset -- <ファイル名><br>
<br>
〇　ファイル・フォルダを削除しステージング<br>
git rm (ファイル名)<br>
git rm -r (フォルダ名)<br>
<br>
〇　ファイル・フォルダを変更しステージング<br>
git mv (元パス) (変更後パス)<br>
<br>

---<インデックスエリア ⇄ ローカルリポジトリ>---<br>
〇　コミットする（変更をローカルリポジトリに登録する）<br>
git commit -m "メッセージ" (-mオプションはエディターなしでコミットするオプション)<br>
<br>
〇　直前のコミットを修正<br>
git commit --amend -m <メッセージ><br>
<br>
〇　コミットログの確認<br>
git log --oneline (省略表示) -<表示数><br>
<br>
〇　他のブランチに特定のコミットを取り込む<br>
git cherry-pick <コミットID:7桁以上=git log --oneline でコピー><br>　
                ,<取り込みたいコミットIDの1つ前>..<コミットID><br>
git cherry-pick --abort　(コミットの取り込みを中止)<br>
<br>
〇　状態を確認する<br>
git status<br>
<br>
〇　インデックスエリアとローカルリポジトリの差分確認<br>
git diff --cached<br>
<br>
〇　コミットをインデックスエリアまで戻す<br>
git reset --soft HEAD^<br>
<br>
〇　HEAD,INDEX,ワーキングツリーを変更前に戻す<br>
git reset --hard HEAD^ <or コミットID><br>
<br>
〇　コミット履歴の中身の確認<br>
git show (コミットID) --oneline<br>
git show (コミットID):(ファイル名)<br>
<br>
〇　コミットの作業履歴、ブランチの切り替え作業、マージ作業の確認<br>
git reflog -(表示数)<br>
<br>
〇　指定したコミットをタグづけする<br>
軽量タグ：git tag (タグ名) HEAD^ <1個前のコミットをベースにタグを付ける><br>
注釈タグ：git tag (タグ名) HEAD^^ -a -m "メッセージ"<br>
<br>
リモートリポジトリにタグを反映<br>
タグ全て：git push origin --tag<br>
特定のタグ：git push origin (タグ名)<br>
<br>
タグを確認:git show (タグ名)<br>
タグを削除：git tag -d (タグ名)<br>
<br>

---<ブランチ>---<br>
〇　ブランチ名変更<br>
git branch -m main <br>
<br>
〇　現在のブランチの全体像の確認(アスタリスクが現在いるブランチ)<br>
git branch<br>
git branch <ブランチ名> (ブランチの生成)<br>
git branch -r(リモートブランチの確認)　-a(ローカルも含めたブランチの確認)　--merge(マージされているブランチの確認)<br>
<br>
〇　コミットからブランチを作る<br>
git branch <ブランチ名> <コミットID><br>
git switch -c <ブランチ名> <コミットID><br>
<br>
〇　ブランチの削除<br>
git branch -d <ブランチ名>(ブランチの削除) -D  <ブランチ名>(マージされていないブランチの削除)<br>
<br>
〇　ブランチの移動<br>
git switch <ブランチ名><br>
git switch -c <ブランチ名> 「作成と同時に移動」<br>
<br>
〇　ブランチ名の変更<br>
git branch -m <変更前（省略可）> <変更後> <br>
　　　　　　-M<強制上書き><br>
<br>
〇　マージ(現在 HEAD が存在するブランチに他のブランチの変更を取り込む)<br>
git merge <コミットしたいブランチ:dev><br>
マージはFast-Forwardで行われるため、分岐があれば取り込まれ、分岐が無ければ最新のコミットに移動<br>
分岐が無い場合に取り組んだコミットにするためには --no-ff を使用<br>
<br>
〇　別のブランチのコミットを取り組む(mergeと近い)=分岐がないイメージ<br>
git rebase (ブランチ名)<br>
<br>
〇　コミットを整理する=コミットの歴史修正になるので push 前に実施<br>
git rebase -i (コミットID)<br>
<br>
〇　コンフリクト(競合)が発生したら矛盾か所を修正して add →commit →merge<br>
<br>
〇　detached HEAD:ブランチを参照することなく直接コミットを参照している状態<br>
git switch でコミットを参照した際に発生しやすいが、ブランチを作って移動することで解消<br>
<br>

---<リモートリポジトリ>---<br>
〇　リモートブランチの登録(origin はリモートリポジトリのエイリアス)<br>
git remote add origin (URL)<br>
<br>
〇　リポジトリ名を変更したさいに、設定しなおす<br>
git remote set-url origin <URL><br>
確認するコマンド: git remote -v<br>
<br>
〇　ローカルのコミットのリモートリポジトリへの反映<br>
1.git push origin (ローカルの反映したいブランチ)<br>
2.push 後、Git Hub だと「pull Request」→「Compare pull request」<br>
→コメント 「Merge pull request」→「Confirm merge」<br>
<br>
〇　前回と差異が出る等の際に無理やりリモートへ反映<br>
git push -f origin main<br>
<br>
〇　リモートリポジトリからローカルに持ってくる<br>
git clone (URL)<br>
<br>
〇　リモートの情報をローカル(origin/main)にコピー<br>
1.git fetch origin main (リモート情報をコピー) / git fetch (リモート情報をフルコピー)<br>
その後mainブランチにリモートリポジトリをマージ <br>
2.git merge origin/main<br>
フェッチとマージを同時に行う場合<br>
git pull origin main<br>
<br>
〇　リモートリポジトリが進んでいてpushできない場合<br>
git pull<br>
コンフリクトが発生している場合は、git pull --rebase (中断するとき--abort)<br>
解消できた場合、git pull --rebase --continue<br>
<br>

## Git Hub
1.Setting → branch でデフォルトブランチの変更可能<br>
2.File changed 「内容確認可能」<br>
Add single comment :コメントのやり取りが可能<br>
Start a review :レビュアーのみが変更可能<br>
3.イシュー：Labels でラベリング可能<br>
4.他の Git Hub への貢献<br>
Git Hub 上でフォーク、Fetch upstream でフォーク元のリポジトリ変更をマージ可能<br>
(流れ)ローカルで変更→ git push →プルリクエスト<br>
フォーク先と同期：git remote add upstream (URL)<br>
リモートの情報をローカルにコピー: git fetch upstream<br>
その後マージ： git merge upstream/main<br>
5.GitHub Actions:CI/CD をサポート<br>
6.フォースプッシュを防ぐ設定可能：「Setting」→「Branches」 →プロテクションルール作成可能<br>

