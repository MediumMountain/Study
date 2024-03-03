# termios 
- ターミナルI/O用の Unix API
- サポートされる主な機能は次のとおり

    - シリアルポートの開閉
    - 通信のパラメータの設定
    - シリアル通信による読み書き


## 使用方法
- C/C++ の場合，
```
#include <termios.h>  
```
 とすれば使用可能になります．
- なお，termios 構造体の定義はtermios.hではなく termbits.hに記述されていることに注意が必要です．



## 構造体
- termios 構造体の中身は次の通りです．

```
typedef unsigned char   cc_t;
typedef unsigned int    tcflag_t;
#define NCCS 19
```

```
struct termios {
    tcflag_t c_iflag;       /* input mode flags */
    tcflag_t c_oflag;       /* output mode flags */
    tcflag_t c_cflag;       /* control mode flags */
    tcflag_t c_lflag;       /* local mode flags */
    cc_t c_line;            /* line discipline */
    cc_t c_cc[NCCS];        /* control characters */
};

```