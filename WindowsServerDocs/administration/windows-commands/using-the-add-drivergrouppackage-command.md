---
title: 追加 DriverGroupPackage
description: ドライバーパッケージをドライバーグループに追加する追加 DriverGroupPackage のリファレンス記事です。
ms.topic: article
ms.assetid: 7cd323ae-9049-448e-a460-6c7d6462d4c8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1aedf8ee37feb6a0ee9c26f917aad5f93b9dd91e
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87879354"
---
# <a name="add-drivergrouppackage"></a>追加 DriverGroupPackage

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ドライバー パッケージをドライバー グループに追加します。

## <a name="syntax"></a>構文
```
wdsutil /add-DriverGroupPackage /DriverGroup:<Group Name> [/Server:<Server Name>] {/DriverPackage:<Name> | /PackageId:<ID>}
```
### <a name="parameters"></a>パラメーター

|         パラメーター         |                                                                                                                                               説明                                                                                                                                               |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| DriverGroup<Group Name> |                                                                                                                                 ドライバー グループの名前を指定します。                                                                                                                                 |
|   Server<Server name>   |                                                                                  サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。                                                                                  |
|   DriverPackage<Name>   |                                                                      グループに追加するドライバー パッケージの名前を指定します。 ドライバー パッケージを名前によって一意に識別できない場合は、このオプションを指定する必要があります。                                                                       |
|      PackageId<ID>      | パッケージの ID を指定します。 パッケージ ID を検索するには、パッケージがドライバー グループをクリックして (または **すべてのパッケージ** ノード)、パッケージを右クリックし、[クリックして **プロパティ**します。 パッケージ ID が [**全般**] タブに表示されます。例: **{DD098D20-1850-4fc8-8E35-EA24A1BEFF5E}**。 |

## <a name="examples"></a>例
ドライバー パッケージを追加するには、次のいずれかを入力します。
```
wdsutil /add-DriverGroupPackage /DriverGroup:printerdrivers /PackageId:{4D36E972-E325-11CE-Bfc1-08002BE10318}
```
```
wdsutil /add-DriverGroupPackage /DriverGroup:printerdrivers /DriverPackage:XYZ
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のキー](command-line-syntax-key.md) 
[追加 DriverGroupPackages コマンド](using-the-add-drivergrouppackages-command.md) 
 を使用してください。[追加 DriverPackage コマンド](using-the-add-driverpackage-command.md) 
 を使用してください。[Add AllDriverPackages サブコマンドを使用する](using-the-add-alldriverpackages-subcommand.md)
