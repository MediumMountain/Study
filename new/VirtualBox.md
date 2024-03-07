# VirtualBox

## 
## 
## 
## 

## VirtualBoxでのUSBデバイス認識

### Extension Packをいれとけ！
https://www.virtualbox.org/wiki/Downloads

### vboxusersグループに追加しておけ！(linux)
- USB機器の一覧がでないときは、virtualboxを起動するユーザがvboxusersグループに所属していないとダメ

```
$ sudo gpasswd -a YOUR_USERNAME vboxusers
```

で追加

### USBデバイスフィルターに追加しておけ！
- ゲストOSをシャットダウンし、ゲストOSの設定からデバイスフィルターを調整



### Ubuntuでの認識
Ubuntuには、デフォルトでFTDIシリアルポートドライバがインストールされているため、UM232Hが接続されると、仮想シリアルポートへアクセスするためのデバイスファイルが出現します。

```
oversea@Ubuntu64:~$ ls -l /dev/*USB*
crw-rw---- 1 root dialout 188, 0 12月 21 11:11 /dev/ttyUSB0
```
/dev/ttyUSB0はキャラクタ型デバイスファイルであり、グループオーナーはdialout(発信)となっています。

### ホスト環境からの切断
UM232HがUbuntu上で認識されると同時に、ホスト環境では切断されます。
```
MacBookPro:~ $ ls /dev/*serial*
ls: /dev/*serial*: No such file or directory
MacBookPro:~ $ kextstat |grep FTDI
MacBookPro:~ $
```
/devディレクトリのデバイスファイルエントリは消失し、FTDIシリアルポート対応拡張モジュールもアンロードされています。この時点で、ホスト上のD2XXライブラリを使用したプログラムはFTDIデバイスを認識できなくなりますので、注意してください。

VirtualBoxステータスラインのUSBアイコン上で切断を行うと、再びホスト環境に拡張モジュールがロードされ、デバイスファイルも復帰します(Ubuntu上のデバイスファイルは消失)




## REFERENCE

VirtualBoxでのUSBデバイス認識  
https://qiita.com/civic/items/684c4b82428feb0c4ae1

VirtualBox UbuntuへのホストUSBデバイスの接続  
http://www.oversea-pub.com/free/environment/2073.html  