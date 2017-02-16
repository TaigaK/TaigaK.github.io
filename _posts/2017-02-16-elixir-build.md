---
layout: post
title:  "Elixir buildまとめ"
date:   2017-02-16 21:00:00 +0900
---

# Elixirビルド手順
ちょくちょく忘れるのでメモ。  
rbenvみたいな感じで切り替えられるように。  
ubuntuを想定

# evm経由でErlangインストール

	#必要なもの先に入れとく
		apt install build-essential libncurses5-dev openssl libssl-dev
		apt install wget git

	#clone&install
		cd ~
		git clone https://github.com/robisonsantos/evm.git
		cd evm
		./install

	#PATH通す
		echo 'source /root/.evm/scripts/evm' >> ~/.bashrc　　　#'~'の部分は./installした時の出力の最後に書いてあるのでコピペ
		source ~/.bashrc

	#erlangインストール
		evm install OTP_18.0

	#使うやつに設定＆常用に設定
		evm use 18.0 default

	#erl起動確認
		erl

#####参考ページ
	Linuxでkerlを使用して複数バーションのErlang/OTPを導入する
		http://qiita.com/tatsuya6502/items/f15da8ea6e793c5038a2
	Elixir/Phoenixを実行してみる
		http://qiita.com/yokaigundan/items/0e8da4938bd91fab400b

# kiex経由でelixirインストール
こちらもubuntu想定

	#取ってくる
		\curl -sSL https://raw.githubusercontent.com/taylor/kiex/master/install | bash -s

	#PATH通す
		echo 'test -s "$HOME/.kiex/scripts/kiex" && source "$HOME/.kiex/scripts/kiex"' >> ~/.bashrc

	#インストール
		kiex install 1.2.2

	#使うやつに設定＆常用に設定
		kiex use 1.2.2 default

	#iex起動確認
		iex

#####参考ページ
	Elixir/Phoenixを実行してみる
		http://qiita.com/yokaigundan/items/0e8da4938bd91fab400b
