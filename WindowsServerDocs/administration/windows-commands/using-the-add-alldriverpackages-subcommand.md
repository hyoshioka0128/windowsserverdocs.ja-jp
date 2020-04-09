---
title: 追加 AllDriverPackages サブコマンドを使用します。
description: Windows コマンドに関するトピックでは、フォルダーに格納されているすべてのドライバーパッケージをサーバーに追加します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ba6641c1-d7e9-43a9-9819-702dad5484ed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dc8252339fcae04517c2074c24bbfab44228b779
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80832265"
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
|  /FolderPath:\<フォルダーのパス >  |                      ドライバ パッケージの .inf ファイルを含むフォルダーへの完全パスを指定します。                      |
|   [/Server:\<サーバー名 >]   | サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。 |
|     [/アーキテクチャ: {x86      |                                                                 ia64                                                                  |
| [/Drivergroup:\<グループ名 >] |                             パッケージの追加先となるドライバー グループの名前を指定します。                             |

## <a name="examples"></a><a name=BKMK_examples></a>例

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