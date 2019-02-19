# マスタ
https://valeur.backlog.jp/wiki/VALEUR/VagrantAnsibleLaravel%E9%96%8B%E7%99%BA%E7%92%B0%E5%A2%83%E3%81%B2%E3%81%AA%E5%BD%A2

--- 以下20190219コピー ---

*Vagrant/ansible/Laravel 開発環境

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

