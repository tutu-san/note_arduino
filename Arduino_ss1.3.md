# Arduinoの基本の書き方を学ぶ (section 1) -つづき-

## section 1.3 デジタル入力を試してみよう
目的　：　Arduinoのデジタル入力の方法を関数を学ぶ
### 用意するもの
* section 1.2 で用意したもの 
* タクトスイッチ
* 抵抗(10kΩ)

### 回路を作る
<img src="https://github.com/tutu-san/note_arduino/assets/106954082/04597539-b298-4299-a0ee-7a5afa49a335" width="70%">

上記の回路図を見て、ブレッドボードに回路を作ってみましょう。
LED周りは、前回と同じままでいいです。  
タクトスイッチのつなぎ方に注意して、ボタン周りも作ってください。  
今回は、GNDの書き方が前回と違いますが、 Arduino nano にある２箇所のGNDピンのどちらかにつなげばOKです。  
(白色になっているはずです。 書いてあるので確かめて見てください。)  

### プログラムを書く
回路ができたら、プログラムを組んでみましょう。
#### 新しいもの
今回は、初めての関数が１つと、新しいオプションが１つあります。  
1. digitalRead 関数
```cpp
digitalRead(uint8_t pin)
```
```digitalRead```関数は、ピンの入力状態をチェックして戻り値を返す関数です。
入力があると```HIGH```、ないと```LOW```を返します。  
(HIGH/LOWは、 #define で 1/0 という風に定義されているだけなので、 0とか、1とかが戻ってきているとも言えます。)  

#### 問題 2
ボタンを押したら、LEDが点灯して、ボタンから手を放したらLEDが消灯するプログラムを書いてください。  
(出力ピン 5,入力ピン 2)

ヒント1 : pinMode()のオプションは、OUTPUT と INPUT の二種類あります。  
ヒント2 : digitalRead() の戻り値は、0 と 1 として考えるといいかもしれません。

<details> <summary>答え</summary><div>
  
```cpp
#include <Arduino.h>

void setup(){
	pinMode(5, OUTPUT);
    pinMode(2, INPUT);
}

void loop(){
	if(digitalWrite(2)){
        digitalWrite(5, HIGH);
    }else{
        digitalWrite(5, LOW);
    }   
}
/*
loopの中身は、この通りじゃなくてもいいです。
このコードと同じような動作をすればどれも正解とします。
*/
```
</div> 
</details>
