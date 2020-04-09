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
ms.openlocfilehash: aa6692dbb8af1ec832650971c6723c060fc2cd56
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844015"
---
# <a name="fsutil-transaction"></a>Fsutil トランザクション
>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7、Windows 2008、Windows Vista

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

#### <a name="parameters"></a>パラメーター

| パラメーター  |                                                                                                                                                     説明                                                                                                                                                     |
|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   コミット (commit)   |                                                                                                                      暗黙的または明示的に指定されたトランザクションが正常に終了したことを示します。                                                                                                                      |
|   <GUID>   |                                                                                                                               トランザクションを表す GUID 値を指定します。                                                                                                                               |
|  fileinfo  |                                                                                                                              指定されたファイルのトランザクション情報を表示します。                                                                                                                               |
| <Filename> |                                                                                                                                         完全なパスとファイル名を指定します。                                                                                                                                          |
|    リスト    |                                                                                                                                 現在実行されているトランザクションの一覧を表示します。                                                                                                                                  |
|   query    | 指定されたトランザクションの情報を表示します。<p>- **Fsutil transaction Query Files**が指定されている場合、ファイル情報は指定したトランザクションに対してのみ表示されます。<br />- **[Fsutil transaction Query All]** が指定されている場合、トランザクションのすべての情報が表示されます。 |
|  ロールバック  |                                                                                                                                指定されたトランザクションを先頭にロールバックします。                                                                                                                                 |

### <a name="remarks"></a>コメント

-   トランザクション NTFS は、Windows Server 2008 で導入されました。

### <a name="examples"></a><a name="BKMK_examples"></a>例
ファイル c:\test.txt のトランザクション情報を表示するには、次のように入力します。

```
fsutil transaction fileinfo c:\test.txt  
```

### <a name="additional-references"></a>その他の参照情報
- [コマンド ライン構文の記号](command-line-syntax-key.md)

[Fsutil](Fsutil.md)

[トランザクション NTFS](https://go.microsoft.com/fwlink/?LinkID=165402)


