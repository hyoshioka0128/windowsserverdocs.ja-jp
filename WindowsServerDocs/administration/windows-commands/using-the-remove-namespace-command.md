---
title: 名前空間の削除
description: カスタム名前空間を削除する、remove Namespace の Windows コマンドに関するトピック。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4eb758b6-8519-4e26-9fe0-2e19bb0e8702
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1f8b830a5d99d13ed00a3a19f2cf246ad71d1c5f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830235"
---
# <a name="using-the-remove-namespace-command"></a>名前空間の削除 コマンドを使用してください。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

カスタムの名前空間を削除します。

## <a name="syntax"></a>構文
```
wdsutil /remove-Namespace /Namespace:<Namespace name> [/Server:<Server name>] [/force]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/Namespace:<Namespace name>|名前空間の名前を指定します。 フレンドリ名ではありませんし、一意である必要があります。<p>-   **展開サーバーの役割サービス**: 名前空間名の構文は/NAMESPACE: WDS:<ImageGroup>/<ImageName>/<Index>です。 例: **WDS:ImageGroup1/install.wim/1**<br />-   **トランスポートサーバーの役割サービス**: この値は、サーバー上で作成されたときに名前空間に指定された名前と一致する必要があります。|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|
|/force|名前空間を直ちに削除し、すべてのクライアントを終了します。 **/Force**を指定しない限り、既存のクライアントは転送を完了できますが、新しいクライアントは参加できません。|
## <a name="examples"></a><a name=BKMK_examples></a>例
名前空間を停止する (現在のクライアントは、転送を完了できますが、新しいクライアントが参加することができません、) の種類。
```
wdsutil /remove-Namespace /Namespace:Custom Auto 1
```
すべてのクライアントの終了時に、次のように入力します。
```
wdsutil /remove-Namespace /Server:MyWDSServer /Namespace:Custom Auto 1 /force
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のポイント](command-line-syntax-key.md)
[get AllNamespaces コマンドを使用して](using-the-get-allnamespaces-command.md)
[新しい名前空間のコマンドを使用して](using-the-new-namespace-command.md)
[サブコマンド: 名前空間の開始](subcommand-start-namespace.md)
