---
title: 削除 DriverPackages コマンドを使用してください。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a527084b-305e-4d3d-95c3-4f5a5ea0637b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 166602bcb1203f0ecb870ed04888ca0051f16827
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872483"
---
# <a name="using-the-remove-driverpackages-command"></a>削除 DriverPackages コマンドを使用してください。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サーバーからドライバー パッケージを削除します。
## <a name="syntax"></a>構文
```
wdsutil /remove-DriverPackages [/Server:<Server name>] /Filtertype:<Filter type> /Operator:{Equal | NotEqual | GreaterOrEqual | LessOrEqual | Contains} /Value:<Value> [/Value:<Value> ...]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|
|/Filtertype:<Filter type>|検索するドライバー パッケージの属性を指定します。 1 つのコマンドでは、複数の属性を指定できます。 指定する必要があります **に** と **/value** このオプションを使用します。<br /><br /><Filter type> 次のいずれかを指定できます。<br /><br />**PackageId**<br /><br />**PackageName**<br /><br />**PackageEnabled**<br /><br />**Packagedateadded**<br /><br />**PackageInfFilename**<br /><br />**PackageClass**<br /><br />**PackageProvider**<br /><br />**PackageArchitecture**<br /><br />**PackageLocale**<br /><br />**PackageSigned**<br /><br />**PackagedatePublished**<br /><br />**Packageversion**<br /><br />**Driverdescription**<br /><br />**DriverManufacturer**<br /><br />**DriverHardwareId**<br /><br />**DrivercompatibleId**<br /><br />**DriverExcludeId**<br /><br />**DriverGroupId**<br /><br />**DriverGroupName**|
|/演算子: {等号と &#124; 文字です。NotEqual &#124;文字です。GreaterOrEqual &#124;文字です。LessOrEqual &#124;文字です。含まれています|属性と値間のリレーションシップを指定します。 だけを指定できます **Contains** 文字列の属性を持つ。 だけを指定できます **GreaterOrEqual** と **LessOrEqual** 日、バージョン属性を持つ。|
|/値:<Value>|指定した検索する値を指定 <attribute>します。 1 つの複数の値を指定する **/Filtertype**します。 次の一覧では、各フィルターに指定できる属性について説明します。 これらの属性の詳細については、次を参照してください。[ドライバーとパッケージの属性](https://go.microsoft.com/fwlink/?LinkId=166895)(https://go.microsoft.com/fwlink/?LinkId=166895)します。<br /><br />-PackageId - は、有効な GUID を指定します。 例: {4d36e972-e325-11ce-bfc1-08002be10318} します。<br />-パッケージ名を指定する任意の文字列値。<br />-PackageEnabled - 指定 **はい** または **いいえ**します。<br />-Packagedateadded - は、次の形式で日付を指定します。YYYY DD MM<br />-Packageinffilename を指定する任意の文字列値。<br />-PackageClass - は、有効なクラス名またはクラス GUID を指定します。 次に、例を示します。**ディスク ドライブ**、 **Net**、または {4d36e972-e325-11ce-bfc1-08002be10318} します。<br />-Packageprovider を指定する任意の文字列値。<br />-PackageArchitecture - 指定 **x86**, 、**x64**, 、または **ia64**します。<br />-PckageLocale - は、有効な言語識別子を指定します。 例: **EN-US** または **ES-ES**します。<br />-PackageSigned - 指定 **はい** または **いいえ**します。<br />-Packagedatepublished - は、次の形式で日付を指定します。YYYY DD MM<br />-Packageversion - は、次の形式でバージョンを指定: します a.b.x.y. 次に、例を示します。6.1.0.0<br />-Driverdescription を指定する任意の文字列値。<br />-Drivermanufacturer を指定する任意の文字列値。<br />-DriverHardwareId - は、任意の文字列値を指定します。<br />--Drivercompatibleid は、任意の文字列値を指定します。<br />-DriverExcludeId - は、任意の文字列値を指定します。<br />-DriverGroupId - は、有効な GUID を指定します。 例: {4d36e972-e325-11ce-bfc1-08002be10318} します。<br />-Drivergroupname を指定する任意の文字列値。|
## <a name="BKMK_examples"></a>例
パッケージを削除するには、次のいずれかを入力します。
```
wdsutil /verbose /remove-DriverPackages /Server:MyWdsServer
/Filtertype:PackageProvider /Operator:Equal /Value:Name1 /Value:Name2
```
```
wdsutil /remove-DriverPackages /Filtertype:PackageArchitecture /Operator:Equal
/Value:x86 /Value:x64 /Filtertype:PackageEnabled /Operator:Equal /Value:No
```
```
wdsutil /verbose /remove-DriverPackages /Server:MyWdsServer
/Filtertype:Packagedateadded /Operator:LessOrEqual /Value:2008/01/01
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[削除 DriverPackage コマンドを使用して](using-the-remove-driverpackage-command.md)
