---
title: サブコマンド セット TransportServer
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7863225c-f4b2-4cd0-b929-78a454bef249
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d144ed7d461cbebcd351aa4347fde20f35736c26
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886603"
---
# <a name="subcommand-set-transportserver"></a>サブコマンド: セット TransportServer

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

トランスポート サーバーの構成設定を設定します。
## <a name="syntax"></a>構文
```
wdsutil [Options] /Set-TransportServer [/Server:<Server name>]
     [/ObtainIpv4From:{Dhcp | Range}]
        [/start:<starting IP address>]
        [/End:<Ending IP address>]
     [/ObtainIpv6From:Range]\n\
        [/start:<start IP address>]\n\
        [/End:<End IP address>]      
     [/startPort:<starting port>
        [/EndPort:<starting port>
     [/Profile:{10Mbps | 100Mbps | 1Gbps | Custom}]    
     [/MulticastSessionPolicy]
             [/Policy:{None | AutoDisconnect | Multistream}]
                 [/Threshold:<Speed in KBps>]
                 [/StreamCount:{2 | 3}]
                 [/Fallback:{Yes | No}]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|トランスポート サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) を指定できます。 トランスポート サーバーの名前が指定されていない場合は、ローカル サーバーが使用されます。|
|[/ObtainIpv4From: {Dhcp &#124 文字です。範囲}]|次のように、IPv4 アドレスのソースを設定します。<br /><br />-[/start: <IP address>] IP アドレスの範囲の開始日を設定します。 これは必須でありに設定されている場合にのみ有効なオプション **範囲**します。<br />-[/End: <IP address>] IP アドレスの範囲の末尾を設定します。 これは必須でありに設定されている場合にのみ有効なオプション **範囲**します。<br />-[/startPort: <port>] ポートの範囲の開始日を設定します。<br />-[/EndPort: <port>] ポートの範囲の末尾を設定します。|
|[/ObtainIpv6From:Range]|IPv6 アドレスのソースを指定します。 このオプションは、Windows Server 2008 R2 にのみ適用され、唯一サポートされている値は **範囲**します。<br /><br />-[/start: <IP address>] IP アドレスの範囲の開始日を設定します。 これは必須でありに設定されている場合にのみ有効なオプション **範囲**します。<br />-[/End: <IP address>] IP アドレスの範囲の末尾を設定します。 これは必須でありに設定されている場合にのみ有効なオプション **範囲**します。<br />-[/startPort: <port>] ポートの範囲の開始日を設定します。<br />-[/EndPort: <port>] ポートの範囲の末尾を設定します。|
|[/Profile: {10 mbps (& a) #124; 100 mbps &#124; 1 gbps &#124 文字です。カスタム}]|使用するネットワーク プロファイルを指定します。 このオプションは、Windows Server 2008 または Windows Server 2003 を実行しているサーバーで利用できるだけです。|
|[/MulticastSessionPolicy]|マルチキャスト転送用の転送設定を構成します。 このコマンドでは、Windows Server 2008 R2 の使用のみです。<br /><br />-[/ポリシー: {なしと #124 文字です。自動切断 &#124 文字です。複数ストリーム}] では、低速なクライアントの処理方法を決定します。 **[なし]** 同じ速度での 1 つのセッションをすべてのクライアントを維持することを意味します。 **自動切断** 、指定の下にドロップするすべてのクライアントをつまり **/Threshold** が切断されています。 **複数ストリーム** クライアントが複数のセッションで指定したとおりに区切られるようにすることを意味 **/StreamCount**します。<br />-[/しきい値:<Speed in KBps>] で KBps で最小の転送速度を設定 **/Policy:AutoDisconnect**します。 この速度より下にあるクライアントは、マルチキャスト転送から切断されます。<br />-[/StreamCount: {2 &#124; 3}] []、[フォールバック: {[はい] (& a) #124 文字です。No}] のセッションの数を決定 **/Policy:Multistream**します。 **2** (高速で低速)、2 つのセッションのことを意味し、 **3** 3 つのセッション (低速、中、高速) ことを意味します。<br />-[]、[フォールバック: {[はい] (& a) #124 文字です。判別クライアント tha が切断されているかどうかは引き続き no}] 転送 (クライアントがサポートされている) 場合は、別のメソッドを使用しています。 WDS クライアントを使用している場合、コンピュータがフォールバック ユニキャストにします。 Wdsmcast.exe は、フォールバック メカニズムをサポートしていません。 このオプションはサポートしていないクライアントにも適用されます **複数ストリーム**します。 その場合は、コンピューターは、低速の転送セッションに移動させる代わりに別のメソッドに戻る分類されます。|
## <a name="BKMK_examples"></a>例
サーバーの IPv4 アドレスの範囲を設定するには、次のように入力します。
```
wdsutil /Set-TransportServer /ObtainIpv4From:Range /start:239.0.0.1 /End:239.0.0.100
```
サーバーの IPv4 アドレスの範囲、ポートの範囲、およびプロファイルを設定するには、次のように入力します。
```
wdsutil /Set-TransportServer /Server:MyWDSServer /ObtainIpv4From:Range /start:239.0.0.1 /End:239.0.0.100 /startPort:12000 /EndPort:50000 /Profile:10mbps
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[TransportServer 無効にするコマンドを使用して](using-the-disable-transportserver-command.md)
[TransportServer 有効にするコマンドを使用して](using-the-enable-transportserver-command.md)
[get TransportServer コマンドを使用して](using-the-get-transportserver-command.md)
[サブコマンド: 開始 TransportServer](subcommand-start-transportserver.md)
[サブコマンド: 停止 TransportServer](subcommand-stop-transportserver.md)
