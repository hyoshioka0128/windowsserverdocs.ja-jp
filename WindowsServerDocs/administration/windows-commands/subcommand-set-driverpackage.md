---
title: サブコマンド セット DriverPackage
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 11804bb6-ca29-4461-8c63-5131748cd742
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 24acd672184b8df235e8de843961ac4adb2bd412
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441132"
---
# <a name="subcommand-set-driverpackage"></a>サブコマンド: セット DriverPackage



名前を変更や有効または、サーバー上のドライバー パッケージを無効にします。

## <a name="syntax"></a>構文

```
WDSUTIL /Set-DriverPackage [/Server:<Server name>] {/DriverPackage:<Name> | /PackageId:<ID>} [/Name:<New Name>] [/Enabled:{Yes | No}
```

## <a name="parameters"></a>パラメーター

|        パラメーター         |                                                                                                                                                                                                               説明                                                                                                                                                                                                                |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server:\<サーバー名 >] |                                                                                                                                                 サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。                                                                                                                                                 |
| [/DriverPackage:\<Name>] |                                                                                                                                                                                       変更するドライバー パッケージの現在の名前を指定します。                                                                                                                                                                                        |
|    [/PackageId:\<ID>]    | ドライバー パッケージの Windows 展開サービス ID を指定します。 ドライバー パッケージを名前によって一意に識別できない場合は、このオプションを指定する必要があります。 パッケージのこの ID を検索するには、パッケージがドライバー グループをクリックして (または**すべてのパッケージ**ノード)、パッケージを右クリックし、クリックして**プロパティ**します。 [パッケージ ID が表示されて、 **全般** ] タブをクリックします。例: {dd098d20-1850-4fc8-8e35-ea24a1beff5e} します。 |
|   [/Name:\<新しい名 >]    |                                                                                                                                                                                              ドライバー パッケージの新しい名前を指定します。                                                                                                                                                                                              |
|      [有効になっている/: {[はい]      |                                                                                                                                                                                                                   No}                                                                                                                                                                                                                    |

## <a name="BKMK_examples"></a>例

パッケージに関する設定を変更するには、次のいずれかを入力します。
```
WDSUTIL /Set-DriverPackage /PackageId:{4D36E972-E325-11CE-BFC1-08002BE10318} /Name:MyDriverPackage
```
```
WDSUTIL /Set-DriverPackage /DriverPackage:MyDriverPackage /Name:NewName /Enabled:Yes
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)