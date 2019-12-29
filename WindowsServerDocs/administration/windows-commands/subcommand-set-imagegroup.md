---
title: サブコマンドセット-ImageGroup
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d86946a-e261-4d41-8b0c-1ab0ba2e3430
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 10023e493ae4db51783b7401c12bc1605145b86c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370793"
---
# <a name="subcommand-set-imagegroup"></a>サブコマンド: セット ImageGroup

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

イメージグループの属性を変更します。
## <a name="syntax"></a>構文
```
wdsutil [Options] /Set-ImageGroumediaGroup:<Image group name> [/Server:<Server name>] [/Name:<New image group name>] [/Security:<SDDL>]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
mediaGroup: <Image group name>|イメージグループの名前を指定します。|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 指定しない場合は、ローカルサーバーが使用されます。|
|[/Name:<New image group name>]|イメージグループの新しい名前を指定します。|
|[セキュリティ: <SDDL>]|セキュリティ記述子定義言語 (SDDL) 形式で、イメージグループの新しいセキュリティ記述子を指定します。|
## <a name="BKMK_examples"></a>例
イメージグループの名前を設定するには、次のように入力します。
```
wdsutil /Set-ImageGroumediaGroup:ImageGroup1 /Name:"New Image Group Name"
```
イメージグループのさまざまな設定を指定するには、次のように入力します。
```
wdsutil /verbose /Set-ImageGroumediaGroup:ImageGroup1 /Server:MyWDSServer /Name:"New Image Group Name" 
/Security:"O:BAG:S-1-5-21-2176941838-3499754553-4071289181-513 D:AI(A;ID;FA;;;SY)(A;OICIIOID;GA;;;SY)(A;ID;FA;;;BA)(A;OICIIOID;GA;;;BA) (A;ID;0x1200a9;;;AU)(A;OICIIOID;GXGR;;;AU)"
```
#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文のキー](command-line-syntax-key.md)
[追加 imagegroup コマンド](using-the-add-imagegroup-command.md)を使用して 
 @no__t Get[allimagegroups コマンド](using-the-get-allimagegroups-command.md)を使用して[get imagegroup コマンド](using-the-get-imagegroup-command.md)を使用して、[削除 imagegroup](using-the-remove-imagegroup-command.md)コマンドを使用して 

