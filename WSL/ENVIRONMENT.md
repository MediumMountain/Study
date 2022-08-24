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


# REFERENCE
[WindowsでWSL2を使って「完全なLinux」環境を作ろう！](https://www.kagoya.jp/howto/it-glossary/develop/wsl2_linux/)
[WSL2とDockerとVisual Studio Codeでつくる開発環境](https://zenn.dev/canard0328/articles/wsl2-docker-vscode)