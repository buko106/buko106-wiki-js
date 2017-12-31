<!-- TITLE: VPSのセットアップ -->
<!-- SUBTITLE:  -->

# VPSのセットアップ
## VPSの契約
* [ConoHa](https://www.conoha.jp/)の1GBプランを借りています。
* プリペイドなので払いすぎる心配なし。

## VPSの初期設定
* Ubuntu 16.04 をインストール
* アカウント周りの設定
	* 作業用ユーザの作成
		* 公開鍵アップロード
		* sudoグループに登録
	* rootでのログインを禁止
* aptでnginxを導入
* nを用いたnodeのバージョン管理を導入
[UbuntuにNode.jsをインストールするベストプラクティス](http://kamatte.me/2017/08/17/ubuntu%E3%81%ABnode-js%E3%82%92%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB%E3%81%99%E3%82%8B%E3%83%99%E3%82%B9%E3%83%88%E3%83%97%E3%83%A9%E3%82%AF%E3%83%86%E3%82%A3%E3%82%B9/)

## ドメインの取得
* お名前.com
* [ここ](https://qiita.com/sugra511/items/3b05423d4adeeec5cdd4)を参考にネームサーバを変更
	* サブドメインの追加も忘れずに
	* 上の変更をしておけば、あとはVPS側での設定になる

## WIki.jsを用いたWikiの公開
* 公式に従うのみ https://docs.requarks.io/wiki#installation
* SSHを使うのにhttpsのアドレスを書くありがちなミスを再発した(placeholderがhttpsだったのが悪い...)
* リバースプロキシの設定が悪いと色々と動かない
	* バージョン1.xではサブディレクトリではWiki.jsが動かないのでサブドメインを使わないといけない
	* 普通にドキュメントに書いてあった https://docs.requarks.io/wiki/admin-guide/setup-nginx

## ポートの設定
* ConoHaのコンソールで全てのポートを開放(これをしないとVPSに届く前にブロックされる)
* sshのポートの変更
	* /etc/ssh/sshd_configのPortをxyzに書き換え
	* `sudo service ssh restart`
	* `ssh`するときは`-p xyz`
		* `scp`するときは`-P xyz`
* ufwを設定

```powershell
sudo ufw allow xyz
sudo ufw allow 80
sudo ufw allow 443
sudo ufw enable
```
などなど

## TODO
* ~~ポート開放の自前化(Ubuntuなのでufwを使う?)~~
* SSLの導入(Let's Encrypt)
* Wiki.jsサーバの自動起動・永続化