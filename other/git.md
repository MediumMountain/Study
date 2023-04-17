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
    
## trable shouting

- プッシュ時のエラー  
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

### コマンドメモ
git log  
git branch  
git checkout  
git reset  
git reset --hard  
git rebase  

# git pull 時に以下のエラー
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