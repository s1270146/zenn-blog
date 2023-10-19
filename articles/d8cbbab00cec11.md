---
title: "【Kali-Linux】Kali LinuxをVirtualBoxで使うための環境構築"
emoji: "🎉"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["kalilinux", "Ubuntu", "VirtualBox"]
published: true
published_at: 2023-10-19 21:45
---

## 前提

- VirtualBoxはインストール済み(7.0.8)
- OSはUbuntu23.04
- この記事はVirtualBoxでkali-linuxが使えるようになるまでのメモである

## イメージをダウンロード

kali-linuxのVirtualBox用のイメージをダウンロードする

https://www.kali.org/get-kali/

```sh
wget https://ftp.riken.jp/Linux/kali-images/kali-2023.3/kali-linux-2023.3-virtualbox-amd64.7z
```

拡張子7zのファイルを解凍するために``p7zip-full``をインストール

```sh
sudo apt install p7zip-full
```

オプションxを使ってファイルを解凍

```sh
7z x kali-linux-2023.3-virtualbox-amd64.7z
```

フォルダ構成の確認

```sh
$ tree kali-linux-2023.3-virtualbox-amd64

kali-linux-2023.3-virtualbox-amd64
├── kali-linux-2023.3-virtualbox-amd64.vbox
└── kali-linux-2023.3-virtualbox-amd64.vdi
```

## VirtualBoxでkali-linuxを使う

拡張子vboxのファイルを使ってVirtualBoxにインストールしていく

下の画像の追加(A)をクリック

ファイルを選択できるのでさっきダウンロードした``kali-linux-2023.3-virtualbox-amd64.vbox``を選択

![](/images/d8cbbab00cec11/virtualbox1.png)

そうすると以下の画像のようになる

![](/images/d8cbbab00cec11/virtualbox2.png)

メインメモリを増量したいので

設定(S)でメインメモリを2048MBから4096MBに変更

## kali-linux起動

いざ起動しようとおもったらエラーがでた

以下のコマンドを実行するように言われた

```sh
sudo /sbin/vboxconfig
```

でも実行してみたら

```sh
vboxdrv.sh: Stopping VirtualBox services.
vboxdrv.sh: Starting VirtualBox services.
vboxdrv.sh: Building VirtualBox kernel modules.
vboxdrv.sh: failed: modprobe vboxdrv failed. Please use 'dmesg' to find out why.

There were problems setting up VirtualBox.  To re-start the set-up process, run
  /sbin/vboxconfig
as root.  If your system is using EFI Secure Boot you may need to sign the
kernel modules (vboxdrv, vboxnetflt, vboxnetadp, vboxpci) before you can load
them. Please see your Linux system's documentation for more information.
```

上記のようなエラーが出た

セキュアブートを有効にしていると署名がどうたらみたいな

なので、無効にしてもう一度実行

うまくいったのでvirtualboxでkali-linuxを起動

![](/images/d8cbbab00cec11/kalilinuxlogin.png)

usernameとpasswordはともに``kali``

ログインするとこのような感じ

![](/images/d8cbbab00cec11/kaliindex.png)

## さいごに

CTFを解くための環境を作りたくてこのようなことを行いました。

初心者ですがCTFの問題もっと解けるようにがんばります。