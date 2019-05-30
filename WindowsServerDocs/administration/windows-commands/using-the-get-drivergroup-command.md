---
title: Get DriverGroup コマンドを使用してください。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7cfe10c3-a63f-48e7-bef9-f6b474b4ddbe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7f82969e03b3474cf39afd2ae5c3ef2f9d4f8b5f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847153"
---
# <a name="using-the-get-drivergroup-command"></a>Get DriverGroup コマンドを使用してください。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サーバー上のドライバー グループについての情報を表示します。
## <a name="syntax"></a>構文
```
wdsutil /Get-DriverGroup /DriverGroup:<Group Name> [/Server:<Server name>]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/DriverGroup:<Group Name>|ドライバー グループの名前を指定します。|
|[/Server:<Server name>]|サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。  サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|
|[/Show: {行き着きます &#124;文字です。フィルターと #124 文字です。All}]|指定したグループ内のすべてのドライバー パッケージのメタデータを表示します。 **行き着きます** ドライバー グループのすべてのフィルターに関する情報を表示します。 **フィルター** すべてのドライバー パッケージのメタデータと、グループのフィルターが表示されます。|
## <a name="BKMK_examples"></a>例
ドライバー ファイルに関する情報を表示するには、次のように入力します。
```
wdsutil /Get-DriverGroup /DriverGroup:printerdrivers /Show:PackageMetaData
```
```
wdsutil /Get-DriverGroup /DriverGroup:printerdrivers /Server:MyWdsServer /Show:Filters
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[get AllDriverGroups コマンドを使用して](using-the-get-alldrivergroups-command.md)
