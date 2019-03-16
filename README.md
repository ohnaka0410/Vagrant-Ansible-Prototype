# Vagrant で作る仮想環境

## 技術要素 ##
- Vagrant - 仮想マシンの作成・起動・停止などを簡単に行うためのツール
- VirtualBox - 仮想化ソフトウェア
- Ansible - エージェントレスな構成管理ツール


## ディレクトリ構成 ##

```
[プロジェクトのルートディレクトリ]
  ├─ README.md
  ├─ Vagrantfile
  └─ ansible/
      ├─ group_vars/
      │   └─ all.yml
      ├─ host_vars/
      │   └─ all.yml
      └─ roles/
         ├─ common/
         ├  ・・・
         └─ httpd/
```

### Vagrantfile ###
vmの設定などを記述する

```
# vmのベースになるVagrantのbox
config.vm.box = "bento/centos-6"

# ポートフォワーディングの設定
config.vm.network "forwarded_port", guest: 80, host: 1080
config.vm.network "forwarded_port", guest: 443, host: 1443

# vmとの共有ディレクトリの設定
# 編集するプログラム資産などを指定する
config.vm.synced_folder "../data", "/vagrant_data"
config.vm.synced_folder "../data", "/vagrant_data", :mount_options => ['dmode=777', 'fmode=666']
```

### ansible
VagrantのProvisionで実行されるAnsibleのソース配置ディレクトリ

### shell/ ###
VagrantのProvisionで実行するshell script格納ディレクトリ

## インストール ##
- VirtualBoxのインストール [https://www.virtualbox.org/](https://www.virtualbox.org/ "https://www.virtualbox.org/")
- Vagrantのインストール [https://www.vagrantup.com/](https://www.vagrantup.com/ "https://www.vagrantup.com/")

## よく使うコマンド ##

### Vagrant ###

```
# ローカルにキャッシュされているVagrantのbox(vmのテンプレート)
$ vagrant box list

# Vagrantのbox(vmのテンプレート)をローカルにキャッシュ
$ vagrant box add bento/centos-6

# vmの起動
$ vagrant up

# vmへのsshログインまたはログイン情報の表示
$ vagrant ssh

# vmの初期構築の再実行
$ vagrant provision

# vmの再起動
$ vagrant reload

# vmの停止
$ vagrant halt

# vmの削除
$ vagrant destroy
```
