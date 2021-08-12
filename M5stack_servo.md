M5 Stackでサーボモータを動かす

# はじめに

M5 Stack は，esp32マイコンを搭載し，高い処理能力と豊富な拡張性を有する便利なマイコンキットです．
今回は，拡張モジュールの一種であるServo2モジュールを使用して，サーボモータを複数制御する方法を調べてみます．

# 準備するもの

* M5 Stack
* Servo2モジュール
* バッテリー(今回はKONDO製，6.6 VのLiFeバッテリーを使用)


# M5 Stackの準備

M5 Stackは様々な方法でプログラムを作れますが，今回はArduino IDEを使用することにします．
(参考) https://docs.m5stack.com/

1. Arduino IDEをインストールしましょう．
2. Arduino IDEを起動し，「ファイル」から「環境設定」を開き，「追加のボードマネージャのURL」に" https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json "を追記します．
3. 「ツール」から「ボードマネージャ」を開きます．
4. 「eps32」を検索し，「eps32 by Espressif Systems」をインストール
2. 「ツール」から「ライブラリを管理」を選択して「ライブラリマネージャ」を呼び出します．
4. 「M5stack」を検索し，「M5stack by M5stack」をインストール
5. M5 StackをPCに接続し，「ツール」から「ボード」を展開し，"M5Stack-core-ESP32"を選択します．

次に，COMMUモジュールでCAN通信ができるように`mpc_can`ライブラリを追加します．