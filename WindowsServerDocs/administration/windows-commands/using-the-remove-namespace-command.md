---
title: 名前空間の削除 コマンドを使用してください。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4eb758b6-8519-4e26-9fe0-2e19bb0e8702
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 115c0a90a60e18ee4b89758200773d1dfec2163f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842043"
---
# <a name="using-the-remove-namespace-command"></a>名前空間の削除 コマンドを使用してください。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

カスタムの名前空間を削除します。
## <a name="syntax"></a>構文
```
wdsutil /remove-Namespace /Namespace:<Namespace name> [/Server:<Server name>] [/force]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/Namespace:<Namespace name>|名前空間の名前を指定します。 フレンドリ名ではありませんし、一意である必要があります。<br /><br />-   **展開サーバーの役割サービス**:名前空間名の構文は/Namespace:WDS:<ImageGroup>/<ImageName>/<Index>します。 次に、例を示します。**WDS:ImageGroup1/install.wim/1**<br />-   **サーバーの役割サービスのトランスポート**:この値は、サーバー上で作成されたときに、名前空間に付けた名前と一致する必要があります。|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|
|[/force]|すぐに、名前空間を削除し、すべてのクライアントを終了します。 指定しない限り注意 **/force**、既存のクライアントは、転送を完了できますが、新しいクライアントは参加できません。|
## <a name="BKMK_examples"></a>例
名前空間を停止する (現在のクライアントは、転送を完了できますが、新しいクライアントが参加することができません、) の種類。
```
wdsutil /remove-Namespace /Namespace:"Custom Auto 1"
```
すべてのクライアントの終了時に、次のように入力します。
```
wdsutil /remove-Namespace /Server:MyWDSServer /Namespace:"Custom Auto 1" /force
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[get AllNamespaces コマンドを使用して](using-the-get-allnamespaces-command.md)
[新しい名前空間のコマンドを使用して](using-the-new-namespace-command.md)
[サブコマンド: 名前空間の開始](subcommand-start-namespace.md)
