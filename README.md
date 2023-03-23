# study-flutter-android_tv

flutter でAndroid tv アプリを作るための事前調査リポジトリ



## 初期構築
brew の方法と、公式サイトからinstallとあるが、  
昔構築した名残で、  

https://github.com/flutter/flutter

`/Users/ao/development/flutter`
にcloneしてして、中のflutterに
`/Users/ao/development/flutter/bin/flutter`
にpathを通して使っている。

git のbranchまたはtagをcheckoutでバージョンを切り替えられる。

### flutter doctor

`flutter doctor`
実行で環境が整っているか確認が出来る。
エラーがなくなるまで調整をする。

![](https://i.imgur.com/VCG7578.png)

#### Android Sdk managerがない場合
`flutter doctor --android-licenses`
でエラーになる。
![](https://i.imgur.com/fcEbzKz.png)
Android Studioを開いて「Preferences > SDK Manager > SDK Tools」にある「Android SDK Command-line Tools(latest)」にチェックを入れて右下の「OK」をクリック


#### android-licenses
`flutter doctor --android-licenses`
を再度実行する

![](https://i.imgur.com/lVbadVC.png)


#### もう一度 flutter doctor

![](https://i.imgur.com/7JQQwml.png)

repositoryはchannelに依存しているみたい。

#### flutter channel

flutter channel の確認とstableに変更
![](https://i.imgur.com/uabL443.png)

gitも自動的に切り替わった。
(flutter のバージョン指定したいときはどうするんだろう？)

##### [おまけ]3.7.8のままやってみる
chanel切り替えの際にでていた、
`flutter upgrade`
を実行すれば残っている
> ✗ Downloaded executables cannot execute on host.

のエラーがきえるか。

![](https://i.imgur.com/Tqngck7.png)
だめだった。。。。

version どうやって切り替えるんだ。。。ｗ

#### flutter upgrade
![](https://i.imgur.com/pxt8CLq.png)

#### もう一度 flutter doctor
![](https://i.imgur.com/HF9dWjU.png)
> ✗ Downloaded executables cannot execute on host.

これがまだ残る。

記載されているissueにとぶ。
https://github.com/flutter/flutter/issues/6207
![](https://i.imgur.com/cNiffCw.png)

`sudo apt-get install lib32stdc++6`
を実行

not found command apt-get エラー！

実行して気づく。
これUbuntuの話だー！w

#### macの場合のDownloaded executables cannot execute on host.

https://github.com/flutter/flutter/issues/95220
issueみっけ


![](https://i.imgur.com/hD5yoMM.png)
キャッシュ削除かな？

![](https://i.imgur.com/vzwSO63.png)


#### もう一度 flutter doctor

![](https://i.imgur.com/Hfi1EFx.png)
キャッシュ消したのでbuildとDownloadが走る。

![](https://i.imgur.com/ydeirSG.png)


OKKKKKKK！！！！


##### [おまけ]やっぱり3.7.8のままやってみる
結局キャッシュの問題だっただけで、flutter upgradeたたけなくても良いなら、いけるのでは？

`git checkout 3.7.8`

一応もう一度キャッシュ削除
`cd bin`
`rm -rf cache`

多分エラーにはなるだろうけど一応
`flutter upgrade`

![](https://i.imgur.com/pF8MJ9p.png)
案の定。

`flutter doctor`
![](https://i.imgur.com/0bv3oFF.png)
いけた！！！(警告はchannelの話なのでしかたない)
CocoaPodも一旦は無視。

flutter upgrade が出来ていないとバージョンが実は更新されていないとかありそうなので、
本当に問題ないかは知らない。



### プロジェクト作成
