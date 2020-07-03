---
title: fsutil reparsepoint
description: 再解析ポイントを照会または削除する fsutil reparsepoint コマンドの参照記事です。
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.assetid: fb95c8ee-a418-4520-a12a-7754ae947c3c
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: edbbc578b6a84ebd4e342493e29cbe2bd5c5a2cd
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931216"
---
# <a name="fsutil-reparsepoint"></a>fsutil reparsepoint

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8

再解析ポイントを照会または削除します。  **Fsutil reparsepoint**コマンドは、通常、サポート担当者によって使用されます。

再解析ポイントは、ユーザー定義のデータを含む、定義可能な属性を持つ NTFS ファイルシステムオブジェクトです。 これらの使用方法は次のとおりです。

- 入出力 (i/o) サブシステムの機能を拡張します。

- ディレクトリ接合ポイントおよびボリュームマウントポイントとして機能します。

- 特定のファイルをファイルシステムフィルタードライバーに特別なマークを付けます。

## <a name="syntax"></a>構文

```
fsutil reparsepoint [query] <filename>
fsutil reparsepoint [delete] <filename>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| query | 指定したハンドルによって識別されるファイルまたはディレクトリに関連付けられている再解析ポイントデータを取得します。 |
| delete | 指定したハンドルによって識別されるファイルまたはディレクトリから再解析ポイントを削除します。ただし、ファイルまたはディレクトリは削除しません。 |
| `<filename>` | ファイル名と拡張子を含むファイルへの完全パスを指定します (例*C:\documents\filename.txt*)。 |

#### <a name="remarks"></a>注釈

- プログラムは、再解析ポイントを設定すると、このデータと再解析タグを格納します。このタグは、格納されているデータを一意に識別します。 ファイルシステムは、再解析ポイントを使用してファイルを開くと、関連付けられているファイルシステムフィルターの検索を試みます。 ファイルシステムフィルターが見つかった場合、フィルターは再解析データによって指示されたファイルを処理します。 ファイルシステムフィルターが見つからない場合、**ファイルオープン**操作は失敗します。

### <a name="examples"></a>例

*C:\ サーバー*に関連付けられている再解析ポイントデータを取得するには、次のように入力します。

```
fsutil reparsepoint query c:\server
```

指定したファイルまたはディレクトリから再解析ポイントを削除するには、次の形式を使用します。

```
fsutil reparsepoint delete c:\server
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [fsutil](fsutil.md)
