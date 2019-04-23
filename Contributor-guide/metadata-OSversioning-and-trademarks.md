# <a name="metadata-and-version-identifiers"></a>メタデータとバージョンの識別子

ここでは、商標、バージョン管理、および windowsserverdocs pr リポジトリ内のアーティクルのメタデータについて知っておく必要があります。 記事の作成者は、記事は、これらの標準や要件に従うことを確認します。

## <a name="trademarks"></a>商標
テクニカル ライブラリの記事での製品参照した後、商標記号を使用しないでください。 Technet.microsoft.com や docs.microsoft.com、そしてチャネルを公開するその他の公式 Microsoft が含まれるためは必要ない、[商標](https://www.microsoft.com/trademarks)フッター リンク リストへの Microsoft の商標です。 そのリンクには、法的要件が満たされます。 バック グラウンドからのガイダンスを参照してください[CELA](https://microsoft.sharepoint.com/sites/LCAWeb/Home/Copyrights-Trademarks-and-Patents/Trademarks/Trademark-List-and-Usage)の"web サイト"と Microsoft 文書作成スタイル ガイドを使用すると、[著作権と商標](https://worldready.cloudapp.net/Styleguide/Read?id=2700&topicid=26696)"web ページで Microsoft.com"の下のページ。 

## <a name="versioning"></a>バージョン
複数の種類のバージョン管理は、このリポジトリ内のアーティクルに適用されます。 

-  バージョン管理にアーティクルが適用される製品バージョンを示すには、2 つの方法は行われます。
    - 手動でアーティクルがパブリッシュされたアーティクルにテキストとして表示されているために 1 行。
    - メタデータでは、以下について説明します。
-  ソース コンテンツのバージョン管理は、Github のファイル履歴によって処理されます。 

## <a name="metadata-structure-and-format"></a>メタデータ構造と形式

- H1 見出しの上、ファイルの上部にあるメタデータを配置します。
- ブロックの最初と最後の行で 3 つだけのダッシュを使用して、ファイルの内容の残りの部分から、ブロックを区切ります。 これらの行では、他のテキストを配置しないでください。
- 各メタデータの名前/値ペアを別々 の行に配置します。
- メタデータが定義済みの値が必要ですかカスタム値を受け入れるかどうかに応じて、次の構文パターンのいずれかを使用します。 

        ---
        name1: predefined-value
        name2: "my custom value"
        ---

## <a name="metadata-names-and-values"></a>メタデータの名前と値

特定のメタデータは、その他のメタデータが推奨されますがないために必要なときに、TechNet テクニカル ライブラリのアーティクルとしてパブリッシュするすべてのファイルに必要です。 場合によっては、特定の値のみが、特定のメタデータが許可されます。 

|名前|Value|
|---|---|
|title|H1 見出しに一致するカスタムの値。 [ブラウザー] タブに表示される内容を決定します。|
|description|検索結果に表示され、SEO に影響を与えます。 適切なキーワードを含めるより小さい 160 文字までの長さを保持します。|
|作成者|プライマリ、記事の作成者の Github のエイリアス|
|ms.author|記事で取り上げるテクノロジ分野を担当する記事の作成者やコンテンツ開発者の MSFT エイリアスです。|
|ms.date|コンテンツの更新は最後の日です。 メタデータのみへの変更の更新はありません。 形式年/月/日を使用します。|
|ms.prod|BI レポート、に基づいて、定義済みの Windows Server のバージョンを識別する[値](https://microsoft.sharepoint.com/teams/STBCSI/Insights/_layouts/15/WopiFrame.aspx?sourcedoc=%7b7A321BF1-0611-4184-84DA-A0E964C435FA%7d&file=WEDCS_MasterList_CSIValues.xlsx&action=default&IsList=1&ListId=%7b46B17C8A-CD7E-47ED-A1B6-F2B654B55E2B%7d&ListItemId=969)します。|
|ms.technology|定義済みのベースのレポート、BI テクノロジ領域を識別する[値](https://microsoft.sharepoint.com/teams/STBCSI/Insights/_layouts/15/WopiFrame.aspx?sourcedoc=%7b7A321BF1-0611-4184-84DA-A0E964C435FA%7d&file=WEDCS_MasterList_CSIValues.xlsx&action=default&IsList=1&ListId=%7b46B17C8A-CD7E-47ED-A1B6-F2B654B55E2B%7d&ListItemId=969)|
|ms.asset|BI レポートのすべてのロケールで、情報の記事を識別する GUID です。 記事は、以前作成から移行これは、システムが既にあります。 Github で作成した記事などのツールの使用の[ https://guidgenerator.com/](https://guidgenerator.com/)します。| 

## <a name="troubleshooting"></a>トラブルシューティング

パブリッシュされたアーティクルの上部に表示されるメタデータは、ソース ファイルにフォーマット エラーがある場合に発生します。 一般的なエラーは次のとおりです。

- ブロック、またはハイフンの間違った数の最初と最後の行で 3 倍になるハイフンがありません。
- メタデータは、必要な構文に従っていない:\<名前\>:\<1 つの領域\>\<値 >

これらおよびその他の明らかなエラー、ファイルを確認し、更新されたファイルを発行するための PR を送信します。 進めない場合、電子メール、PR レビュー担当者のエイリアス。 wssc-pra@microsoft.com

## <a name="see-also"></a>関連項目
このリポジトリで使用されるメタデータは国際化 (&)、コンテンツ サービスで使用されるメタデータに基づいて\(CSI\)します。 をオプションのメタデータを含む詳細については、「 [ http://aka.ms/skyeye/meta](http://aka.ms/skyeye/meta)します。
Business intelligence のリソースを参照してください、CSI BI チームの[wiki](https://microsoft.sharepoint.com/teams/STBCSI/Insights/Selfserve%20BI%20wiki/Self-serve%20BI%20wiki.aspx)します。