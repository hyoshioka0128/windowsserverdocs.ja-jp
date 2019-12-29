---
title: サブコマンドの設定-DriverPackage
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 65751cf6e03baa87c7734b318a26111652bee0a1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370821"
---
# <a name="subcommand-set-driverpackage"></a>サブコマンド: セット DriverPackage



サーバー上のドライバーパッケージの名前を変更するか、有効または無効にします。

## <a name="syntax"></a>構文

```
WDSUTIL /Set-DriverPackage [/Server:<Server name>] {/DriverPackage:<Name> | /PackageId:<ID>} [/Name:<New Name>] [/Enabled:{Yes | No}
```

## <a name="parameters"></a>パラメーター

|        パラメーター         |                                                                                                                                                                                                               説明                                                                                                                                                                                                                |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server: \<Server name >] |                                                                                                                                                 サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。                                                                                                                                                 |
| [/Driverpackage: \<Name >] |                                                                                                                                                                                       変更するドライバーパッケージの現在の名前を指定します。                                                                                                                                                                                        |
|    [/PackageId: \<ID >]    | ドライバーパッケージの Windows 展開サービス ID を指定します。 ドライバー パッケージを名前によって一意に識別できない場合は、このオプションを指定する必要があります。 パッケージのこの ID を検索するには、パッケージが含まれているドライバーグループ (または **[すべてのパッケージ]** ノード) をクリックし、パッケージを右クリックして、 **[プロパティ]** をクリックします。 [パッケージ ID が表示されて、 **全般** ] タブをクリックします。例: {DD098D20-1850-4FC8-8E35-EA24A1BEFF5E}。 |
|   [/Name: \<New Name >]    |                                                                                                                                                                                              ドライバーパッケージの新しい名前を指定します。                                                                                                                                                                                              |
|      [/有効: {はい]      |                                                                                                                                                                                                                   番号                                                                                                                                                                                                                    |

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