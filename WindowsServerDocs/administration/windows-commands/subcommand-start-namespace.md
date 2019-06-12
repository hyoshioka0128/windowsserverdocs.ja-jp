---
title: サブコマンド開始 Namespace
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 9a54f849580a139470c2cca43ba57fee60dc81ec
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441151"
---
# <a name="subcommand-start-namespace"></a>サブコマンド: 開始-名前空間

> 適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012 は、スケジュールされたキャストの名前空間を開始します。
> ## <a name="syntax"></a>構文
> ```
> wdsutil /start-Namespace /Namespace:<Namespace name> [/Server:<Server name>]
> ```
> ## <a name="parameters"></a>パラメーター
> 
> |          パラメーター          |                                                                                                                                                                                             説明                                                                                                                                                                                             |
> |-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
> | /Namespace:<Namespace name> | 名前空間の名前を指定します。 これは、フレンドリ名ではない、一意である必要があることに注意してください。<br /><br />-   **展開サーバー**:名前空間名の構文は/Namspace:WDS:<Image group>/<Image name>/<Index>します。 例:**WDS:ImageGroup1/install.wim/1**<br />-   **トランスポート サーバー**:この名前は、サーバー上で作成されたときに、名前空間に付けた名前に一致する必要があります。 |
> |   [/Server:<Server name>]   |                                                                                                           サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。                                                                                                           |
> 
> ## <a name="BKMK_examples"></a>例
> 名前空間を開始するには、次のいずれかを入力します。
> ```
> wdsutil /start-Namespace /Namespace:"Custom Auto 1"
> wdsutil /start-Namespace /Server:MyWDSServer /Namespace:"Custom Auto 1"
> ```
> #### <a name="additional-references"></a>その他の参照
> [コマンドライン構文のポイント](command-line-syntax-key.md)
> [get AllNamespaces コマンドを使用して](using-the-get-allnamespaces-command.md)
> [新しい名前空間のコマンドを使用して](using-the-new-namespace-command.md)
> [名前空間の削除 コマンドを使用して](using-the-remove-namespace-command.md)
