---
title: 追加 AllDriverPackages サブコマンドを使用します。
description: フォルダーに格納されているすべてのドライバーパッケージをサーバーに追加する追加 AllDriverPackages のリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ba6641c1-d7e9-43a9-9819-702dad5484ed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a505175b1b2efc56c9be6d77384c71f8c1db7392
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85937258"
---
# <a name="add-alldriverpackages"></a>追加-AllDriverPackages

サーバーにフォルダーに格納されているすべてのドライバー パッケージを追加します。

## <a name="syntax"></a>構文

```
WDSUTIL /Add-AllDriverPackages /FolderPath:<Folder Path> [/Server:<Server name>] [/Architecture:{x86 | ia64 | x64}] [/DriverGroup:<Group Name>]
```

### <a name="parameters"></a>パラメーター

|          パラメーター           |                                                              説明                                                              |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
|  FolderPath\<Folder Path>  |                      ドライバ パッケージの .inf ファイルを含むフォルダーへの完全パスを指定します。                      |
|   [/Server:\<Server name>]   | サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。 |
|     [/アーキテクチャ: {x86      |                                                                 ia64                                                                  |
| [/DriverGroup:\<Group Name>] |                             パッケージの追加先となるドライバー グループの名前を指定します。                             |

## <a name="examples"></a>例

ドライバー パッケージを追加するには、次のいずれかを入力します。
```
WDSUTIL /verbose /Add-AllDriverPackages /FolderPath:C:\Temp\Drivers /Architecture:x86
```
```
WDSUTIL /Add-AllDriverPackages /FolderPath:C:\Temp\Drivers\Printers /DriverGroup:Printer Drivers
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

[追加-WdsDriverPackage](https://technet.microsoft.com/library/dn283440.aspx)