# static

## ① static
- staticはC言語時代からある修飾子
- staticがつけられた変数は静的領域に確保されます。

## static 修飾子とは
- 「static」は静的という意味で「dynamic（動的）」の対義語である。
- 下記の様に変数宣言または関数宣言時に「static」を付加することで、付加された変数または関数が静的であることを宣言する。

```
    static int var;
    static int func() { return 0; }
```

## staticメンバ変数
次のPeapleクラスはstaticメンバ変数numを持ちます。  
また、コンストラクタが呼ばれた時にnumを+1し、デストラクタが呼ばれた時、numを-1しています。  

```
myClass.hpp
#include <stdio.h>
#include <iostream>
using namespace std;

class Peaple{
private:
    string str;
    static int num;
public:
    //コンスラクタ
    Peaple(const string& newName):str(newName) {num++;}
    //デストラクタ
    ~ Peaple(){num--;}
    //メンバ関数1
    void ret_Peaple_num(void);
};

```
メンバ関数の実装は次の通り。メンバ関数のret_Peaple_numはstaticメンバ変数 numの値を返すプログラムになっています。

```
myClass.cpp
int Peaple::num = 0; //Undefined symbols for architecture x86_64:
void Peaple::ret_Peaple_num(void){
    cout << num <<endl;
}
```

ここで、クラスを定義したhppファイルと対応するcppファイルにおいて、

int Peaple::num = 0;
として、staticメンバ変数の実体を作っておくことを忘れないようにしてください。もし、書き忘れたらUndefined symbols for architecture x86_64:(Clangでは)というエラーがでてコンパイルが通りません。(また、staticは不要なのでそこにも注意してください)

さて、前置きが長くなりましたが、staticメンバ変数の一番面白いところは、Peapleクラスの全てのインスタンスでその値を共有できるところです。 ??? 意味が分からないと思うので、実動作を見ながら説明していきます。

```
main.cpp
#include <iostream>
#include "myClass.hpp"

int main(int argc, const char * argv[]) {

    Peaple A("ペトロフ");
    Peaple B("ジダン");
    Peaple C("キアヌ");
    A.ret_Peaple_num();//3と表示される。

    Peaple *D = new Peaple("キャスカ");
    A.ret_Peaple_num();//4と表示される。
    delete(D);

    A.ret_Peaple_num();//3と表示される。

    return 0;
}
```
このmain関数を実行すると、

3
4
3
と表示されます。この数字はPeapleクラスのメンバ変数numの値を表しているはずです。numはコンストラクタが呼ばれた時、すなわち、Peapleクラスのインスタンスが生成された時に、+1されるのでしたね。このことを加味して実行結果を見るとnumの値は、Peapleクラスのインスタンスを3つ(A,B,C)を生成した後に3、インスタンスDを生成した後に4、さらにDをdeleteした後に3(デストラクタが呼ばれてnum--されている)と変化していることが分かると思います。すなわち、numは現在生成されているPeapleクラスの数を示しているのです。この結果からも、staticメンバ変数numがインスタンス毎に確保されているのではなく、インスタンス間で共有されていることが分かります。

staticメンバ変数の仕組み
staticメンバ変数は、何故インスタンス間で共有されているのでしょうか。それは、staticメンバ変数はインスタンス毎に確保されるのはなく、クラスにつき1つ静的領域に確保されるからです。 すなわち、各インスタンスのstaticメンバ変数は静的領域に確保されたも1つのものを指していることになります。

staticメンバ関数
次のコードを見てください。このコードは先のコードのメンバ関数ret_Peaple_num()を様々インスタンスから呼び出すように変更したものです。

main.cpp
#include <iostream>
#include "myClass.hpp"

int main(int argc, const char * argv[]) {

    Peaple A("ペトロフ");
    Peaple B("ジダン");
    Peaple C("キアヌ");
    A.ret_Peaple_num();//3と表示される。

    Peaple *D = new Peaple("キャスカ");
    D->ret_Peaple_num();//4と表示される。
    delete(D);//ここで、デストラクタがnum--

    B.ret_Peaple_num();//3と表示される。

    return 0;
}
ret_Peaple_numはstatic変数numを表示するものなので結果は変更前と同じになります。結果は同じなのに、呼び出し方が違う。。。これは非常に鬱陶しいですよね。
こんな時には、ret_Peaple_numをstaticメンバ変数にしていまいましょう。そのために先のコードを次のように変更します。まずは、Peapleクラス内のret_Peaple_numにstaticをつけます。

myClass.hpp
#include <stdio.h>
#include <iostream>
using namespace std;

class Peaple{
private:
    string str;
    static int num;
public:
    //コンスラクタ
    Peaple(const string& newName):str(newName) {num++;}
    //デストラクタ
    ~ Peaple(){num--;}
    //メンバ関数1
    static void ret_Peaple_num(void);//staticメンバ関数に
};

メンバ関数の実装は変更なしです。

myClass.cpp
int Peaple::num = 0; //Undefined symbols for architecture x86_64:
void Peaple::ret_Peaple_num(void){//変更なし
    cout << num <<endl;
}
このようにすると、ret_Peaple_numはstaticメンバ関数になります。staticメンバ関数を呼び出すには、次のようにPeaple::ret_Peaple_numとすれば呼び出せます。

main.cpp
#include <iostream>
#include "myClass.hpp"

int main(int argc, const char * argv[]) {
    Peaple A("ペトロフ");
    Peaple B("ジダン");
    Peaple C("キアヌ");

    Peaple::ret_Peaple_num();//3と表示される。

    Peaple *D = new Peaple("キャスカ");
    Peaple::ret_Peaple_num();//4と表示される。
    delete(D);

    Peaple::ret_Peaple_num();//3と表示される。

    return 0;
}
このように、メンバ関数ret_Peaple_num()をstaticにするとPeaple::ret_Peaple_num()という記述でret_Peaple_num()を統一的に呼び出すことができて非常に便利です。

ただし、staicメンバ関数はstaticメンバ変数以外のメンバ変数は操作できません。例えば、ret_Peaple_num()内でstaticでないメンバ変数strを使用しようとすると、Invalid use of member 'str' in static member functionというコンパイルエラーが出ます。

myClass.cpp
void Peaple::ret_Peaple_num(void){
    //Invalid use of member 'str' in static member function
    str = "ロナウジーニョ"; //staticでない、メンバ変数を変更する
    cout << str <<num <<endl;//staticでない、メンバ変数を使用する
}
staticメンバ関数を呼び出す時には、インスタンスのアドレスを渡さずに呼ぶ仕組みになっています。平たくいうと、インスタンスのアドレスがどこにあるかstaticメンバ関数は分からないわけです。なので、あるインスタンス固有のメンバ変数を変更しようにも、そのインスタンスのアドレスが分からない、インスタンスのアドレスが分からなければメンバ変数の値のアドレスも分からないのでエラーが出てくるわけです。

まとめ
staticにはメンバ関数を静的領域に確保し、インスタンス内で共有できるようにする効果があります。また、メンバ関数をstaticメンバ関数にすることで、そのメンバ関数はstaticメンバ変数以外を取扱えなくなります。少し不便な気もしますが、逆に言えばstaticメンバ変数以外のメンバ変数を取り扱わないという関数の挙動を事前に読み手に伝えることができるのでコードの可読性の向上に繋がり効果もあるのかなと思いました。

インスタンス内で共有したい値があるならグローバル変数でいいじゃんと思う方もいらっしゃると思います(私も最初はそう思いました)。ですが、staticメンバ変数はグローバル変数とは違い、プログラム全体で共有はなく、インスタンス間でのみという共有される範囲が明確であるとうメリットがあると私は思います。

個人的な見解ですが、グローバル変数を使ったプログラムはどこでその変数が操作されているか特定することが困難です。もし、自分があるクラスのインスタンス間でのみ共有するつもりでグローバル変数を使用したつもりでも、他のプログラマがそのグローバル変数を書き換えてしまいプログラムの挙動がおかしくなる・・・なんてことも考えらえます 。そんな時に、staticメンバ変数を使えば、このような事故も防げます。

このように、staticメンバ変数はインスタンス間という特定の範囲のメンバ変数を共有できるので、生成されたインスタンスの数を管理する時とかには非常に便利です。ですが、staricメンバ関数はどのような時に使うのか、少し疑問でもあるのでもう少し勉強してみようと思います。


# REFERENCE
C++ 修飾子についての忘備録  
https://qiita.com/omuRice/items/3c40e8dde19e276ccacf  


http://vivi.dyndns.org/tech/cpp/static.html


基底クラスのstaticメンバ変数を継承先のクラスで書き換えると、別クラスのインスタンスにも影響する
https://qiita.com/y-ken/items/fea3b95ffa005c0ce3cd