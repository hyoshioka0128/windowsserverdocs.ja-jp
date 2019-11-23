---
title: サブコマンド set DriverGroup
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 751985cffea32b5129909576f0631cce83adc9a2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370836"
---
# <a name="subcommand-set-drivergroup"></a>サブコマンド: セット DriverGroup

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サーバー上の既存のドライバー グループのプロパティを設定します。
## <a name="syntax"></a>構文
```
wdsutil /Set-DriverGroup /DriverGroup:<Group Name> [/Server:<Server Name>] [/Name:<New Group Name>] [/Enabled:{Yes | No}] [/Applicability:{Matched | All}]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/Drivergroup:<Group Name>|ドライバー グループの名前を指定します。|
|[/Server:<Server name>]|サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|
|[/Name:<New Group Name>]|ドライバーグループの新しい名前を指定します。|
|[/有効: {Yes &#124; No}]|ドライバーグループを有効または無効にします。|
|[/適用性: { &#124;一致したすべて}]|フィルター条件が満たされた場合にインストールするパッケージを指定します。 **一致**とは、クライアントのハードウェアに一致するドライバーパッケージのみをインストールすることを意味します。 **すべて**は、ハードウェアに関係なく、すべてのパッケージをクライアントにインストールすることを意味します。|
## <a name="BKMK_examples"></a>例
ドライバーグループのプロパティを設定するには、次のいずれかを入力します。
```
wdsutil /Set-DriverGroup /DriverGroup:printerdrivers /Enabled:Yes
```
```
wdsutil /Set-DriverGroup /DriverGroup:printerdrivers /Name:colorprinterdrivers /Applicability:All
```
#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文のキー](command-line-syntax-key.md)
[サブコマンド: Set drivergroupfilter](subcommand-set-drivergroupfilter.md)
