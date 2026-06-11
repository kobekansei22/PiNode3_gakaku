# PiNode3
PiNode3は温室ハウス内で動作するデータ収集システムです．

# 変更内容
- requirements.txtに必要ライブラリを追加
- usb.pyがモータドライバを認識するように変更
- 毎日正午に画角調整を起動するnoon_monitor.timer,noon_monitor.serviceをserviceフォルダに追加
- camera.pyにロック機能を追加(手動と自動が被らないようにするため)
- srcフォルダにcamera_fast.py,send.py,mortor_test.py,watch.py,yolo_main.py,best_melon.ptを追加

### usb.py
変更前：spresenseかそれ以外かを判別　→　変更後：spresense,usbカメラ,モータドライバ,それ以外を判別

### 画角調整サービスファイル
install.shにてサービス登録
頻度，時刻などを変更する場合は適時変更

### camera.py, camera_fast.py
usb.pyの変更に伴い一部変更
手動操作の追加に伴い，自動撮影との競合を避けるためロック機能を追加
camera_fast.pyはspresenseでの撮影の際に低解像度画像取得の際使用(それ以外はcamera.pyと同じ)

### send.py
異常検知時(距離が近い，検出対象が無い場合)にteamsに通知を行う機能．現在は大和コン関係者をメンションするため適時変更

### mortor_test.py
サーボモータのモード切替，角度送信，角度読み取り等の関数を格納している．
mainとして呼び出すことで手動操作を行うインターフェースとなる．(現在はコマンドプロンプトで操作)

### watch.py
特定のフォルダを監視して画像が取得された際に画角調整を起動するシステムのmainとなるコード

### yolo_main.py
watch.pyが画像を検知した際呼び出す．
新規画像に対してyoloによる物体検出を行った後，モータ制御，ユーザ通知などを行う

### best_melon.pt
メロン画像1000枚を用いて学習したファイル
"\\minelab-dataset\minelab-dataset\20260220_画角調整メロン_アノテーションデータ_甲部"にデータセット格納