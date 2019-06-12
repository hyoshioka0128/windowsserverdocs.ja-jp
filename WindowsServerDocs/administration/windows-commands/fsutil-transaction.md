---
ms.assetid: f2eefaaf-2817-4ac7-abac-d2b65fa971dc
title: fsutil トランザクション
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: c225c99919a2558559b1ec7a47b61d716e199a73
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439001"
---
# <a name="fsutil-transaction"></a>fsutil トランザクション
>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7、Windows 2008、Windows Vista

NTFS のトランザクションを管理します。

このコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。

## <a name="syntax"></a>構文

```
fsutil transaction [commit] <GUID>
fsutil transaction [fileinfo] <Filename>
fsutil transaction [list]
fsutil transaction [query] [{Files|All}] <GUID>
fsutil transaction [rollback] <GUID>
```

### <a name="parameters"></a>パラメーター

| パラメーター  |                                                                                                                                                     説明                                                                                                                                                     |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   コミット (commit)   |                                                                                                                      成功した暗黙的または明示的な指定されたトランザクションの終了を示します。                                                                                                                      |
|   <GUID>   |                                                                                                                               トランザクションを表す GUID 値を指定します。                                                                                                                               |
|  fileinfo  |                                                                                                                              指定したファイルのトランザクション情報を表示します。                                                                                                                               |
| <Filename> |                                                                                                                                         完全なパスとファイル名を指定します。                                                                                                                                          |
|    list    |                                                                                                                                 現在実行中のトランザクションの一覧が表示されます。                                                                                                                                  |
|   query    | 指定したトランザクションの情報が表示されます。<br /><br />If **fsutil トランザクション クエリ ファイル**を指定すると、指定したトランザクションのみのファイルの情報が表示されます。<br />If **fsutil トランザクション クエリすべて**を指定すると、トランザクションのすべての情報が表示されます。 |
|  ロールバック  |                                                                                                                                最初に指定されたトランザクションをロールバックします。                                                                                                                                 |

### <a name="remarks"></a>注釈

-   トランザクション NTFS は、Windows Server 2008 で導入されました。

### <a name="BKMK_examples"></a>例
ファイル c:\test.txt のトランザクション情報を表示するには、次のように入力します。

```
fsutil transaction fileinfo c:\test.txt  
```

### <a name="additional-references"></a>その他の参照情報
[コマンド ライン構文の記号](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)

[トランザクション NTFS](https://go.microsoft.com/fwlink/?LinkID=165402)


