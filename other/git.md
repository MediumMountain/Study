# Git①　導入編

## git for VScode

### 準備
- Gitをインストールする
- VScodeを
- GitHubにアカウントを作っておく

### 基本設定
```
git config --global user.name {自分の名前}
git config --global user.email {メールアドレス}
```

### 初期化
1. フォルダを開く  
1. 適当なフォルダを作成
1. ターミナルで以下を実行
```
git init
```

※以下が出れば完了  
Initialized empty Git repository in I:/git-sample/.git/

### GitHub
1. リモートリポジトリを作成する  
Newを押下
    ![](https://miya-system-works.com/resource/media/1625/1625_w1280.jpg)　　

    色々選択
    ![](https://miya-system-works.com/resource/media/1627/1627_w1280.jpg)　　
1. ローカルリポジトリをリモートリポジトリに紐づける
    ```
    git remote add origin https://github.com/{ユーザー名}/{リポジトリ名}.git
    ```

    確認
    ```
    git remote -v
    ```
    こんな感じのが出ればOK
    ```
    origin  https://github.com/{ユーザー名}/{リポジトリ名}.git (fetch)  
    origin  https://github.com/{ユーザー名}/{リポジトリ名}.git (push) 
    ```

1. ローカルリポジトリからリモートリポジトリにプッシュする  
    1. ローカルの変更をステージング  
        ```
        git add (オプション)
        ```
    1. ローカルコミット
        ```
        git commit -a 
        または
        git commit (ファイル名)
        ```
    1. リモートへプッシュ  
    プッシュコマンドでできること
        1. ローカルブランチ「master」を、リモートブランチ「master」に push 
            ```
            git push origin master:master
            ```
        1. リモートブランチの削除  
            originの（ブランチ名）ブランチを削除
            ```
            git push origin --delete (ブランチ名)
            ```
        
            : コロンを使えばリモートブランチを削除できる  
            ※ 左を右にプッシュする。空をプッシュすれば削除になる、そんな感じ
            ```
            git push origin :tmp
            ```
            
        1. リモートブランチを上書き  
            強制プッシュを行うことで上書きを行う
            ```
            git push -f origin master
            ```

        1. 上流ブランチ（リモートブランチ）の指定
            ```
            git push -u origin (ブランチ名)
            ```
            設定ができれば次回からブランチ名の省略ができる。


### コマンドメモ
git log  
git branch  
git checkout  
git reset  
git reset --hard  
git rebase  



# trable shouting

## プッシュ時のエラー  
1. 
    ```
    Git: remote: Permission to ~/AA.git denied to AAA 
    ```

    - プッシュ先のリポジトリに対する権限がない、違っている  
    資格マネージャーからgit のアカウントを編集する

        ![](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.amazonaws.com%2F0%2F245438%2Ff9cd18db-75d2-b1d3-cc61-74ce6421818a.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&w=1400&fit=max&s=fb619ea2e1faaf9eda4e31240a1ab78e)

1. 
    ```
    Git: remote: Permission to ~/~~.git denied to XXXX 
    ```

- XXXXの部分がremoteに設定しているものと違う。


- リモートのリポジトリを削除する
    - 削除したいリポジトリ内でsettingを選択  
    下部の方にDanger Zoneがあるのでその中のDelete this repositoryをクリック  
    提示に従いリポジトリ名を入力

        ![](https://qiita-user-contents.imgix.net/https%3A%2F%2Fqiita-image-store.s3.ap-northeast-1.amazonaws.com%2F0%2F559347%2F971597f1-41d6-4953-e7f6-2642532998a3.png?ixlib=rb-4.0.0&auto=format&gif-q=60&q=75&w=1400&fit=max&s=e3d23b4001f7944743fc5108762d8f68)


## git pull 時に以下のエラー
remote: Support for password authentication was removed on August 13, 2021. Please use a personal access token instead.
remote: Please see https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/ for more information.
fatal: unable to access 'https://github.com/Naya1128/naya_repo.git/': The requested URL returned error: 403

- 原因  
    GitHubでhttpsのパスワード認証が廃止
- 解決方法  
    以下を実施  
    - githubで二段階認証を設定。
    - githubでアクセストークン(repo権限)を発行。
    - Windows資格情報のパスワードをアクセストークンに変更。
    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

## WSLからのプッシュ

- ssh鍵を作って手順を進めるも、以下エラー
    - git githubをwslで使う　初心者用
        - https://qiita.com/TTOM/items/64277258f2dc7a6cb8ac

```
ssh -T git@github.com
...
git@github.com: Permission denied (publickey).
```

- vコマンドで確認 (ssh -vT git@github.com)
```
naka@DESKTOP-0ERPVKH:~/.ssh$ ssh -vT git@github.com
OpenSSH_8.2p1 Ubuntu-4ubuntu0.7, OpenSSL 1.1.1f  31 Mar 2020
debug1: Reading configuration data /etc/ssh/ssh_config
debug1: /etc/ssh/ssh_config line 19: include /etc/ssh/ssh_config.d/*.conf matched no files
debug1: /etc/ssh/ssh_config line 21: Applying options for *
debug1: Connecting to github.com [20.27.177.113] port 22.
debug1: Connection established.
debug1: identity file /home/naka/.ssh/id_rsa type 0
debug1: identity file /home/naka/.ssh/id_rsa-cert type -1
debug1: identity file /home/naka/.ssh/id_dsa type -1
debug1: identity file /home/naka/.ssh/id_dsa-cert type -1
debug1: identity file /home/naka/.ssh/id_ecdsa type -1
debug1: identity file /home/naka/.ssh/id_ecdsa-cert type -1
debug1: identity file /home/naka/.ssh/id_ecdsa_sk type -1
debug1: identity file /home/naka/.ssh/id_ecdsa_sk-cert type -1
debug1: identity file /home/naka/.ssh/id_ed25519 type -1
debug1: identity file /home/naka/.ssh/id_ed25519-cert type -1
debug1: identity file /home/naka/.ssh/id_ed25519_sk type -1
debug1: identity file /home/naka/.ssh/id_ed25519_sk-cert type -1
debug1: identity file /home/naka/.ssh/id_xmss type -1
debug1: identity file /home/naka/.ssh/id_xmss-cert type -1
debug1: Local version string SSH-2.0-OpenSSH_8.2p1 Ubuntu-4ubuntu0.7
debug1: Remote protocol version 2.0, remote software version babeld-6664243a
debug1: no match: babeld-6664243a
debug1: Authenticating to github.com:22 as 'git'
debug1: SSH2_MSG_KEXINIT sent
debug1: SSH2_MSG_KEXINIT received
debug1: kex: algorithm: curve25519-sha256
debug1: kex: host key algorithm: ecdsa-sha2-nistp256
debug1: kex: server->client cipher: chacha20-poly1305@openssh.com MAC: <implicit> compression: none
debug1: kex: client->server cipher: chacha20-poly1305@openssh.com MAC: <implicit> compression: none
debug1: expecting SSH2_MSG_KEX_ECDH_REPLY
debug1: Server host key: ecdsa-sha2-nistp256 SHA256:p2QAMXNIC1TJYWeIOttrVc98/R1BUFWu3/LiyKgUfQM
debug1: Host 'github.com' is known and matches the ECDSA host key.
debug1: Found key in /home/naka/.ssh/known_hosts:1
debug1: rekey out after 134217728 blocks
debug1: SSH2_MSG_NEWKEYS sent
debug1: expecting SSH2_MSG_NEWKEYS
debug1: SSH2_MSG_NEWKEYS received
debug1: rekey in after 134217728 blocks
debug1: Will attempt key: /home/naka/.ssh/id_rsa RSA SHA256:eqDgH6UUnXstzgYAGLdyyDv0smYPrqoKBLoWt1giFas
debug1: Will attempt key: /home/naka/.ssh/id_dsa
debug1: Will attempt key: /home/naka/.ssh/id_ecdsa
debug1: Will attempt key: /home/naka/.ssh/id_ecdsa_sk
debug1: Will attempt key: /home/naka/.ssh/id_ed25519
debug1: Will attempt key: /home/naka/.ssh/id_ed25519_sk
debug1: Will attempt key: /home/naka/.ssh/id_xmss
debug1: SSH2_MSG_EXT_INFO received
debug1: kex_input_ext_info: server-sig-algs=<ssh-ed25519-cert-v01@openssh.com,ecdsa-sha2-nistp521-cert-v01@openssh.com,ecdsa-sha2-nistp384-cert-v01@openssh.com,ecdsa-sha2-nistp256-cert-v01@openssh.com,sk-ssh-ed25519-cert-v01@openssh.com,sk-ecdsa-sha2-nistp256-cert-v01@openssh.com,rsa-sha2-512-cert-v01@openssh.com,rsa-sha2-256-cert-v01@openssh.com,ssh-rsa-cert-v01@openssh.com,sk-ssh-ed25519@openssh.com,sk-ecdsa-sha2-nistp256@openssh.com,ssh-ed25519,ecdsa-sha2-nistp521,ecdsa-sha2-nistp384,ecdsa-sha2-nistp256,rsa-sha2-512,rsa-sha2-256,ssh-rsa>
debug1: SSH2_MSG_SERVICE_ACCEPT received
debug1: Authentications that can continue: publickey
debug1: Next authentication method: publickey
debug1: Offering public key: /home/naka/.ssh/id_rsa RSA SHA256:eqDgH6UUnXstzgYAGLdyyDv0smYPrqoKBLoWt1giFas
debug1: Authentications that can continue: publickey
debug1: Trying private key: /home/naka/.ssh/id_dsa
debug1: Trying private key: /home/naka/.ssh/id_ecdsa
debug1: Trying private key: /home/naka/.ssh/id_ecdsa_sk
debug1: Trying private key: /home/naka/.ssh/id_ed25519
debug1: Trying private key: /home/naka/.ssh/id_ed25519_sk
debug1: Trying private key: /home/naka/.ssh/id_xmss
debug1: No more authentication methods to try.
git@github.com: Permission denied (publickey).
```


### 問題点
- id_rsaの中身をコピーしてしまっていた。
- 必要なのはid_rsa.pubの中身


## アクセストークン認証（WSL）
- 以下をWSLで実行

```
git config --global credential.helper "/mnt/c/Program\ Files/Git/mingw64/libexec/git-core/git-credential-manager-core.exe"
```