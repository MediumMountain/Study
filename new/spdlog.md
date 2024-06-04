# SPDLOG
- GitHubで公開されているヘッダオンリーのC++用のログ出力ライブラリで、簡単に導入・高機能なログ出力を行うことができる。

https://github.com/gabime/spdlog


## メリット
- iostream の代替であるオープンソースのフォーマットライブラリ「{fmt}」を使用しているため、pythonのformat()メソッドのようにシンプルに記述できる
- 信頼性・安全性が高い
- パフォーマンスが良い(速い)
- MITライセンスである

## デメリット
- テンプレートをたくさん使用しているためコンパイルが遅くなる
    - どれくらい遅くなるのか？



# logger

spd関連の出力関数が明示的に作成されず呼び出された場合、デフォルトのパラメータをもったロガーが自動的に作成される



# sink


# レジストリ


# formatter


# thread pool


# 非同期





## REFERENCE

spdlog ログ ライブラリのソース コード:
https://www.cnblogs.com/fortunely/p/16838749.html


spdlog の非同期ロギング スキーム
https://blog.csdn.net/weixin_73240939/article/details/135228656?spm=1001.2101.3001.6650.4&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-4-135228656-blog-125075334.235%5Ev43%5Epc_blog_bottom_relevance_base6&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-4-135228656-blog-125075334.235%5Ev43%5Epc_blog_bottom_relevance_base6&utm_relevant_index=9