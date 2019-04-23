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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879563"
---
# <a name="metadata-and-markdown-template"></a>メタデータと Markdown テンプレート

この OPS テンプレートには、メタデータの設定に関するガイダンスと同様に、マークダウン構文の例が含まれています。 最大限に得るに、両方を表示する必要があります、[生のマークダウン](https://raw.githubusercontent.com/Microsoft/WindowsServerDocs-pr/master/Contributor-guide/ws-template.md?token=AG1vEhARRHNLtPgKXP35BGjNZGajKOArks5YLNIwwA%3D%3D)と[表示ビュー](https://github.com/Microsoft/WindowsServerDocs-pr/blob/master/Contributor-guide/ws-template.md)します。 (生のマークダウンいますが、メタデータ ブロックに描画されたビューはありません。)

マークダウン ファイルを作成するときにこのテンプレートを新しいファイルにコピーします。 以下に指定されたセットとして、情報の記事のタイトルを上の H1 見出し、メタデータを入力、コンテンツを削除してください。 角かっこで CAPS で何も、注意が必要です。


## <a name="metadata"></a>メタデータ 

完全なメタデータ ブロックされます。 重要事項:

- **する必要があります**コロン (:) とメタデータ要素の値の間にスペースを入れます。
- 値 (たとえば、タイトル) 内のコロンは、メタデータ パーサーを中断します。 代わりに HTML エンコードのコロンを使用して、 `&#58;` (たとえば、 `"title: Azure Rights Management&#58; the basics | Azure RMS"`)。
- **タイトル**:このタイトルは、検索エンジン結果に表示されます。 
- **作成者**:[作成者] フィールドを含める必要があります、 **GitHub ユーザー名**の作成者のエイリアスではありません。
- **ms.prod**, **ms.technology**:「Windows server しきい値」を使用して、ms.prod: (または w10 このテンプレートを使用して、Windows 10 のコンテンツを作成する場合)。 Ms.technology: 値を取得する CX 取引先担当者に問い合わせてください。

## <a name="basic-markdown-gfm-and-special-characters"></a>基本マークダウン、GFM、および特殊文字

すべての basic、および GitHub flavored Markdown がサポートされています。 これらの詳細についてを参照してください。

- [ベースライン マークダウン構文](https://daringfireball.net/projects/markdown/syntax)
- [GitHub フレーバー Markdown (GFM) ドキュメント](https://guides.github.com/features/mastering-markdown)

Markdown などの特殊文字の使用\*、 \`、および\#の書式設定します。 これらの文字のいずれかをコンテンツに含める場合は、次の 2 つのいずれかを行う必要があります。

- 「エスケープ」する特殊文字の前にバック スラッシュを入力 (たとえば、 \\ \*の\*)
- 使用して、 [HTML エンティティ コード](http://www.ascii.cl/htmlcodes.htm)文字の (たとえば、 \& \#42\;の&#42;)。

## <a name="headings"></a>見出し

見出しを行う必要があります atx スタイルを使用して、使用して、1. ~ 6. ハッシュ文字 (#)、行の先頭を HTML 見出しレベルの H1 〜 H6 に対応する、見出しを示すためにします。 最初と 2 番目のレベルのヘッダーの例については、上に使用されます。 

ある**する必要があります**ページ上のタイトルとして表示されるトピックの最初のレベル見出し (H1) 1 つだけです。  

2 番目のレベルの見出しでは、ページのタイトルの下に"で、この記事の内容」セクションに表示されるページ上の目次を生成します。

### <a name="third-level-heading"></a>第 3 レベルの見出し
#### <a name="fourth-level-heading"></a>第 4 レベルの見出し
##### <a name="fifth-level-heading"></a>5 番目のレベルの見出し
###### <a name="sixth-level-heading"></a>6 番目のレベルの見出し

## <a name="text-styling"></a>テキスト スタイルの設定

*斜体* 

**太字** 

~~取り消し線~~

## <a name="links"></a>リンク

### <a name="internal-links"></a>内部リンク

同じマークダウン ファイル内のヘッダーにリンクするには、パブリッシュされたアーティクルのソースを表示、ヘッドの ID を検索 (たとえば、 `id="blockquote"`)、# と id を使用してリンクし、(たとえば、 `#blockquote`)。

- 以下に例を示します。[ブロック引用](#blockquote)

同じリポジトリ内のマークダウン ファイルにリンクするには、使用[相対リンク](https://www.w3.org/TR/WD-html40-970917/htmlweb.html#h-5.1.2)、ファイル名の末尾に".md"を含むです。

- 以下に例を示します。[ヒントと潜在的な問題](tips-gotchas.md)
- 以下に例を示します。[ツールとの共同作成者用のセットアップ](../readme.md)

同じリポジトリ内のマークダウン ファイル内のヘッダーにリンクするには、相対リンクとハッシュタグ リンクを使用します。

- 以下に例を示します。[ファイルを削除します。](tips-gotchas.md#deleting-files)

### <a name="external-links"></a>外部リンク

外部ファイルにリンクするには、リンクとして完全な URL を使用します。

- 以下に例を示します。[GitHub](http://www.github.com)

マークダウン ファイル内の URL が表示された場合は、クリック可能なリンクに変換されます。

- 例: http://www.github.com

## <a name="lists"></a>リスト

### <a name="ordered-lists"></a>順序付きリスト

1. この 
1. します。
1. を
1. 順序付け
1. 一覧  


#### <a name="ordered-list-with-an-embedded-list"></a>順序付けられた埋め込みリストを持つ一覧

1. ここは
1. します。
1. を
1. 埋め込み
    1. ミス ヨハンソン
    1. Plum 教授
1. 順序付け
1. list


### <a name="unordered-lists"></a>順序なしリスト

- この
- が
- a
- 箇条書き
- list


##### <a name="unordered-list-with-an-embedded-list"></a>埋め込みリストを持つ順序付けられていないリスト

- この 
- 箇条書き 
- list
    - 加藤さんの mrs.
    - Mr. 緑
- 含まれています  
- その他
    1. Mustard 大佐
    1. Mrs. ホワイト
- 一覧表示します。


## <a name="horizontal-rule"></a>水平線

---

## <a name="tables"></a>テーブル

ほぼすべてのインスタンスでは、テーブル書式を MD を使用します。 HTML テーブルに柔軟性が向上されません、使用、コンテンツ。 HTML テーブルにある場合に、この記事では、私たちと、その記事ではマージできません。

| テーブル        | は           | クール  |
| ------------- |:-------------:| -----:|
| 列 3 は      | 右揃え | $1600 |
| 列 2 は      | 中央揃え      |   $12 |
| 列 1 は既定値です。 | 左揃え     |    $1 |


## <a name="code"></a>コード

### <a name="generic-codeblock"></a>ジェネリック codeblock

ジェネリック codeblock をコーディングするためのコード 4 スペースのインデントを設定します。

    function fancyAlert(arg) {
      if(arg) {
        $.docs({div:'#foo'})
      }
    }


### <a name="codeblocks-with-language-identifier"></a>言語識別子を持つ Codeblocks

使用して、3 つのバッククォート (&#96;&#96;&#96;) + コード ブロック コーディング言語に固有の色を適用する言語の ID。  すべての一覧を次に示します[GitHub Flavored Markdown (GFM) 言語 Id](https://github.com/jmm/gfm-lang-ids/wiki/GitHub-Flavored-Markdown-(GFM)-language-IDs)します。

##### <a name="c9839"></a>C&AMP;#9839;

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

使用して、バッククォート (&#96;) の`inline code`します。

## <a name="blockquotes"></a>ブロック引用

> すでにのようになりました 1000万年間、継続がおよびのとうに終わっていた。 ここでは 1 日と呼ばれる、アフリカになる大陸で、赤道の存在の戦いに達し極めの新しい生存し、victor 氏が、まだ視認でします。 この干からびたともの land 小さなのみまたは、swift、厳しいでしたすばしっこく、またはも存続することと思います。

## <a name="images"></a>画像

### <a name="static-image"></a>静的イメージ

![これは、alt テキスト](../windowsserverdocs/get-started/media/wsbanner.png)

### <a name="linked-image"></a>リンクされている画像

[![リンクされたイメージの代替テキスト](../windowsserverdocs/get-started/nano.png)](../windowsserverdocs/get-started/getting-started-with-nano-server.md) 

## <a name="alerts"></a>オブジェクト エクスプローラーには

### <a name="note"></a>注

> [!NOTE]
> これは注記です。

### <a name="warning"></a>警告

> [!WARNING]
> これは警告です。

### <a name="tip"></a>ヒント

> [!TIP]
> これはヒントです。

### <a name="important"></a>重要

> [!IMPORTANT]
> これは重要です。

