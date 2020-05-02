---
ms.assetid: fb95c8ee-a418-4520-a12a-7754ae947c3c
title: Fsutil reparsepoint
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 05c203ef610dda0443ddc845245a4072e617f7a6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725437"
---
# <a name="fsutil-reparsepoint"></a>Fsutil reparsepoint
> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7、windows 2008、Windows Vista

再解析ポイントを照会または削除します。  **Fsutil reparsepoint**コマンドは、通常、サポート担当者によって使用されます。



## <a name="syntax"></a>構文

```
fsutil reparsepoint [query] <FileName>
fsutil reparsepoint [delete] <FileName>
```

### <a name="parameters"></a>パラメーター

| パラメーター  |                                                                [説明]                                                                |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------|
|   query    |            指定したハンドルによって識別されるファイルまたはディレクトリに関連付けられている再解析ポイントデータを取得します。             |
|   delete   | 指定したハンドルによって識別されるファイルまたはディレクトリから再解析ポイントを削除します。ただし、ファイルまたはディレクトリは削除しません。 |
| <FileName> |             ファイル名と拡張子を含むファイルへの完全パスを指定します (例 C:\documents\filename.txt.)。             |

## <a name="remarks"></a>Remarks

-   再解析ポイントは、ユーザー定義データを含む定義可能な属性を持つ NTFS ファイルシステムオブジェクトです。このオブジェクトは、入力/出力 (i/o) サブシステムの機能を拡張するために使用されます。

-   再解析ポイントは、ディレクトリの接合ポイントとボリュームマウントポイントに使用されます。 また、ファイルシステムフィルタードライバーによって、特定のファイルをそのドライバーに特別なマークを付けるためにも使用されます。

-   プログラムは、再解析ポイントを設定すると、このデータと再解析タグを格納します。このタグは、格納されているデータを一意に識別します。 ファイルシステムは、再解析ポイントを使用してファイルを開くと、関連付けられているファイルシステムフィルターの検索を試みます。 ファイルシステムフィルターが見つかった場合、フィルターは再解析データによって指示されたファイルを処理します。 ファイルシステムフィルターが見つからない場合、ファイルオープン操作は失敗します。

## <a name="examples"></a><a name="BKMK_examples"></a>例
C:\ サーバーに関連付けられている再解析ポイントデータを取得するには、次のように入力します。

```
fsutil reparsepoint query c:\server
```

指定したファイルまたはディレクトリから再解析ポイントを削除するには、次の形式を使用します。

```
fsutil reparsepoint delete c:\server
```

## <a name="additional-references"></a>その他のリファレンス
- [コマンド ライン構文の記号](command-line-syntax-key.md)

[Fsutil](Fsutil.md)


