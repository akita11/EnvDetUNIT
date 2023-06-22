# Envelope Detector (包絡線検波UNIT)

アナログ信号波形の包絡線（波形の外側の波形）を生成します。マイクなどからの音声信号の振幅を計測する場合などに便利です。Grove端子または3ピン端子で、マイク等の信号源とM5Stack等のマイコンとの間に接続して使用します。（スイッチサイエンスで委託販売予定）

<img src="https://github.com/akita11/EnvDetUNIT/blob/main/EnvDet1.jpg" width="240px">

表面

<img src="https://github.com/akita11/EnvDetUNIT/blob/main/EnvDet2.jpg" width="240px">

裏面

左側（CN1・J1、矢印の根本側）から信号源（マイクアンプの出力）を接続し、右側（CN2・J2、矢印の先端側）に包絡線波形が出力されるので、マイコン等に接続します。

## ピン配置

電源はCN1/J1/CN2/J2のいずれからのVDDへ+3.3V〜+5Vを与える。

### 入力側

- CN1(Groveコネクタ): アナログ入力1/アナログ入力2/VDD/GND （信号入力は標準で「アナログ入力1」で、JP1で「アナログ入力2」に切り替え可能
- J1（2.54mmピンヘッダ3ピン）: VDD/GND/アナログ入力

### 出力側

- CN2(Groveコネクタ): アナログ出力1/アナログ出力2/VDD/GND （信号出力は標準で「アナログ出力1」で、JP2で「アナログ出力2」に切り替え可能
- J2（2.54mmピンヘッダ3ピン）: VDD/GND/アナログ出力


## 包絡線検波とは？

<img src="https://github.com/akita11/EnvDetUNIT/blob/main/wave1.png" width="240px">

音声信号などの変化が速い信号をマイコン等のA/D変換で取得する場合、A/D変換のタイミングと信号波形の変化のタイミングがあわないと、A/D変換値が波形の山の部分や谷の部分をバラバラに拾ってしまい（図中の◯）、正しく振幅を取得できません。


<img src="https://github.com/akita11/EnvDetUNIT/blob/main/EnvDet_wave.png" width="240px">

信号波形を包絡線検波回路に与えると、信号波形の外側をつないだ「包絡線」をつくることができます。（包絡線検波回路は、ダイオードを用いる半波整流回路にコンデンサの平滑回路を組み合わせたもの。厳密にはコンデンサの容量によって包絡線の波形が少し変わる。なおこのUNITでは、特に小さい振幅の信号も正しく扱えるようにオペアンプを使った理想ダイオードを使っています）

<img src="https://github.com/akita11/EnvDetUNIT/blob/main/wave2.png" width="240px">

このようにして得られた包絡線波形に対してA/D変換を行えば、（ほぼ）正しく信号波形の振幅を取得することができます。

<img src="https://github.com/akita11/EnvDetUNIT/blob/main/measured_wave1.jpg">

実際のマイク（M5StackマイクUNIT）の波形（黄色）と、このUNITの出力（水色）。

※なおこの回路の出力インピーダンスは高めなので、抵抗などの低インピーダンスの負荷を駆動すると波形が歪むことがあります。必要に応じて出力側にバッファ（ボルテージフォロア等）を使用してください。

## （オプション）時定数の調整

包絡線検波の回路の特性上、入力する信号波形の周波数によっては正しく包絡線を得られない場合があります。標準設定では1kHz前後の音声帯域の信号では、ほぼ正しい包絡線を得られますが、必要であれば回路の特性（時定数）を変更することができます。JP3をカットし、J3（2.54mmピンヘッダ2ピン）に適当な容量のコンデンサを接続します。標準では10uF（時定数は約160Hz）で、これより大きな容量のコンデンサを接続すると、包絡線の変化がより緩やかになります。

<img src="https://github.com/akita11/EnvDetUNIT/blob/main/measured_wave2.jpg">

Aoutに100uFのコンデンサを接続したときの、マイクの波形（黄色）と、このUNITの出力（水色）。


## Author

Junichi Akita (akita@ifdl.jp, @akita11)
