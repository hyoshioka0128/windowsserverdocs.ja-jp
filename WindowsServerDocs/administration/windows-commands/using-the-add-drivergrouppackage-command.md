---
title: 追加 DriverGroupPackage コマンドを使用してください。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: b32d72a1317683e4c1bbeb2d6101d1315b69148e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862643"
---
# <a name="using-the-add-drivergrouppackage-command"></a>追加 DriverGroupPackage コマンドを使用してください。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ドライバー パッケージをドライバー グループに追加します。
## <a name="syntax"></a>構文
```
wdsutil /add-DriverGroupPackage /DriverGroup:<Group Name> [/Server:<Server Name>] {/DriverPackage:<Name> | /PackageId:<ID>}
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/DriverGroup:<Group Name>|ドライバー グループの名前を指定します。|
|/Server:<Server name>|サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|
|/DriverPackage:<Name>|グループに追加するドライバー パッケージの名前を指定します。 ドライバー パッケージを名前によって一意に識別できない場合は、このオプションを指定する必要があります。|
|/PackageId:<ID>|パッケージの ID を指定します。 パッケージ ID を検索するには、パッケージがドライバー グループをクリックして (または **すべてのパッケージ** ノード)、パッケージを右クリックし、クリックして **プロパティ**します。 パッケージ ID が表示されて、**全般**] タブの [例: **{dd098d20-1850-4fc8-8e35-ea24a1beff5e}** します。|
## <a name="BKMK_examples"></a>例
ドライバー パッケージを追加するには、次のいずれかを入力します。
```
wdsutil /add-DriverGroupPackage /DriverGroup:printerdrivers /PackageId:{4D36E972-E325-11CE-Bfc1-08002BE10318}
```
```
wdsutil /add-DriverGroupPackage /DriverGroup:printerdrivers /DriverPackage:XYZ
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[追加 DriverGroupPackages コマンドを使用して](using-the-add-drivergrouppackages-command.md)
[追加 DriverPackage コマンドを使用して](using-the-add-driverpackage-command.md)
[追加 AllDriverPackages サブコマンドを使用します。](using-the-add-alldriverpackages-subcommand.md)
