---
title: サブコマンド セット DriverGroup
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e4ba9b1c-8c52-4fd5-969b-f7905611b364
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6e645e16a3d78dd91bad98fedbb04896025b0eaf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852703"
---
# <a name="subcommand-set-drivergroup"></a>サブコマンド: セット DriverGroup

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サーバー上の既存のドライバー グループのプロパティを設定します。
## <a name="syntax"></a>構文
```
wdsutil /Set-DriverGroup /DriverGroup:<Group Name> [/Server:<Server Name>] [/Name:<New Group Name>] [/Enabled:{Yes | No}] [/Applicability:{Matched | All}]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/DriverGroup:<Group Name>|ドライバー グループの名前を指定します。|
|[/Server:<Server name>]|サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|
|[/Name:<New Group Name>]|ドライバー グループの新しい名前を指定します。|
|[有効になっている/: {[はい] &#124; No}|有効または、ドライバー グループを無効にします。|
|[/適用性: {一致&#124;すべて}]|フィルター条件が満たされた場合、インストールするパッケージを指定します。 **一致する**クライアントのハードウェアに一致するドライバー パッケージのみをインストールすることを意味します。 **すべて**手段は、ハードウェアに関係なくクライアントにすべてのパッケージをインストールします。|
## <a name="BKMK_examples"></a>例
ドライバー グループのプロパティを設定するには、次のいずれかを入力します。
```
wdsutil /Set-DriverGroup /DriverGroup:printerdrivers /Enabled:Yes
```
```
wdsutil /Set-DriverGroup /DriverGroup:printerdrivers /Name:colorprinterdrivers /Applicability:All
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[サブコマンド: セット DriverGroupFilter](subcommand-set-drivergroupfilter.md)
