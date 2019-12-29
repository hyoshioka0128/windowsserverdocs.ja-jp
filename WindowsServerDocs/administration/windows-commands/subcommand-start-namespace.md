---
title: サブコマンドの開始-名前空間
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2dd1c11e-6ab7-4129-9e3a-3f80e0ba59c0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 55fe4a6136fe4f8e886dc62fff746a1e5ff1898f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370751"
---
# <a name="subcommand-start-namespace"></a>サブコマンド: 開始-名前空間

> 適用対象: windows server (半期チャネル)、Windows server 2016、Windows server 2012 R2、Windows Server 2012 は、スケジュールされたキャストの名前空間を開始します。
> ## <a name="syntax"></a>構文
> ```
> wdsutil /start-Namespace /Namespace:<Namespace name> [/Server:<Server name>]
> ```
> ## <a name="parameters"></a>パラメーター
> 
> |          パラメーター          |                                                                                                                                                                                             説明                                                                                                                                                                                             |
> |-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
> | /Namespace:<Namespace name> | 名前空間の名前を指定します。 これは、フレンドリ名ではない、一意である必要があることに注意してください。<br /><br />-   **展開サーバー**: 名前空間名の構文は/NAMSPACE: WDS:<Image group>/<Image name>/<Index>です。 例: **WDS:ImageGroup1/install.wim/1**<br />-   **トランスポートサーバー**: この名前は、サーバー上で作成されたときに名前空間に指定された名前と一致する必要があります。 |
> |   [/Server:<Server name>]   |                                                                                                           サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。                                                                                                           |
> 
> ## <a name="BKMK_examples"></a>例
> 名前空間を開始するには、次のいずれかを入力します。
> ```
> wdsutil /start-Namespace /Namespace:"Custom Auto 1"
> wdsutil /start-Namespace /Server:MyWDSServer /Namespace:"Custom Auto 1"
> ```
> #### <a name="additional-references"></a>その他の参照情報
> [コマンドライン構文のポイント](command-line-syntax-key.md)
> [get AllNamespaces コマンドを使用して](using-the-get-allnamespaces-command.md)
> [新しい名前空間のコマンドを使用して](using-the-new-namespace-command.md)
> [名前空間の削除 コマンドを使用して](using-the-remove-namespace-command.md)
