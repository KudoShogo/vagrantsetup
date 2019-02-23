* Laravel Project を取り出して新プロジェクトを作る方法

{code}
(1)ひな形プロジェクト(va_laravel_vagrant)をcloneできるようにする。
   https://github.com/valeurgit/va_laravel_vagrant
   開発メンバーに参加

(2)空の新プロジェクトを作成してcloneする
   ここでは仮に project_new と名付ける
   https://github.com/valeurgit/project_new 

(3)新プロジェクトを clone してリポジトリに入る
%> git clone https://github.com/valeurgit/project_new 
%> cd project_new 

(4)ひな形プロジェクトを新リポジトリに pull して自分のマスタとして push する。
%> git remote add valeurgit https://github.com/valeurgit/va_laravel_vagrant.git
%> git pull valeurgit master  --allow-unrelated-histories
%> git push origin master
{/code}

* Laravel のインストール
{code}
%> vagrant ssh
もしくはターミナルから host:192.168.30.50 user: vagrant pass: vagrant　でログイン
%> cd /var/www
%> composer create-project --prefer-dist laravel/laravel html
インストールの最後に下記のように聞かれるので Y
Do you want to remove the existing VCS (.git, .svn..) history? [Y,n]? Y
確認してみてください。
http://192.168.30.50/
{/code}

* Laravel 開発サポート情報
** Windowsの場合
*** シンボリックリンク
{code}
.env ファイルを .env.local でハンドコピーしたくない場合
初期の .env を削除して
%> ln -s .env.local .env
のようにシンボリックリンクで対応したいところですが、ファイルを置いているのがWindowsだとエラーになります。
そこで、”管理者”でコマンドプロンプト(cmd)を呼び出します。管理者権限です！
で、laravel のカレントに移動し
ex)
#> cd /D D:\vm\target_vagrant_project\pj\laravel
#> mklink /D .env .env.local
とすることで、Windowsのシンボリックリンクを作成できます。
{/code}

*Vagrant/ansible/Laravel 開発環境の説明

本モジュールは Vagrant/ansible/Laravel+phpMyAdmin を使った開発環境のひな形です。
- Vagrant : Centos7.3
- ansible : MySQL5.7 + nginx + PHP7.2

**環境を構築するマシン
下記のソフトウェアをインストールする
- VirtualBox
- vagrant
- git(open-ssh)

***参考
https://qiita.com/SatoshiGachiFujimoto/items/4955d41d8015fd06352a
http://www.curict.com/software/Windows10/Windows10_git.html


 
**新しいLaravel Project

新しいLaravel Projectがあれば、下記のように変更してご利用ください。

***自分自身の名称
- Vagrantfile
1個所
	vbox.name = "valeur-laravel"

***IPアドレス変更方法
このパッケージを複数UPする場合は下記を変更してご利用ください。

- Vagrantfile
1個所
	webdb.vm.network "private_network", ip: "192.168.30.50"

- ansible\hosts-Valeur
1個所
	192.168.30.50

- ansible\site-Valeur.retry
1個所
	192.168.30.50

- ansible\roles\nginx\templates\etc\nginx\nginx-webdb.conf
1個所
	server_name 192.168.30.50;



** とりあえず使いたい人

***前提条件
1.開発環境に必要ソフトウェアのインストール済み
2.Vagrant/ansible モジュールの設定変更済み

***起動
- vagrant up

***確認
phpMyAdminは、hosts を書き換え(192.168.30.50 pppp.vm.com を追加)アクセスすることでご利用いただけます。
- http://pppp.vm.com
- http://192.168.30.50

***削除
- vagrant destroy webdb


***サーバアクセス
- SSH
> vargant ssh webdb
うまくあがっていれば外部から入れます。（pass:vagrant）
> ssh vagrant@192.168.30.50


*備考
OS
- user: vagrant
- pass: vagrant  
(root切り替えは、`sudo su -`)

mysql
- user: valeur
- pass: valeur
- db: valeur

