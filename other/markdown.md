#   Markdown記法

#   見出し
##  #の数を変えることで
### 見出しのレベルを
####    調整できる
#####    1~6個

#   箇条書きリスト
-, +, *, を使用。項目の間には半角スペースを1つ入れる
- ハイフン
    - ハイフン
        - ハイフン
+ プラス
* アスタリスク

#   番号付きリスト
1. 数値+半角ドット
    1. 番号の内容は何でもいい。
    1. 実際に表示される際に適切な番号で表示される。
1. 数値+半角ドットと箇条書きの
1. 項目の間には半角スペースを1つ入れる

#   テキストの装飾

*イタリック*
**太字**
~~打消し線~~


# 引用
>引用した部分
>
>こここ
>>二重使用


#code記法
バッククォートで囲むと `code no itibu ` を記載できる

## ソースコード
複数行の場合は ```java のように言語を指定すればVS CodeやGitHub,Gitbucketではハイライトもつけてくれる

 
```php
//複数行のソースコード
$test = 'test';
return $test
```

対応言語は[rouge](http://rouge.jneen.net/v3.26.0/c/)に準ずる  


# 水平線
***
___
---
*    *    *

# 強調
## em
normal *italic* normal  
normal _italic_ normal

## strong
normal **bold** normal  
normal __bold__ normal

## em + strong
normal ***bold*** normal  
normal ___bold___ normal

# 改行
文末に半角空白スペースを2つつける  
1行空白の

行を入れる
<br>タグを使う


# テーブル

| 左寄せ | 中央寄せ | 右寄せ |
|:------|:--------:|-------:|
| 左    | 中央     | 右　   |


|header1|header2|header3|
|:--|--:|:--:|
|align left|align right|align center|
|a|b|c|


# テキストカラー
これは<span style="color: red; ">赤文字</span>です

# 画像
![フクロウ](
https://notepm.jp/assets/img/apple-touch-icon-120x120.png)

# REFERENCE
[Markdown記法 サンプル集](https://qiita.com/tbpgr/items/989c6badefff69377da7)

[Markdown記法/書き方（見出し・表・リンク・画像・文字色など）](https://notepm.jp/help/how-to-markdown)