---
title: 名前空間の削除 コマンドを使用してください。
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: b4c087442c43fd885fe4554cb29f9b2788420e05
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362792"
---
# <a name="using-the-remove-namespace-command"></a>名前空間の削除 コマンドを使用してください。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

カスタム名前空間を削除します。
## <a name="syntax"></a>構文
```
wdsutil /remove-Namespace /Namespace:<Namespace name> [/Server:<Server name>] [/force]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/Namespace: <Namespace name>|名前空間の名前を指定します。 フレンドリ名ではありませんし、一意である必要があります。<br /><br />@no__t 0**展開サーバーの役割サービス**:名前空間名の構文は/Namespace: WDS: <ImageGroup> @ no__t @ no__t @ no__t @ no__t-4 です。 以下に例を示します。**WDS: ImageGroup1/install. .wim/1**<br />-   **トランスポートサーバーの役割サービス**:この値は、サーバー上で作成されたときに名前空間に指定された名前と一致する必要があります。|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|
|/force|名前空間を直ちに削除し、すべてのクライアントを終了します。 **/Force**を指定しない限り、既存のクライアントは転送を完了できますが、新しいクライアントは参加できません。|
## <a name="BKMK_examples"></a>例
名前空間を停止する (現在のクライアントは、転送を完了できますが、新しいクライアントが参加することができません、) の種類。
```
wdsutil /remove-Namespace /Namespace:"Custom Auto 1"
```
すべてのクライアントの終了時に、次のように入力します。
```
wdsutil /remove-Namespace /Server:MyWDSServer /Namespace:"Custom Auto 1" /force
```
#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文のポイント](command-line-syntax-key.md)
[get AllNamespaces コマンドを使用して](using-the-get-allnamespaces-command.md)
[新しい名前空間のコマンドを使用して](using-the-new-namespace-command.md)
[サブコマンド: 名前空間の開始](subcommand-start-namespace.md)
