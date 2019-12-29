---
title: 追加 DriverGroupPackage コマンドを使用してください。
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7cd323ae-9049-448e-a460-6c7d6462d4c8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: eb443b6e6fdc71ccd3340552a23491ef7e61e0b2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363808"
---
# <a name="using-the-add-drivergrouppackage-command"></a>追加 DriverGroupPackage コマンドを使用してください。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ドライバーパッケージをドライバーグループに追加します。
## <a name="syntax"></a>構文
```
wdsutil /add-DriverGroupPackage /DriverGroup:<Group Name> [/Server:<Server Name>] {/DriverPackage:<Name> | /PackageId:<ID>}
```
## <a name="parameters"></a>パラメーター

|         パラメーター         |                                                                                                                                               説明                                                                                                                                               |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /Drivergroup: <Group Name> |                                                                                                                                 ドライバー グループの名前を指定します。                                                                                                                                 |
|   /Server: <Server name>   |                                                                                  サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。                                                                                  |
|   /Driverpackage: <Name>   |                                                                      グループに追加するドライバー パッケージの名前を指定します。 ドライバー パッケージを名前によって一意に識別できない場合は、このオプションを指定する必要があります。                                                                       |
|      /PackageId: <ID>      | パッケージの ID を指定します。 パッケージ ID を検索するには、パッケージがドライバー グループをクリックして (または **すべてのパッケージ** ノード)、パッケージを右クリックし、クリックして **プロパティ**します。 パッケージ ID が **[全般]** タブに表示されます。例: **{DD098D20-1850-4fc8-8E35-EA24A1BEFF5E}** 。 |

## <a name="BKMK_examples"></a>例
ドライバー パッケージを追加するには、次のいずれかを入力します。
```
wdsutil /add-DriverGroupPackage /DriverGroup:printerdrivers /PackageId:{4D36E972-E325-11CE-Bfc1-08002BE10318}
```
```
wdsutil /add-DriverGroupPackage /DriverGroup:printerdrivers /DriverPackage:XYZ
```
#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文のポイント](command-line-syntax-key.md)
[追加 DriverGroupPackages コマンドを使用して](using-the-add-drivergrouppackages-command.md)
[追加 DriverPackage コマンドを使用して](using-the-add-driverpackage-command.md)
[追加 AllDriverPackages サブコマンドを使用します。](using-the-add-alldriverpackages-subcommand.md)
