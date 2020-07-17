---
title: 削除 DriverPackage
description: ドライバーパッケージをサーバーから削除する削除 DriverPackage のリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6b201e91-0d44-4e4a-8252-8b0235df1002
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c39f34d1556e6ad0f61f3f1cc3cf0aac36b18ee5
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933453"
---
# <a name="remove-driverpackage"></a>削除 DriverPackage

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サーバーからドライバー パッケージを削除します。

## <a name="syntax"></a>構文
```
wdsutil /remove-DriverPackage [/Server:<Server name>] {/DriverPackage:<Package Name> | /PackageId:<ID>}
```
### <a name="parameters"></a>パラメーター

|        パラメーター        |                                                                            説明                                                                             |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server:<Server name>] |              サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。              |
| [/DriverPackage:<Name>] |                                                        削除するドライバー パッケージの名前を指定します。                                                         |
|    [/パッケージ Id:<ID>]    | 削除するドライバー パッケージの Windows 展開サービス ID を指定します。 ドライバー パッケージを名前によって一意に識別できない場合は、ID を指定する必要があります。 |

## <a name="examples"></a>例
イメージに関する情報を表示するには、次のいずれかを入力します。
```
wdsutil /remove-DriverPackage /PackageId:{4D36E972-E325-11CE-Bfc1-08002BE10318}
```
```
wdsutil /remove-DriverPackage /Server:MyWdsServer /DriverPackage:MyDriverPackage
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のキー](command-line-syntax-key.md) 
[削除 DriverPackages コマンドを使用して](using-the-remove-driverpackages-command.md)ください。
