---
title: 名前空間の削除
description: カスタム名前空間を削除する、名前空間の削除に関するリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4eb758b6-8519-4e26-9fe0-2e19bb0e8702
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2ef329a53a7f212c1810af2e4ced11a2abf76840
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720334"
---
# <a name="using-the-remove-namespace-command"></a>名前空間の削除] コマンドを使用してください。

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

カスタムの名前空間を削除します。

## <a name="syntax"></a>構文
```
wdsutil /remove-Namespace /Namespace:<Namespace name> [/Server:<Server name>] [/force]
```
### <a name="parameters"></a>パラメーター
|パラメーター|[説明]|
|-------|--------|
|空間<Namespace name>|名前空間の名前を指定します。 フレンドリ名ではありませんし、一意である必要があります。<p>-   **展開サーバーの役割サービス**: 名前空間名の構文は/NAMESPACE: WDS<ImageGroup>/<ImageName>/<Index>: です。 例: **WDS:ImageGroup1/install.wim/1**<br />-   **トランスポートサーバーの役割サービス**: この値は、サーバー上で作成されたときに名前空間に指定された名前と一致する必要があります。|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|
|/force|名前空間を直ちに削除し、すべてのクライアントを終了します。 **/Force**を指定しない限り、既存のクライアントは転送を完了できますが、新しいクライアントは参加できません。|
## <a name="examples"></a>例
名前空間を停止する (現在のクライアントは、転送を完了できますが、新しいクライアントが参加することができません、) の種類。
```
wdsutil /remove-Namespace /Namespace:Custom Auto 1
```
すべてのクライアントの終了時に、次のように入力します。
```
wdsutil /remove-Namespace /Server:MyWDSServer /Namespace:Custom Auto 1 /force
```
## <a name="additional-references"></a>その他のリファレンス
- [コマンドライン構文のキー](command-line-syntax-key.md)
を使用して[get allnamespaces コマンド](using-the-get-allnamespaces-command.md)
を使用して[、](using-the-new-namespace-command.md)
[サブコマンド: 開始名前](subcommand-start-namespace.md)空間
