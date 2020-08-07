---
title: サブコマンド set TransportServer
description: サブコマンド set TransportServer のリファレンス記事。トランスポートサーバーの構成設定を設定します。
ms.topic: article
ms.assetid: 7863225c-f4b2-4cd0-b929-78a454bef249
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9b7725101bcc2230a07c8082f9a57b85d411e80d
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87882126"
---
# <a name="subcommand-set-transportserver"></a>サブコマンド: セット TransportServer

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

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
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|トランスポート サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) を指定できます。 トランスポート サーバーの名前が指定されていない場合は、ローカル サーバーが使用されます。|
|[/ObtainIpv4From: {Dhcp & #124 文字です。範囲}]|次のように、IPv4 アドレスのソースを設定します。<p>-[/start: <IP address> ] IP アドレス範囲の開始を設定します。 これは必須でありに設定されている場合にのみ有効なオプション **範囲**します。<br />-[/End: <IP address>] IP アドレスの範囲の末尾を設定します。 これは必須でありに設定されている場合にのみ有効なオプション **範囲**します。<br />-[/startPort: <port> ] ポート範囲の開始を設定します。<br />-[/EndPort: <port>] ポートの範囲の末尾を設定します。|
|[/ObtainIpv6From:Range]|IPv6 アドレスのソースを指定します。 このオプションは Windows Server 2008 R2 にのみ適用され、サポートされる値は**範囲**のみです。<p>-[/start: <IP address> ] IP アドレス範囲の開始を設定します。 これは必須でありに設定されている場合にのみ有効なオプション **範囲**します。<br />-[/End: <IP address>] IP アドレスの範囲の末尾を設定します。 これは必須でありに設定されている場合にのみ有効なオプション **範囲**します。<br />-[/startPort: <port> ] ポート範囲の開始を設定します。<br />-[/EndPort: <port>] ポートの範囲の末尾を設定します。|
|[/Profile: {10 mbps (& a) #124; 100 mbps & #124; 1 gbps & #124 文字です。カスタム}]|使用するネットワーク プロファイルを指定します。 このオプションは、Windows Server 2008 または Windows Server 2003 を実行しているサーバーで利用できるだけです。|
|[/MulticastSessionPolicy]|マルチキャスト転送用の転送設定を構成します。 このコマンドでは、Windows Server 2008 R2 の使用のみです。<p>-[/ポリシー: {なしと #124 文字です。自動切断 & #124 文字です。複数ストリーム}] では、低速なクライアントの処理方法を決定します。 **None**は、すべてのクライアントを同じ速度で1つのセッションに保持することを意味します。 **自動切断** 、指定の下にドロップするすべてのクライアントをつまり **/Threshold** が切断されています。 **複数ストリーム**は、クライアントは、 **/streamcount**によって指定された複数のセッションに分割されることを意味します。<br />-[/しきい値:<Speed in KBps>] で KBps で最小の転送速度を設定 **/Policy:AutoDisconnect**します。 この速度より下にあるクライアントは、マルチキャスト転送から切断されます。<br />-[/StreamCount: {2 & #124; 3}] []、[フォールバック: {[はい] (& a) #124 文字です。No}] のセッションの数を決定 **/Policy:Multistream**します。 **2** (高速で低速)、2 つのセッションのことを意味し、 **3** 3 つのセッション (低速、中、高速) ことを意味します。<br />-[]、[フォールバック: {[はい] (& a) #124 文字です。判別クライアント tha が切断されているかどうかは引き続き no}] 転送 (クライアントがサポートされている) 場合は、別のメソッドを使用しています。 WDS クライアントを使用している場合、コンピュータがフォールバック ユニキャストにします。 Wdsmcast.exe は、フォールバック メカニズムをサポートしていません。 このオプションは、**複数ストリーム**をサポートしていないクライアントにも適用されます。 その場合は、コンピューターは、低速の転送セッションに移動させる代わりに別のメソッドに戻る分類されます。|
## <a name="examples"></a>例
サーバーの IPv4 アドレスの範囲を設定するには、次のように入力します。
```
wdsutil /Set-TransportServer /ObtainIpv4From:Range /start:239.0.0.1 /End:239.0.0.100
```
サーバーの IPv4 アドレスの範囲、ポートの範囲、およびプロファイルを設定するには、次のように入力します。
```
wdsutil /Set-TransportServer /Server:MyWDSServer /ObtainIpv4From:Range /start:239.0.0.1 /End:239.0.0.100 /startPort:12000 /EndPort:50000 /Profile:10mbps
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のキー](command-line-syntax-key.md) 
[無効化-TransportServer コマンド](using-the-disable-transportserver-command.md) 
 の使用[Enable TransportServer コマンド](using-the-enable-transportserver-command.md) 
 の使用[Get TransportServer コマンド](using-the-get-transportserver-command.md) 
 を使用する[サブコマンド: 開始 TransportServer](subcommand-start-transportserver.md) 
[サブコマンド: 停止 TransportServer](subcommand-stop-transportserver.md)
