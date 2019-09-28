---
ms.assetid: f2eefaaf-2817-4ac7-abac-d2b65fa971dc
title: Fsutil トランザクション
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 286660baad699e21abe751a9cb956b1ac7613e80
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376860"
---
# <a name="fsutil-transaction"></a>Fsutil トランザクション
>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7、Windows 2008、Windows Vista

NTFS トランザクションを管理します。

このコマンドの使用方法の例については、「[例](#BKMK_examples)」を参照してください。

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
|   コミット (commit)   |                                                                                                                      暗黙的または明示的に指定されたトランザクションが正常に終了したことを示します。                                                                                                                      |
|   <GUID>   |                                                                                                                               トランザクションを表す GUID 値を指定します。                                                                                                                               |
|  fileinfo  |                                                                                                                              指定されたファイルのトランザクション情報を表示します。                                                                                                                               |
| <Filename> |                                                                                                                                         完全なパスとファイル名を指定します。                                                                                                                                          |
|    list    |                                                                                                                                 現在実行されているトランザクションの一覧を表示します。                                                                                                                                  |
|   クエリ (query)    | 指定されたトランザクションの情報を表示します。<br /><br />- **Fsutil transaction Query Files**が指定されている場合、ファイル情報は指定したトランザクションに対してのみ表示されます。<br />- **[Fsutil transaction Query All]** が指定されている場合、トランザクションのすべての情報が表示されます。 |
|  ロールバック  |                                                                                                                                指定されたトランザクションを先頭にロールバックします。                                                                                                                                 |

### <a name="remarks"></a>コメント

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


