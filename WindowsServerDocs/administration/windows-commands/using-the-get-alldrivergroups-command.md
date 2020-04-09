---
title: get AllDriverGroups
description: サーバー上のすべてのドライバーグループに関する情報を表示する、get AllDriverGroups の Windows コマンドに関するトピック。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f245ba53-f150-41b1-8418-38dcf0410a05
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6112c38ec8e89effe5cdecaa99c6b75becd2e90d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80831365"
---
# <a name="get-alldrivergroups"></a>get AllDriverGroups

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サーバー上のすべてのドライバー グループに関する情報を表示します。

## <a name="syntax"></a>構文
```
wdsutil /Get-AllDriverGroups [/Server:<Server name>] [/Show:{PackageMetaData | Filters | All}]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|
|[/Show: {行き着きます & #124 文字です。フィルターと #124 文字です。All}]|指定したグループ内のすべてのドライバー パッケージのメタデータを表示します。 **行き着きます** ドライバー グループのすべてのフィルターに関する情報を表示します。 **フィルター** すべてのドライバー パッケージのメタデータと、グループのフィルターが表示されます。|
## <a name="examples"></a><a name=BKMK_examples></a>例
ドライバー ファイルに関する情報を表示するには、次のように入力します。
```
wdsutil /Get-AllDriverGroups /Server:MyWdsServer /Show:All
```
```
wdsutil /Get-AllDriverGroups [/Show:PackageMetaData]
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のポイント](command-line-syntax-key.md)
[get DriverGroup コマンドを使用して](using-the-get-drivergroup-command.md)
