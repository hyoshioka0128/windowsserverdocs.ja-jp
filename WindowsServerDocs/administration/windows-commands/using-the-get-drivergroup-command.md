---
title: get DriverGroup
description: Windows コマンドに関するトピック。このトピックでは、サーバー上のドライバーグループに関する情報を表示します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7cfe10c3-a63f-48e7-bef9-f6b474b4ddbe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 60a0649e98a0af0cbbd12db9a07f97dade66344c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80831095"
---
# <a name="get-drivergroup"></a>get DriverGroup

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サーバー上のドライバー グループについての情報を表示します。

## <a name="syntax"></a>構文
```
wdsutil /Get-DriverGroup /DriverGroup:<Group Name> [/Server:<Server name>]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/Drivergroup:<Group Name>|ドライバー グループの名前を指定します。|
|[/Server:<Server name>]|サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。  サーバー名が指定されていない場合は、ローカルサーバーが使用されます。|
|[/Show: {行き着きます & #124 文字です。フィルターと #124 文字です。All}]|指定したグループ内のすべてのドライバー パッケージのメタデータを表示します。 **行き着きます** ドライバー グループのすべてのフィルターに関する情報を表示します。 **フィルター** すべてのドライバー パッケージのメタデータと、グループのフィルターが表示されます。|
## <a name="examples"></a><a name=BKMK_examples></a>例
ドライバー ファイルに関する情報を表示するには、次のように入力します。
```
wdsutil /Get-DriverGroup /DriverGroup:printerdrivers /Show:PackageMetaData
```
```
wdsutil /Get-DriverGroup /DriverGroup:printerdrivers /Server:MyWdsServer /Show:Filters
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のポイント](command-line-syntax-key.md)
[get AllDriverGroups コマンドを使用して](using-the-get-alldrivergroups-command.md)
