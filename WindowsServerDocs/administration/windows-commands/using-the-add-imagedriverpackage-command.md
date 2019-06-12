---
title: 追加 ImageDriverPackage コマンドを使用してください。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6c2a4833-6427-47f8-9ffb-20b3786cb406
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 38d6c032f347f9945701f17b9289f3e3ff474031
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440625"
---
# <a name="using-the-add-imagedriverpackage-command"></a>追加 ImageDriverPackage コマンドを使用してください。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サーバー上の既存のブート イメージにドライバー ストアにドライバー パッケージを追加します。 イメージのバージョンは、Windows 7 または Windows Server 2008 R2 をする必要がありますまたはそれ以降。
## <a name="syntax"></a>構文
```
wdsutil /add-ImageDriverPackage [/Server:<Server name>media:<Image namemediatype:Boot /Architecture:{x86 | ia64 | x64} 
```
```
[/Filename:<File name>] {/DriverPackage:<Package Name> | /PackageId:<ID>}
```
## <a name="parameters"></a>パラメーター

|                 パラメーター                  |                                                                                                                                                                                                            説明                                                                                                                                                                                                             |
|--------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           [/Server:<Server name>           |                                                                                                                                               サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。                                                                                                                                                |
|             メディア:<Image name>             |                                                                                                                                                                                       ドライバーを追加するイメージの名前を指定します。                                                                                                                                                                                        |
|               mediatype:Boot               |                                                                                                                                                                ドライバーを追加する画像の種類を指定します。 ドライバー パッケージは、ブート イメージにのみ追加できます。                                                                                                                                                                 |
| /アーキテクチャ: {x86 &#124; ia64 &#124; x64} |                                                                                                       ブート イメージのアーキテクチャを指定します。 さまざまなアーキテクチャでブート イメージで同じイメージの名前を指定することも可能であるために、確実に適切なイメージが使用されるアーキテクチャを指定してください。                                                                                                        |
|           /ファイル名:<File name>]           |                                                                                                                                                        ファイルの名前を指定します。 イメージは、名前によって一意に識別できない、ファイル名を指定してください。                                                                                                                                                        |
|           [/DriverPackage:<Name>           |                                                                                                                                                                                   イメージに追加するドライバー パッケージの名前を指定します。                                                                                                                                                                                    |
|             [/パッケージ Id:<ID>]              | ドライバー パッケージの Windows 展開サービス ID を指定します。 ドライバー パッケージを名前によって一意に識別できない場合は、このオプションを指定する必要があります。 パッケージ ID を検索するには、パッケージがドライバー グループをクリックして (または **すべてのパッケージ** ノード)、パッケージを右クリックし、クリックして **プロパティ**します。 [パッケージ ID が表示されて、 **全般** ] タブをクリックします。例: {dd098d20-1850-4fc8-8e35-ea24a1beff5e} します。 |

## <a name="BKMK_examples"></a>例
ブート イメージにドライバー パッケージを追加するには、次のいずれかを入力します。
```
wdsutil /add-ImageDriverPackagmedia:"WinPE Boot Imagemediatype:Boot /Architecture:x86 /DriverPackage:XYZ
```
```
wdsutil /verbose /add-ImageDriverPackagmedia:"WinPE Boot Image" /Server:MyWDSServemediatype:Boot /Architecture:x64 /PackageId:{4D36E972-E325-11CE-Bfc1-08002BE10318}
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[追加 ImageDriverPackages コマンドを使用して](using-the-add-imagedriverpackages-command.md)
