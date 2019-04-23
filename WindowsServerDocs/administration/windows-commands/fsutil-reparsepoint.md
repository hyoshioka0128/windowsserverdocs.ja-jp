---
ms.assetid: fb95c8ee-a418-4520-a12a-7754ae947c3c
title: fsutil reparsepoint
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 940131a02a5cd3a6122022cf9b0dff3281d1dabf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847943"
---
# <a name="fsutil-reparsepoint"></a>fsutil reparsepoint
>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7、Windows 2008、Windows Vista

再解析ポイントのクエリまたは削除します。  **Fsutil reparsepoint**コマンドは、通常のサポート担当者によって使用されます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
fsutil reparsepoint [query] <FileName>
fsutil reparsepoint [delete] <FileName>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------------|---------------|
|クエリ (query)|ファイルまたは指定したハンドルによって識別されたディレクトリに関連付けられている再解析ポイントのデータを取得します。|
|delete|ファイルまたはディレクトリを指定したハンドルによって識別されますが、ファイルまたはディレクトリを削除しませんから、再解析ポイントを削除します。|
|<FileName>|ファイル名と拡張子、たとえば C:\documents\filename.txt を含むファイルへの完全パスを指定します。|

## <a name="remarks"></a>注釈

-   再解析ポイントは NTFS ファイルをユーザー定義のデータを含む定義可能な属性を持つシステム オブジェクトであり、入力/出力 (I/O) のサブシステムでの機能を拡張するために使用します。

-   再解析ポイントは、ディレクトリの接合ポイントとボリューム マウント ポイントに使用されます。 ファイル システム フィルター ドライバーでドライバーを特別なものとして特定のファイルをマークにも使用されます。

-   プログラムが再解析ポイントを設定すると、このデータと格納しているデータを一意に識別する再解析タグを格納します。 ファイル システムでは、再解析ポイントと、ファイルを開くときに、関連付けられているファイル システム フィルターを検索しようとします。 ファイル システム フィルターが見つかった場合、フィルターは、再解析データの指示に従って、ファイルを処理します。 ファイル システム フィルターが見つからない場合、ファイルを開く操作は失敗します。

## <a name="BKMK_examples"></a>例
関連付けられた C:\Server 再解析ポイントのデータを取得するには、次のように入力します。

```
fsutil reparsepoint query c:\server
```

再解析ポイントを指定したファイルまたはディレクトリから削除するには、次の形式を使用します。

```
fsutil reparsepoint delete c:\server
```

#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文キー](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)


