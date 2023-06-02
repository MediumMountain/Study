# WindowsでWSL2を使って「完全なLinux」環境を作る

# WSL2とは
「WSL（Windows Subsystem for Linux）」とは、Windows上で動作するLinuxの実行環境
WSL1ではLinuxカーネルでなく、LXCoreというサブシステムがLinuxの実行環境を作っている
WSL2ではHyper-V上でLinuxカーネルが動作
WS1より少ないメモリでLinuxを起動できる

![WSL1とWSL2の仕組みのちがい](https://github.com/MediumMountain/Study/blob/new_branch/PICTURE/WSL1_WSL2.png)


WSL1ではWindows標準のファイルシステムであるNTFSを使うことから、Linuxファイルへのファイルアクセスが遅くなる。
一方のWSL2ではLinux標準のファイルシステム「EXT4」が採用され、Linuxファイルへのアクセスが高速化している。
逆にNTFSへの書き込みは遅い




## WSLの有効化

```
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```



## WSL2を規定のバージョンに設定
```
wsl --set-default-version 2
```


## Windowsとの連携による開発環境構築（VSCode）
- 拡張機能のからRemote WSLを選択してインストールする
- このときUbuntuが起動していたら一度終了させる（Ctrl + D）


## 連携動作確認
ubuntuを起動させログインします（しています）。
適当な作業ディレクトリを作成し（しなくてもいいです）、vscodeを起動させます。

ubuntu側での処理

```
mkdir test
cd test
code .
```


### WSLからWindowsファイルシステムへのアクセス
- /mnt/{ドライブ名}からアクセスできます。cドライブの場合は、/mnt/cです。

### windowsからWSLファイルシステムへのアクセス
- エクスプローラを開き、パスに\\wsl$を入力すると、WSLのディストリビューション毎のファイルシステムにアクセスできます。


### WSL2/UbuntuのIPアドレスを取得したい
- Ubuntu上でip aコマンドを実行
    - 実行結果のうち、eth0のinetが取得したいWSL2のIPアドレス

- hostnameコマンドを使う

- ホスト側からIPアドレスを取得したい
```
wsl -e hostname -I
```

https://qiita.com/neko_the_shadow/items/25b797cb436078b9e832
https://qiita.com/samunohito/items/019c1432161a950892be


### Windows11 の WSL2 ＋ WSLg で GUI アプリ実行時に発生するエラー「Error: Can’t open display: 0」の対処方法
https://snowsystem.net/other/windows/wsl2-wslg-error-display0/#
https://torisky.com/wsl%E3%81%A7%E3%82%A8%E3%83%A9%E3%83%BC%EF%BC%9Aerror-cant-open-display%E3%81%AE%E5%AF%BE%E5%87%A6/



# REFERENCE
[WindowsでWSL2を使って「完全なLinux」環境を作ろう！](https://www.kagoya.jp/howto/it-glossary/develop/wsl2_linux/)  
[WSL2とDockerとVisual Studio Codeでつくる開発環境](https://zenn.dev/canard0328/articles/wsl2-docker-vscode)



https://qiita.com/zaburo/items/27b5b819fae2bde97a3b#windows%E3%81%A8%E3%81%AE%E9%80%A3%E6%90%BA%E3%81%AB%E3%82%88%E3%82%8B%E9%96%8B%E7%99%BA%E7%92%B0%E5%A2%83%E6%A7%8B%E7%AF%89vscode

https://suzukalight.com/blog/posts/2021-01-14-cpp-vscode-wsl2
https://novnote.com/vscode-wsl-cpp-env/511/
https://novnote.com/wsl-cpp-env-build-task/551/

https://qiita.com/_masa_u/items/d3c1fa7898b0783bc3ed

https://ntk-ta01.hatenablog.com/entry/2020/09/09/181155
https://qiita.com/2019Shun/items/5ab290a4117a00e373b6#tasksjson%E3%81%AE%E8%A8%AD%E5%AE%9A
https://qiita.com/yoyomion/items/ed60a89009616f2efd55