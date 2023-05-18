# Arduinoの基本の書き方を学ぶ (section 1)

## section 1.1 Arduino のはじめの画面

```cpp
#include <arduino.h> //platformIO only

void setup(){

}

void loop(){

}
```
Arduino IDE や VSCode (以下両方含めて "IDE" とします)を開いて、Arduinoのプロジェクトを新規作成すると、このような表示になる。  

すでに二つの関数```setup()```と```loop()```がありますね。
この関数がArduinoの開発にとって、とっても重要なものになります。  
まずは左の```setup()```について、この関数はArduinoが起動or書きこみご一度だけ実行される関数です。主に１度だけ実行されればよいセットアップ関係に関係するコードを書きます。  
次にもう一つの```loop()```について、この関数は先ほどの```setup()```が実行された後、ずっと繰り返し実行される関数です。
この二つの関数に他の関数を書いていくことになります。

```#include <arduino.h>```が一番上にある人もいると思います。書かれてなかったら、これは書きましょう。  
Arduino IDE以外では、 Arduino用のファイルをインクルードする必要があるからです。

<details> <summary>おまけ：実際にsetupとloopを使用した例</summary><div>
  
```cpp
//簡単な Lチカのコード
void setup(){
  pinMode(11, OUTPUT); //ピンの初期設定
}
  
void loop(){
  digitalWrite(11, HIGH); //11番ピンから電流を流す
  delay(100);             //100ms待つ
  digitalWrite(11, LOW);  //11番ピンからの電流を止める
  delay(100);             //100ms待つ
}
```

```cpp
//校内ロボコンで使用したコード(改)
void setup(){
	//UART(シリアル)通信関係
	Serial.begin(115200); //PCで状況を見るためにポートを開けている

	//ステッピング関係
	l6470_setup();

	//LED1
	pinMode(LED1_PIN, OUTPUT);

	//電磁弁のピンの初期設定
	pinMode(VALVE_SIGN1, OUTPUT);
    digitalWrite(VALVE_SIGN1, LOW);

    //コントローラーの初期設定
    ps4_init();
}

void loop(){
    //コントローラーの受信関連の関数(ループで実行する)
	ps4_receive();
}
```
校内ロボコンの例からもわかるように、実際には、```setup()```や```loop()```にたくさんの処理を直接書くようなことはそんなにしません。
<br>
機能別に関数を作り、分けたほうが、読みやすく、修正しやすくなることが多いからです。
</div> 
</details>

## section 1.2 Lチカをもう一度やってみよう
### 用意するもの
* Arduino nano 
* ブレッドボード
* 抵抗(1kΩ)
* ジャンパ線
* LED

### 回路を組む
体験の時の復習になるが、ブレッドボードは短い辺の方が、電気的につながっています(図中の黒線方向)。  
<img src="https://user-images.githubusercontent.com/106954082/228745989-886c0635-d565-4d32-9e69-351bf8846512.png" width="50%">  
つまり、つなぎ方は部品同士のつなぎ方は次図のようになります。  
<img src="https://github.com/tutu-san/note_arduino/assets/106954082/2176bd40-e6f8-4354-ac46-2bc859106e36" width="50%">  

