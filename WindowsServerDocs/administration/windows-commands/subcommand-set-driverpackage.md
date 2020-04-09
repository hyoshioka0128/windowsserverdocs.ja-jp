---
title: サブコマンドの設定-DriverPackage
description: コマンドの Windows コマンドに関するトピックでは、サーバー上のドライバーパッケージの名前を変更したり、有効または無効にしたりします。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 11804bb6-ca29-4461-8c63-5131748cd742
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 68d282b3338e67a33a55481658f55db69930b10e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834022"
---
# <a name="subcommand-set-driverpackage"></a>サブコマンド: セット DriverPackage

サーバー上のドライバーパッケージの名前を変更するか、有効または無効にします。

## <a name="syntax"></a>構文

```
WDSUTIL /Set-DriverPackage [/Server:<Server name>] {/DriverPackage:<Name> | /PackageId:<ID>} [/Name:<New Name>] [/Enabled:{Yes | No}
```

### <a name="parameters"></a>パラメーター

|        パラメーター         |                                                                                                                                                                                                               説明                                                                                                                                                                                                                |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server:\<サーバー名 >] |                                                                                                                                                 サーバーの名前を指定します。 これには、NetBIOS 名または FQDN を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。                                                                                                                                                 |
| [/Driverpackage:\<名 >] |                                                                                                                                                                                       変更するドライバーパッケージの現在の名前を指定します。                                                                                                                                                                                        |
|    [/PackageId:\<ID >]    | ドライバーパッケージの Windows 展開サービス ID を指定します。 ドライバー パッケージを名前によって一意に識別できない場合は、このオプションを指定する必要があります。 パッケージのこの ID を検索するには、パッケージが含まれているドライバーグループ (または **[すべてのパッケージ]** ノード) をクリックし、パッケージを右クリックして、 **[プロパティ]** をクリックします。 **[全般]** タブにパッケージ ID が表示されます。例: {DD098D20-1850-4FC8-8E35-EA24A1BEFF5E}。 |
|   [/Name:\<新しい名前 >]    |                                                                                                                                                                                              ドライバーパッケージの新しい名前を指定します。                                                                                                                                                                                              |
|      [/有効: {はい]      |                                                                                                                                                                                                                   番号                                                                                                                                                                                                                    |

## <a name="examples"></a><a name=BKMK_examples></a>例

パッケージに関する設定を変更するには、次のいずれかを入力します。
```
WDSUTIL /Set-DriverPackage /PackageId:{4D36E972-E325-11CE-BFC1-08002BE10318} /Name:MyDriverPackage
```
```
WDSUTIL /Set-DriverPackage /DriverPackage:MyDriverPackage /Name:NewName /Enabled:Yes
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)