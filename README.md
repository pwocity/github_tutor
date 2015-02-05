# github_tutor

== 1st
create a new repository on the command line
--------------------------------------
echo # github_tutor >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/pwocity/github_tutor.git
git push -u origin master
------------------------------------------


commitとpushしかできない人のためのgithubの使い方まとめ
github
github(というよりgit)使っている方は結構な数いらっしゃると思います。
私もそのうちの一人ですが、正直「addしてcommitしてpushするだけ」です、はい。
branchとかmergeとかfetchとかあの辺がいまいちわからない情弱です。

あんまりこの辺をまとめて書いた記事が見当たらなかったのでまとめることにしました。
基本的にはgithub:helpの要約だと思ってくださればよいかと思います。

レポジトリを作る

レポジトリ

gitで作ったレポジトリは./.git以下に全てのcommitなどが保存されます。gitはさらにリモートでレポジトリを持つことができ、これの一つがgithub repositoryになります。

レポジトリの作り方:

$ mkdir ~/Hello-World
# "Hello-World"ディレクトリを作ります

$ cd ~/Hello-World
# 作ったディレクトリに移動します

$ git init
# 必要なGitファイルを用意します
# ./.gitディレクトリの中身が空のgitとして初期化されます

$ touch README
# "README"ファイルをこのディレクトリに作ります
次は適当にREADMEを書きましょう。分からなければ参考文献[2]の辺を読んで下さい。

コミット

READMEがかけたらいよいよcommitです！
gitにはzips, rars, jarsのような圧縮ファイル, obj, lib, exeのようなコンパイル済みファイル,データベースのバックアップ, flv, psdや音楽、メディアファイルなどのサイズの大きいファイルは置かないほうがbetterです。最悪の場合レポジトリが壊れることがあります。

コミットの仕方:

git add README
# READMEファイルをコミットするファイルに加えます

git commit -m 'first commit'
# メッセージ付きでコミットを行います
プッシュ

さて、commitが出来たらあなたのローカルレポジトリはちゃんと更新されています。今度はこれをリモートのgithubの方にも反映させなくてはいけません。これを行う操作がプッシュです。

git remote add origin https://github.com/username/Hello-World.git
# originと呼ばれる名前でリモートを追加します(リモートのレポジトリで一番良く使うものをoriginとするのが一般的なようです)

git push origin master
# "master"ブランチのコミット内容をgithubに送ります
以上がリポジトリを作ってからの一連の流れになります。

リポジトリをフォークする

フォーク

リポジトリをフォークすれば、色々な人の開発に貢献できます。
気になるレポジトリをフォークボタンからフォークすることができます。

クローン

フォークしたリポジトリをローカルに置かなければ開発ができません。そのためにクローンを行います。

git clone https://github.com/username/Spoon-Knife.git
# フォークした"username"さんの"Spoon-Knife"リポジトリをローカルにクローンします
リモートの設定

リポジトリをクローンすると、それは元のリポジトリではなくてあなたのフォークリポジトリとしてoriginという名前でgithubに置かれています。元のリポジトリの変更などを反映させるためには、upstreamと呼ばれる別のリモートを追加しなくてはいけません。

cd Spoon-Knife
# ディレクトリを変更します
git remote add upstream https://github.com/octocat/Spoon-Knife.git
# 元のリポジトリをupstreamと呼ばれるリモートに割り当てます

git fetch upstream
# あなたのファイルを修正せずに、ローカルに元のリポジトリの変更などを引っ張ります
フォークしたリポジトリにプッシュ

普通にプッシュする時と全く同じようにすれば、あなたのフォークしたリポジトリの方に変更が加えられます

git push origin master
元のリポジトリの変更を引っ張る(pull)

元のリポジトリが更新された場合、それを自分のリポジトリに引っ張る(同じように更新する)ことができます
githubではpullと呼ばれます

git fetch upstream
# 元のリポジトリの変更情報を自分のリポジトリに伝えます

git merge upstream/master
# あなたの開発中のファイルに反映させます
branchを加える

ブランチを加えるのは、新しい機能を加えたり実験的な変更を行うのに便利です。gitではブランチは常に最終コミットを保存しているという意味ではブックマークのようなものと考えてもよいでしょう。

git branch mybranch
# "mybranch"という名前で新しいブランチを作ります

git checkout mybranch
# "mybranch"をアクティブなブランチにします
# ブランチをスイッチするのにはこのコマンドを使います

## branchしてcheckoutするのが面倒な場合は
# git checkout -b mybranch
## とすれば一発でブランチを作ってからアクティブにするまでを行えます
ブランチで作業が終わり、元のブランチに追加させたくなれば、mergeを行えば良いです。

git checkout master
git merge mybranch
# "mybranch"から"master"ブランチに変更を追加し、反映させます

git branch -d mybranch
# "mybranch"ブランチを削除します
pullとfetch、何が違うの？

git pullではあなたの開発中のファイルに、変更点を伝えずに自動的に変更を反映させます。ブランチをしっかり管理していなければ、頻繁に衝突が起こる可能性があります。
fetchでは、まずはフォークした元のリポジトリの変更点を取得します。ここではまだあなたのファイルは書き換えられたりはしません。ファイルを書き換えられたくないけれど、元のリポジトリの変更点だけバックアップのような形で取得しておきたいという場合にはfetchのみをすればいいでしょう。変更を反映したくなって初めて、mergeすることになります。

pull requestを送る

pull requestを送れば、あなたがフォークしたリポジトリに加えた変更点をフォークする元のリポジトリに送ることができます。これによって元のリポジトリの開発に加わることができます。

リクエストを送るには、フォークしたリポジトリでリクエストを送りたいブランチに切り替え、画面上部のpull requestボタンを押します。
すると、どんなリクエストを送るのか(何を変更したのか)などを記入するボックスが出てくるので、そちらにメッセージを記入します。ここでのメッセージにはgithub markdownが使えます。
CommitsタブとFiles Changesタブで送るべきコミットを再度確認して下さい。

最後に、プルリクエストを送るボタンから、リクエストを送信できます。
元のリポジトリの管理者がリクエストを承認すれば、あなたの変更点が反映されます。
