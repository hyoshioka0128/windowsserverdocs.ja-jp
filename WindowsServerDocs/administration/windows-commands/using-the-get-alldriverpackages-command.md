---
title: Get AllDriverPackages コマンドを使用してください。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9eb8fcb7-ef46-4c8d-9623-8969a3c8b8a4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7e531d9e175ba35aa092c1ef95ec5fe7d1eddff6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843653"
---
# <a name="using-the-get-alldriverpackages-command"></a>Get AllDriverPackages コマンドを使用してください。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定した検索条件に一致するサーバー上のすべてのドライバー パッケージについての情報を表示します。
## <a name="syntax"></a>構文
```
wdsutil /Get-AllDriverPackages [/Server:<Server name>] [/Show:{Drivers | Files | All}] [/Filtertype:<Filter type> /Operator:{Equal | NotEqual | GreaterOrEqual | LessOrEqual | Contains} /Value:<Value> [/Value:<Value> ...]]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|サーバーの名前。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|
|[/Show: {ドライバーおよび #124 文字です。ファイルと #124 文字です。All}]|パッケージ情報を表示することを示します。 場合 **/show** が指定されていない、既定では、パッケージ メタデータ ドライバーのみを返します。 **ドライバー** パッケージのドライバーの一覧が表示されます。 **ファイル** パッケージにファイルの一覧が表示されます。 **すべて** ドライバーやファイルが表示されます。|
|/Filtertype:<Filter type>|検索するドライバー パッケージの属性を指定します。 1 つのコマンドでは、複数の属性を指定できます。 指定する必要があります **に** と **/value** このオプションを使用します。<br /><br /><Filter type> 次のいずれかを指定できます。<br /><br />**PackageId**<br /><br />**PackageName**<br /><br />**PackageEnabled**<br /><br />**Packagedateadded**<br /><br />**PackageInfFilename**<br /><br />**PackageClass**<br /><br />**PackageProvider**<br /><br />**PackageArchitecture**<br /><br />**PackageLocale**<br /><br />**PackageSigned**<br /><br />**PackagedatePublished**<br /><br />**Packageversion**<br /><br />**Driverdescription**<br /><br />**DriverManufacturer**<br /><br />**DriverHardwareId**<br /><br />**DrivercompatibleId**<br /><br />**DriverExcludeId**<br /><br />**DriverGroupId**<br /><br />**DriverGroupName**|
|/演算子: {等号と #124 文字です。NotEqual &#124;文字です。GreaterOrEqual &#124;文字です。LessOrEqual &#124;文字です。含まれています|属性と値間のリレーションシップを指定します。 指定できます **Contains** 文字列の属性でのみです。 指定できます **GreaterOrEqual** と **LessOrEqual** 日、バージョン属性を持つのみです。|
|/値:<Value>|指定した検索する値を指定 <attribute>します。  1 つの複数の値を指定する **/Filtertype**します。 次の一覧では、各フィルターに指定できる属性について説明します。 これらの属性の詳細については、次を参照してください。[ドライバーとパッケージの属性](https://go.microsoft.com/fwlink/?LinkId=166895)(https://go.microsoft.com/fwlink/?LinkId=166895)します。<br /><br />-PackageId - は、有効な GUID を指定します。 例: {4d36e972-e325-11ce-bfc1-08002be10318} します。<br />-パッケージ名を指定する任意の文字列値。<br />-PackageEnabled - 指定 **はい** または **いいえ**します。<br />-Packagedateadded - は、次の形式で日付を指定します。YYYY DD MM<br />-Packageinffilename を指定する任意の文字列値。<br />-PackageClass - は、有効なクラス名またはクラス GUID を指定します。 例:**ディスク ドライブ**、 **Net**、または {4d36e972-e325-11ce-bfc1-08002be10318} します。<br />-Packageprovider を指定する任意の文字列値。<br />-PackageArchitecture - 指定 **x86**, 、**x64**, 、または **ia64**します。<br />-PackagLocale - は、有効な言語識別子を指定します。 例: **EN-US** または **ES-ES**します。<br />-PackageSigned - 指定 **はい** または **いいえ**します。<br />-Packagedatepublished - は、次の形式で日付を指定します。YYYY DD MM<br />-Packageversion を次の形式でバージョンを指定してください: します a.b.x.y。 次に、例を示します。6.1.0.0<br />-Driverdescription を指定する任意の文字列値。<br />-Drivermanufacturer を指定する任意の文字列値。<br />-DriverHardwareId - は、任意の文字列値を指定します。<br />--Drivercompatibleid は、任意の文字列値を指定します。<br />-Driverexcludeid を指定する任意の文字列値。<br />-Drivergroupid 有効な GUID を指定します。 例: {4d36e972-e325-11ce-bfc1-08002be10318} します。<br />-Drivergroupname を指定する任意の文字列値。|
## <a name="BKMK_examples"></a>例
情報を表示するには、次のいずれかを入力します。
```
wdsutil /Get-AllDriverPackages /Server:MyWdsServer /Show:All /Filtertype:DriverGroupName /Operator:Contains /Value:printer /Filtertype:PackageArchitecture /Operator:Equal /Value:x64 /Value:x86
```
```
wdsutil /Get-AllDriverPackages /Show:Drivers /Filtertype:Packagedateadded /Operator:GreaterOrEqual /Value:2008/01/01
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[get DriverPackage コマンドを使用して](using-the-get-driverpackage-command.md)
[get DriverPackageFile コマンドを使用して](using-the-get-driverpackagefile-command.md)
