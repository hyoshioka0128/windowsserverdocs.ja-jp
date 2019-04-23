<properties title="" pageTitle="ファイル名と Windows Server 2016 の技術記事の場所" description="記事と、新しいアーティクルを作成するときに従う必要があります名前付け規則のファイル構造について説明します。" metaKeywords="" services="" solutions="" documentationCenter="" authors="Kathy-Davies" videoId="" scriptId="" manager="required" />

<tags ms.service="contributor-guide" ms.devlang="" ms.topic="article" ms.tgt_pltfrm="" ms.workload="" ms.date="03/14/2016" ms.author="jimpark; tysonn" />

# <a name="file-names-and-locations-for-windows-server-technical-articles"></a>ファイル名と Windows Server の技術記事の場所

理解し、次の規則をより迅速に受け入れられるプル要求を取得できます。

+ [ルール]
+ [パターン]
+ [ファイル名の承認]

## <a name="rules"></a>ルール

- すべてのファイルは、markdown であるし、.md ファイル拡張子を使用する必要があります。
- 可能であれば、3 ~ 5 の単語にファイル名を保持 - 10 個の単語は、実際に読みやすさ、SEO の時間が長すぎます。
- 小文字と文字、数字、およびハイフンを使用します。
- スペースまたは句読点はありません。 ハイフンを使用して、単語と、ファイル名に番号を区切ります。
- アクションの動作の短い形式の使用、'-ing' フォーム:`deploy-nano-server`されません `Deploying-Nano-Server`
- などの小規模のワードを除外まままたはします。
- スペルの単語。ファイル名で承認されていないか、不要な頭字語は避ける
- ファイル名を一意にする必要がありますの代わりに`overview.md`使用 `storage-spaces-overview.md`

頭字語やファイル名 - 特定のガイドラインの頭字語:

- 許容可能な名前の省略形の既存の Microsoft ガイダンスに従う
- 業界標準の省略形は、ファイル名で必要に応じて、許容されます。

## <a name="pattern"></a>[パターン]

既存の名を把握するリポジトリ内のアーティクルの一覧を確認します。 一般的なパターンを次に示します。

 **component-topic-title.md**
 
たとえば、`storage-spaces-direct-overview.md` と記述します。

## <a name="file-name-approval"></a>ファイル名の承認

新しいファイルを送信するときに、プル要求レビュー担当者は、名前を確認し、変更が必要な場合は、プル要求のコメント ストリームを使用してフィードバックを提供します。 ファイル名は、プル要求が受け入れられる前に修正する必要があります。 共同作成者は、保留中のプル要求に、更新プログラムを簡単にプッシュできます。

## <a name="folders-in-the-repo"></a>リポジトリ内のフォルダー

既存のフォルダー構造を使用します。 リポジトリ管理者の承認を受けることがなくフォルダーを作成しないでください。新しいフォルダーを必要とすると思われる場合は、それらを説明します。

GitHub リポジトリは、単純ながあるし、比較的 – のフォルダー構造をフラット\<領域 >\\\<テクノロジ > - 例 storage\data-重複除去します。 そうと、次の利点があります。
 - 非常に簡単です。
 - Azure.com の動作方法と似ています
 - これは、簡単ライター/Pm をすばやく見つける –、トピックを探している特定のテクノロジが入れ子になった他のフォルダーを周囲に詳しく調査する必要はありません。
 - URL の短い、SEO に適していますが保たれ、ユーザー エクスペリエンス、場合によってはお客様のキューの URL を確認します。

## <a name="changing-case-in-file-names"></a>ファイルの名前を変更します。

Windows オペレーティング システムは大文字小文字を区別します。 大文字小文字の区別を修正するファイル名を変更する必要がある場合ことをお勧め、ファイルの内容を変更するには、Linux またはファルダ 次に、例を示します。

  biztalk-administration-and-Development-Task-List-in-BizTalk-Services ・ biztalk-services-administration-and-development-task-list

使用して、`git mv`ファイルの名前を変更するコマンド。
```
  git mv <WindowsServerDocs/tech-area/subarea/current-file-name.md> <WindowsServerDocs/tech-area/subarea/new-file-name.md>
```

### <a name="contributors-guide-links"></a>共同作成者ガイドへのリンク

- [ガイダンスの記事のインデックス](./contributor-guide-index.md)


<!--Anchors-->
[ルール]: #rules
[パターン]: #pattern
[ファイル名の承認]: #file-name-approval
