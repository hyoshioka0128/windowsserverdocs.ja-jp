---
title:
- 記事のタイトル
description: ''
author:
- GITHUB USERNAME
ms.author:
- MICROSOFT ALIAS
ms.date:
- DATE
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: ''
ms.localizationpriority:
- high/medium/low
ms.openlocfilehash: 4f885680426c0bfa55d5f73a7ef0c2143a8dd5a9
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2018
ms.locfileid: "2082349"
---
# <a name="metadata-and-markdown-template"></a>メタデータと値下げテンプレート

この OPS テンプレートは、メタデータの設定に関するガイドラインと同様に、値下げ構文の例を示します。 大部分を移動するには、[生値下げ](https://raw.githubusercontent.com/Microsoft/WindowsServerDocs-pr/master/Contributor-guide/ws-template.md?token=AG1vEhARRHNLtPgKXP35BGjNZGajKOArks5YLNIwwA%3D%3D)と[ビューを表示](https://github.com/Microsoft/WindowsServerDocs-pr/blob/master/Contributor-guide/ws-template.md)するの両方を表示する必要があります。 (生値下げいますが、メタデータ ブロック表示していないときに。)

値下げのファイルを作成するときにこのテンプレートを新しいファイルにコピー] の下に指定されたセットとして、H1 見出しを上にあるタイトルは、この記事のメタデータを入力、コンテンツを削除してください。 角かっこで大文字に何も注意が必要です。


## <a name="metadata"></a>Metadata 

完全なメタデータ ブロックされます。 いくつかの重要な注意点:

- コロン (:) とメタデータ要素の値の間にスペースがある**必要があります**があります。
- コロン (タイトルなど) の値には、メタデータ パーサーを解除します。 HTML のコロンのエンコードを使用する代わりに`&#58;`(たとえば、 `"title: Azure Rights Management&#58; the basics | Azure RMS"`)。
- **タイトル**: このタイトルは、検索エンジンの結果に表示されます。 
- **作成者**: author フィールドがないエイリアス、作成者の**GitHub ユーザー名**を含める必要があります。
- **ms.prod**、 **ms.technology**: ms.prod (または Windows 10 用のコンテンツを作成するのには、このテンプレートを使っている場合は、w10)「windows server しきい値」を使用します。 Ms.technology 値を取得する CX 相手に問い合わせてください。

## <a name="basic-markdown-gfm-and-special-characters"></a>基本的な値下げ、GFM、および特殊文字

すべての基本的なと GitHub 系値下げはサポートされません。 これらの詳細についてを参照してください。

- [[基準計画値下げ構文](https://daringfireball.net/projects/markdown/syntax)
- [GitHub 系値下げ (GFM) のドキュメント](https://guides.github.com/features/mastering-markdown)

値下げが次のような特殊文字を使用して \ *、\'、および \ 番号の書式設定します。 コンテンツにこれらの文字のいずれかを含める場合は、次の 2 つのいずれかを行う必要があります。

- 特殊文字を「エスケープ」する前にバック スラッシュを入力 (たとえば、\\\ * の \ *)
- 文字の[エンティティの HTML コード](http://www.ascii.cl/htmlcodes.htm)を使用して (たとえば、\ & \#42\ の & #42;) します。

## <a name="headings"></a>見出し

見出しを行う必要があります atx スタイルを使用して、つまりを使用して 1 ~ 6 時ハッシュ (#)、行の先頭を H6 を通じて見出しレベル H1 HTML に対応する見出しを指定します。 最初の 2 番目のレベルの見出しの例は、上に使用されます。 

ある**ページ上のタイトルと表示される、議題の第 1 レベル見出し (H1) 1 つだけ必要があります**。  

第 2 レベル見出しでは、ページ上のタイトルの下では、"ここ"セクションに表示されるページ上の TOC を生成します。

### <a name="third-level-heading"></a>第 3 レベル見出し
#### <a name="fourth-level-heading"></a>4 番目のレベルの見出し
##### <a name="fifth-level-heading"></a>5 レベル見出し
###### <a name="sixth-level-heading"></a>6 番目のレベルの見出し

## <a name="text-styling"></a>テキスト スタイル

*斜体* 

**Bold** 

~~取り消し線~~

## <a name="links"></a>Links

### <a name="internal-links"></a>内部リンク

同じ値下げファイルでのヘッダーにリンクするには、パブリッシュされたアーティクルのソースを表示、先頭の ID を検索 (たとえば、 `id="blockquote"`)、# + id を使用してリンクと (たとえば、 `#blockquote`)。

- 例: [Blockquotes](#blockquote)

同じリポジトリの索引の値下げファイルにリンクするには、[相対リンク](https://www.w3.org/TR/WD-html40-970917/htmlweb.html#h-5.1.2)、ファイル名の末尾に".md"を含むを使用します。

- 例:[ヒントおよび了解事項](tips-gotchas.md)
- 例:[ツールと共同作成者の設定](../readme.md)

同じリポジトリの索引の値下げファイルでのヘッダーに、リンクするには、相対リンク + ハッシュタグのリンクを使用します。

- 例:[ファイルを削除します。](tips-gotchas.md#deleting-files)

### <a name="external-links"></a>外部リンク

外部ファイルにリンクするには、[リンクとして、完全な URL を使用します。

- 例: [GitHub](http://www.github.com)

値下げファイルの URL が表示された場合は、クリックできるリンクに変換されます。

- 例:http://www.github.com

## <a name="lists"></a>リスト

### <a name="ordered-lists"></a>順序付きリスト

1. これ 
1. します。
1. する
1. 注文
1. リスト  


#### <a name="ordered-list-with-an-embedded-list"></a>埋め込まれたリストを使用してリストの注文

1. ここは
1. します。
1. する
1. 埋め込まれました。
    1. ミス Scarlett
    1. 教授プラム
1. 注文
1. list


### <a name="unordered-lists"></a>並べ替えられていないリスト

- これ
-  が 
- a
- 箇条書き
- list


##### <a name="unordered-list-with-an-embedded-list"></a>埋め込まれたリストを使用して並べ替えられていないリスト

- これ 
- 箇条書き 
- list
    - 青木さんの mrs.
    - 緑の氏
- 含まれています。  
- その他
    1. 大佐マスタード
    1. 白の mrs.
- リスト


## <a name="horizontal-rule"></a>水平線

---

## <a name="tables"></a>テーブル

ほとんどすべてのインスタンスで MD テーブルの書式設定を使用します。 HTML テーブル柔軟性を提供するときにされませんでそれを使ってコンテンツ。 」で、HTML テーブルがあれば、その資料いないマージされます。

| テーブル        | します。           | 冷却  |
| ------------- |:-------------:| -----:|
| 3 列には      | 右揃え | ¥ 1600 |
| 2 段が      | 中央揃え      |   $12 |
| 1 段が既定値です。 | 左揃え     |    $ 1 |


## <a name="code"></a>コード

### <a name="generic-codeblock"></a>一般的な使って

一般的な使ってコーディングのコード 4 スペースのインデントを設定します。

    function fancyAlert(arg) {
      if(arg) {
        $.docs({div:'#foo'})
      }
    }


### <a name="codeblocks-with-language-identifier"></a>言語の識別子を持つ Codeblocks

3 つのダンプ (と #96。 と #96。 &) を使う #96; コード ブロック コーディング言語固有の色を適用する言語 ID + します。  すべての[GitHub Flavored 値下げ (GFM) 言語 Id](https://github.com/jmm/gfm-lang-ids/wiki/GitHub-Flavored-Markdown-(GFM)-language-IDs)の一覧を示します。

##### <a name="c9839"></a>C と #9839 です。

```c#
using System;
namespace HelloWorld
{
    class Hello 
    {
        static void Main() 
        {
            Console.WriteLine("Hello World!");

            // Keep the console window open in debug mode.
            Console.WriteLine("Press any key to exit.");
            Console.ReadKey();
        }
    }
}
```
#### <a name="python"></a>Python

```python
friends = ['john', 'pat', 'gary', 'michael']
for i, name in enumerate(friends):
    print "iteration {iteration} is {name}".format(iteration=i, name=name)
```
#### <a name="powershell"></a>PowerShell

```powershell
Clear-Host
$Directory = "C:\Windows\"
$Files = Get-Childitem $Directory -recurse -Include *.log `
-ErrorAction SilentlyContinue
```

### <a name="inline-code"></a>インライン コード

ダンプ (& #96;) を使用しての`inline code`します。

## <a name="blockquotes"></a>Blockquotes

> 10 ドル年、日照りを今すぐ続いたし、恐ろしいわかったの治世が終了した期間後します。 ここでは 1 日と呼ばれる、アフリカ大陸で、赤道上の存在を戦闘に達した残忍の新しい climax と、ビクターされましたまだ表示したまま。 この不毛と地 land 小さなのみまたは swift、厳しい可能性のあるフローリッシュ、または維持 。

## <a name="images"></a>画像

### <a name="static-image"></a>静的な画像

![これは、代替テキスト](../windowsserverdocs/get-started/media/wsbanner.png)

### <a name="linked-image"></a>リンクされた画像

[![aリンクされた画像の長期テキスト](../windowsserverdocs/get-started/nano.png)](../windowsserverdocs/get-started/getting-started-with-nano-server.md) 

## <a name="alerts"></a>[アラート]

### <a name="note"></a>注

> [!NOTE]
> これは、メモ

### <a name="warning"></a>Warning

> [!WARNING]
> これは、警告が表示されます。

### <a name="tip"></a>ヒント

> [!TIP]
> これは、ヒント

### <a name="important"></a>重要

> [!IMPORTANT]
> これは、重要なタスク

