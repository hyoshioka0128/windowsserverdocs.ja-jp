---
title: 追加 DriverGroupPackages コマンドを使用してください。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 29022f53-ce14-4b2d-a81a-679c18e022b2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ad0f8c7ed202f0d6fccc11307b17b742c70c3e49
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842793"
---
# <a name="using-the-add-drivergrouppackages-command"></a>追加 DriverGroupPackages コマンドを使用してください。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。
## <a name="syntax"></a>構文
```
wdsutil /add-DriverGroupPackages /DriverGroup:<Group Name> [/Server:<Server Name>] /Filtertype:<Filter type> /Operator:{Equal | NotEqual | GreaterOrEqual | LessOrEqual | Contains} /Value:<Value> [/Value:<Value>
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/DriverGroup:<Group Name>|ドライバー グループの名前を指定します。|
|/Server:<Server name>|サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|
|/Filtertype:<Filter type>|検索するドライバー パッケージの属性を指定します。 1 つのコマンドでは、複数の属性を指定できます。 このオプションを使用してもに、/Value を指定する必要があります。<br /><br /><Filter type> 次のいずれかを指定できます。<br /><br />**PackageId**<br /><br />**PackageName**<br /><br />**PackageEnabled**<br /><br />**Packagedateadded**<br /><br />**PackageInfFilename**<br /><br />**PackageClass**<br /><br />**PackageProvider**<br /><br />**PackageArchitecture**<br /><br />**PackageLocale**<br /><br />**PackageSigned**<br /><br />**PackagedatePublished**<br /><br />**Packageversion**<br /><br />**Driverdescription**<br /><br />**DriverManufacturer**<br /><br />**DriverHardwareId**<br /><br />**DrivercompatibleId**<br /><br />**DriverExcludeId**<br /><br />**DriverGroupId**<br /><br />**DriverGroupName**|
|/演算子: {等号と #124 文字です。NotEqual &#124 文字です。GreaterOrEqual &#124 文字です。LessOrEqual &#124 文字です。含まれています|属性と値間のリレーションシップを指定します。 だけを指定できます **Contains** 文字列の属性を持つ。 だけを指定できます **等しい**, 、**NotEqual**, 、**GreaterOrEqual** と **LessOrEqual** 日、バージョン属性を持つ。|
|/値:<Value>|対応するクライアントの値を指定します **/Filtertype**します。 1 つの複数の値を指定する **/Filtertype**します。 次の一覧では、各フィルターに指定できる値について説明します。 これらの値の詳細については、次を参照してください。[ドライバーとパッケージの属性](https://go.microsoft.com/fwlink/?LinkId=166895)(https://go.microsoft.com/fwlink/?LinkId=166895)します。<br /><br />-PackageId - は、有効な GUID を指定します。 例: {4d36e972-e325-11ce-bfc1-08002be10318} します。<br />-パッケージ名を指定する任意の文字列値。<br />-PackageEnabled - 指定 **はい** または **いいえ**します。<br />-Packagedateadded - は、次の形式で日付を指定します。YYYY DD MM<br />-Packageinffilename を指定する任意の文字列値。<br />-PackageClass - は、有効なクラス名またはクラス GUID を指定します。 例:**ディスク ドライブ**、 **Net**、または {4d36e972-e325-11ce-bfc1-08002be10318} します。<br />-Packageprovider を指定する任意の文字列値。<br />-PackageArchitecture - 指定 **x86**, 、**x64**, 、または **ia64**します。<br />-PackageLoale - は、有効な言語識別子を指定します。 例: **EN-US** または **ES-ES**します。<br />-PackageSigned - 指定 **はい** または **いいえ**します。<br />-Packagedatepublished - は、次の形式で日付を指定します。YYYY DD MM<br />-Packageversion - は、次の形式でバージョンを指定: します a.b.x.y. 次に、例を示します。6.1.0.0<br />-Driverdescription を指定する任意の文字列値。<br />-Drivermanufacturer を指定する任意の文字列値。<br />-DriverHardwareId - は、任意の文字列値を指定します。<br />--Drivercompatibleid は、任意の文字列値を指定します。<br />-DriverExcludeId - は、任意の文字列値を指定します。<br />-DriverGroupId - は、有効な GUID を指定します。 例: {4d36e972-e325-11ce-bfc1-08002be10318} します。<br />-Drivergroupname を指定する任意の文字列値。|
## <a name="BKMK_examples"></a>例
ドライバー パッケージを追加するには、次のいずれかを入力します。
```
wdsutil /verbose /add-DriverGroupPackages /DriverGroup:printerdrivers /Filtertype:PackageClass /Operator:Equal /Value:printer /Filtertype:DriverManufacturer /Operator:NotEqual /Value:Name1 /Value:Name2
```
```
wdsutil /verbose /add-DriverGroupPackages /DriverGroup:DisplayDriversX86 /Filtertype:PackageClass /Operator:Equal /Value:Display /Filtertype:PackageArchitecture /Operator:Equal /Value:x86 /Filtertype:Packagedateadded /Operator:LessOrEqual /Value:2008/01/01
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[追加 DriverGroupPackage コマンドを使用して](using-the-add-drivergrouppackage-command.md)
[追加 DriverPackage コマンドを使用して](using-the-add-driverpackage-command.md)
[追加 AllDriverPackages サブコマンドを使用します。](using-the-add-alldriverpackages-subcommand.md)
