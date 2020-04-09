---
title: 新しい名前空間
description: 新しい名前空間を作成して構成する新しい名前空間の Windows コマンドに関するトピック。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6df60703-30bd-4d59-a8d9-9fe3efe96add
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6f616c33525d033827d52925e07764761e7c7b44
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830635"
---
# <a name="new-namespace"></a>新しい名前空間

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

作成し、新しい名前空間を構成します。 インストールされているトランスポート サーバーの役割サービスのみがある場合は、このオプションを使用する必要があります。 展開サーバーの役割サービスとトランスポート サーバーの役割サービスの両方がインストールされる既定値) がある場合は、使用して [MulticastTransmission 新しいコマンドを使用して](using-the-new-multicasttransmission-command.md)します。 このオプションを使用する前に、コンテンツ プロバイダーを登録することに注意してください。
## <a name="syntax"></a>構文
```
wdsutil [Options] /New-Namespace [/Server:<Server name>]
     /FriendlyName:<Friendly name>
     [/Description:<Description>]
     /Namespace:<Namespace name>
     /ContentProvider:<Name>
     [/ConfigString:<Configuration string>]
     /Namespacetype: {AutoCast | ScheduledCast}
         [/time:<YYYY/MM/DD:hh:mm>]
         [/Clients:<Number of clients>]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) を指定できます。 サーバー名が指定されていない場合は、ローカル サーバーが使用されます。|
|/FriendlyName:<Friendly name>|名前空間のフレンドリ名を指定します。|
|/Description<Description>]|名前空間の説明を設定します。|
|/Namespace:<Namespace name>|名前空間の名前を指定します。 これは、フレンドリ名ではない、一意である必要があることに注意してください。<p>-   **展開サーバーの役割サービス**: このオプションの構文は、/NAMESPACE: WDS:<Image group>/<Image name>/<Index>です。 例: **WDS:ImageGroup1/install.wim/1**<br />-   **トランスポートサーバーの役割サービス**: この値は、サーバー上で名前空間が作成されたときに指定された名前と一致する必要があります。|
|/ContentProvider:<Name>]|名前空間のコンテンツを提供するコンテンツ プロバイダーの名前を指定します。|
|[/ConfigString:<Configuration string>]|コンテンツ プロバイダーの構成文字列を指定します。|
|/Namespacetype: {AutoCast &#124; scheduledcast}|送信の設定を指定します。 次のオプションを使用して設定を指定します。<p>-[/時刻: <time>]-YYYY/MM/DD: hh: mm の形式を使用して、転送を開始する時刻を設定します。 このオプションは、スケジュールされたキャスト転送のみに適用されます。<br />-[/クライアント: <Number of clients>]-クライアントから送信が開始する前に待機するの最小数を設定します。 このオプションは、スケジュールされたキャスト転送のみに適用されます。|
## <a name="examples"></a><a name=BKMK_examples></a>例
自動キャストの名前空間を作成するには、次のように入力します。
```
wdsutil /New-Namespace /FriendlyName:Custom AutoCast Namespace /Namespace:Custom Auto 1 /ContentProvider:MyContentProvider /Namespacetype:AutoCast
```
スケジュールされたキャストの名前空間を作成するには、次のように入力します。
```
wdsutil /New-Namespace /Server:MyWDSServer /FriendlyName:Custom Scheduled Namespace /Namespace:Custom Auto 1 /ContentProvider:MyContentProvider 
/Namespacetype:ScheduledCast /time:2006/11/20:17:00 /Clients:20
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のポイント](command-line-syntax-key.md)
[get AllNamespaces コマンドを使用して](using-the-get-allnamespaces-command.md)
[名前空間の削除 コマンドを使用して](using-the-remove-namespace-command.md)
[サブコマンド: 名前空間の開始](subcommand-start-namespace.md)
