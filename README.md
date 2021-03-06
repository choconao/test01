# Git / GitHub
- Gitとは
- GitHubとは

## Gitとは
ソースコードのバージョン管理システム。
これ自体はソフトウェアであり、ローカルマシンでも動き、ローカルのファイルを管理できる。
(macにはデフォルトでインストールされているので、ターミナルでgit --verionと打つgitのversionが表示される）


## GitHubとは
GitHubとは、gitを使ったソースコード管理を、クラウドで共有できるプラットフォーム。
チーム開発などで使える。
GitHubに限らず、このようなプラットフォームは多々ある。(BitBucketなど）


## 出てくる用語
**リポジトリ**
gitの管理下に置くディレクトリ/場所/プロジェクトのこと
ローカルリポジトリとリモートリポジトリに分かれる。ローカルは自分のPCのディレクトリ、リモートはGitHub上のもの。


**コミット**  
変更内容をローカルリポジトリに反映させること


**プッシュ**  
ローカルリポジトリのコミットを、リモートリポジトリに反映させること

**プル**  
リモートリポジトリの変更を、ローカルリポジトリに反映させること

**フェッチ**  
リモートリポジトリの変更があるか確認すること。あればプル。

**マージ**  
異なるブランチの変更を反映すること

**ブランチ**  
枝分かれさせて使う作業スペース

**コンフリクト**  
マージ対象のファイルに対して、複数者による変更がされており、マージできないこと。エラーを治してからマージする。

**ブランチ**  
枝分かれさせて使う作業スペース



## 使い方
ワークフローという、作業の進め方の考え方がチームごとに存在する。
有名なものが、git-flow。

### Git-flow
5つのタイプのブランチを使って開発していく。
- master -> 最新のリリース状態を保持する。このブランチで作業するのはダメ。
- develop -> masterからブランチを作成する。基本的にここでも作業しない。
- feature/ -> developからブランチを作成する。基本的に機能ごとにこのブランチを作り、ここで作業する。feature/create-header, feature/html-footerなど機能が分かりやすい名前にして作る。
- release -> developからブランチを作成。リリース直前のリリース用のもの。終わり次第、masterとdevelopにマージする。
- hotfix -> masterブランチから作成。リリース後のバグの**緊急対応用**。終わり次第、masterとdevelopにマージする。


#### Git-flow開発の流れ
1. リモートリポジトリからブルして、ソースコードを最新の状態にする。
1. developからfeatureブランチを切る
2. featureブランチで作業し、コミットし、プッシュする。
3. 親ブランチ(develop)にプルリクエストを出す
4. コードレビューが終わったら確認者にマージ及びfeatureブランチの削除をしてもらう
5. リリース当日はdevelopからreleaseブランチを切って、万が一修正があればreleaseブランチから修正ブランチを作って作業し、releaseブランチに向けてプルリクエストを出してマージ
6. releaseブランチをmasterとdevelopにマージする。masterにタグ(リリース管理するバージョンや名前)付けをしてリリース（jenkinsなどのciツールなどを使用してデプロイする場合はタグでビルドする）。
※releaseブランチは問題なければリリース作業者が削除


##### 緊急不具合対応編
1. masterからhotfixブランチを切ってそこからfeatureブランチを作成
2. featureブランチで作業完了及びデバッグ完了したらhotfixブランチにプルリクエストを出しレビュアーにマージしてもらう
3. hotfixブランチをmasterとdevelopにマージする
4. masterブランチにタグ(リリース管理するバージョンや名前)付けをしてmasterとdevelopにマージしてリリース（jenkinsなどのciツールなどを使用してデプロイする場合はタグでビルドする）。
※hotfixブランチ問題なければhotfixブランチ作業者が削除



