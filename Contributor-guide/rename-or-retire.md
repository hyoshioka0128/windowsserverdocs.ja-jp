# <a name="rename-or-delete-an-article"></a>名前を変更したり、アーティクルの削除

名前を変更したり、アーティクルを削除する前に回避または壊れたリンクの数を削減するには、このプロセスに従う必要があります。 お客様は、壊れたリンクが嫌いし、いずれかのヒット時オフ発音の似たはありません。 名前を変更するか、アーティクルを削除する最後の手順では、このプロセスは、最初ではありません。


## <a name="step-1-manage-inbound-links"></a>手順 1:受信リンクを管理します。

ブログ、フォーラム、および web 上の他のコンテンツなど、コンテンツへの Microsoft 以外の受信リンクがあるかどうかを決定します。 これらのリンクを変更するブログ所有者にお問い合わせくださいと削除、またはフォーラムの投稿からのリンクを更新します。 Web 分析ツールは、大量のトラフィックの受信リンクがこの方法で管理する必要がありますを識別できます。

## <a name="step-2-remove-all-crosslinks-to-the-article-from-the-windowsserverdocs-pr-repository"></a>手順 2:WindowsServerDocs pr リポジトリからの記事をすべてのクロスリンクを削除します。

1. 更新、ローカル ブランチ – 実行`git pull upstream <branch>`、ie にマスターから更新実行してください `git pull upstream master`

2.  名前を変更したり、インベントリから削除する記事へのリンクの記事を検索する WindowsServerDocs pr フォルダーをスキャンし、更新、記事のリンクを削除するか、別の記事へのリンクで置き換えることをします。 検索を使用して、インストールされているいずれかがある場合は、クロスリンクを検索するためのユーティリティを置換できます。 ない場合は、Windows PowerShell を使用することができます。

 a.  Windows PowerShell を起動します。

 b.  PowerShell プロンプトで、WindowsServerDocs pr フォルダーに変更します。

 `cd WindowsServerDocs-pr\WindowsServerDocs-pr`

 c. 名前変更または削除するアーティクルへのリンクが含まれているすべてのファイルを一覧表示コマンドを実行します。

 `Get-ChildItem -Recurse -Include *.md* | Select-String "<the name of the topic you are deleting>" | group path | select name`

  ファイル名の一覧をテキスト ファイル (この場合、psoutput.txt という名前) を送信するには、次のコマンドを実行します。

  `Get-ChildItem -Recurse -Include *.md* | Select-String "<the name of the topic you are deleting>" | group path | select name | Out-File C:\Users\<your account>\psoutput.txt`

3. 追加し、すべての変更をコミット、それらを独自のフォークにプッシュおよびプル要求を開きます。 手順については、次を参照してください。 [Git コマンドを作成または更新記事](git-steps-create-update-content.md)します。

## <a name="step-3-update-fwlinks"></a>手順 3:Fwlink を更新します。

任意の記事を指す Fwlink FWLink ツールを確認します。 置換するコンテンツは、Fwlink をポイントします。リンクを所有するエイリアスではない場合は、結合します。 所有者がリンクに更新されない場合は、MSCOM 変更リンクでチケットを提出します。 詳細については、[内部 wiki](http://sharepoint/sites/azurecontentguidance/wiki/Pages/Manage%20inbound%20links%20to%20retired%20topics.aspx)します。

## <a name="step-4-remove-crosslinks-to-the-article-from-table-of-contents"></a>手順 4:コンテンツのテーブルからの資料をクロスリンクを削除します。

ToC.md ファイルを管理する人で動作します。 このファイルは、テクニカル ライブラリの内容の左側のテーブルを設定します。 問い合わせ先がわからない場合に電子メールを送信wssc-pra@microsoft.comします。

## <a name="step-5-add-redirects"></a>手順 5:リダイレクトを追加します。
ファイルを削除する以上の名前を変更している場合は、既存のリンクが中断されないように、リダイレクトを追加します。

1. 既存のファイル名を持つ既存の場所にファイルを古いままにします。
2. ファイルの内容は、メタデータのこの部分に置き換えます。
   ```
   ---
   redirect_url: <redirection-URL-or-file>
   ---
   ```
   \<リダイレクト URL ファイル > は別の場所の完全な URL またはパス + ファイル名を同じ OPS リポジトリ内の別のトピックです。

   たとえば、ファイル全体をられます。

   ```
   ---
   redirect_url: ../../failover-clustering/whats-new-in-failover-clustering
   ---
   ```

3. 後のリダイレクト、プル要求のリダイレクトが正常に動作している場合は、コメント内のリンクは、ターゲット トピックを表示する必要があります をクリックして、PR を作成します。

## <a name="step-6-rename-or-delete-the-article"></a>手順 6:名前を変更したり、アーティクルを削除

リダイレクトを使用していない場合は、前の手順を完了して、影響を受けるすべての記事が公開された後、この手順を実行します。 リダイレクトを使用している場合名前を変更するか、アーティクルを削除しています、これを元に戻すして、壊れたリンクが発生します。 ファイルの名前を変更するには、単に、ファイル システムで名前を変更し、追加、コミットし、変更をプッシュおよびプル要求を開きます。
まず、ファイルを削除するには、のみ、これは、ソース管理システムと、これを行うためのものを認識する必要があるため、ファイル システムからファイルを削除するが機能しないことを知る必要があります。 それ以外の場合、削除されたファイルは再表示可能性があります。
これには 2 つの方法があります。

- ファイル システムと git の場合:ファイル システムからファイルを削除します。 Git ツールから、次のいずれかを実行します。  ```Git add -A``` | ```Git add --all``` | ```Git add -u```
- Git の単なる: ```git rm foo.md```を実行します。

    詳細については[ http://stackoverflow.com/questions/2047465/how-can-i-delete-a-file-from-git-repo ](http://stackoverflow.com/questions/2047465/how-can-i-delete-a-file-from-git-repo)と [https://git-scm.com/docs/git-rm](https://git-scm.com/docs/git-rm) 

## <a name="step-7-find-and-fix-straggler-broken-links"></a>手順 7:見つけて straggler 壊れたリンクの修正

コンテンツの QA ツールを使用して、壊れたリンクを前の手順しなかった catch、し、削除するか、リンクの修正を検索します。

## <a name="step-8-remove-cached-pages-from-search-engines"></a>手順 8:検索エンジンからキャッシュされたページを削除します。

検索エンジンからキャッシュされた web ページを削除するには、この web ページに移動します。[Bing](https://www.bing.com/webmaster/tools/content-removal?rflid=1)
[Google](https://www.google.com/webmasters/tools/removals?pli=1)


### <a name="contributors-guide-links"></a>共同作成者ガイドへのリンク

- [ガイダンスの記事のインデックス](./contributor-guide-index.md)

