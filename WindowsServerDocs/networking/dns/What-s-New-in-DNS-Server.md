---
title: Windows Server の DNS サーバーの新機能
description: このトピックでは、Windows Server 2016 以降のバージョンの DNS サーバーの新機能の概要について説明します。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dns
ms.topic: article
ms.assetid: c9cecb94-3cd5-4da7-9a3e-084148b8226b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: de502d7be023d12e3350063e467a60356b2472c4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406237"
---
# <a name="whats-new-in-dns-server-in-windows-server"></a>Windows Server の DNS サーバーの新機能

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、Windows Server 2016 で新しく追加または変更されたドメインネームシステム (DNS) サーバーの機能について説明します。  
  
Windows Server 2016 では、DNS サーバーは次の領域で拡張サポートを提供します。  
  
|機能|新機能か強化された機能か|説明|  
|-----------------|-------------------|---------------|  
|DNS ポリシー|新規|Dns ポリシーを構成して、dns サーバーが DNS クエリにどのように応答するかを指定できます。 DNS 応答は、クライアントの IP アドレス (場所)、時刻、およびその他のいくつかのパラメーターに基づいています。 DNS ポリシーを使用すると、場所を認識する DNS、トラフィック管理、負荷分散、スプリットブレイン DNS などのシナリオが可能になります。|  
|応答率の制限 (RRL)|新規|DNS サーバーで応答率の制限を有効にすることができます。 これにより、dns サーバーを使用している悪意のあるシステムが、DNS クライアントでサービス拒否攻撃を開始する可能性を回避できます。|  
|名前付きエンティティ (DANE) の DNS ベースの認証|新規|TLSA (トランスポート層のセキュリティ認証) レコードを使用して、DNS クライアントに対して、証明書を要求する CA をドメイン名として指定する情報を提供できます。 これにより、他のユーザーが DNS キャッシュを破損して独自の web サイトを参照し、別の CA から発行された証明書を提供する man-in-the-middle 攻撃を防ぐことができます。|  
|不明なレコードのサポート|新規|不明なレコード機能を使用して、Windows DNS サーバーで明示的にサポートされていないレコードを追加することができます。|  
|IPv6 のルートヒント|新規|IPV6 ルートサーバーを使用して、インターネットの名前解決を実行するには、ネイティブ IPV6 ルートヒントのサポートを使用できます。|  
|Windows PowerShell のサポート|強化された機能|DNS サーバーでは、新しい Windows PowerShell コマンドレットを使用できます。|  
  
## <a name="dns-policies"></a>DNS ポリシー

Geo ロケーションベースのトラフィック管理に DNS ポリシーを使用したり、時間に基づくインテリジェント DNS 応答を使用して、分割\-ブレイン展開用に構成された単一の DNS サーバーを管理したり、DNS クエリにフィルターを適用したりすることができます。 これらの機能の詳細については、次の項目を参照してください。

-   **アプリケーションの負荷分散。** 異なる場所にアプリケーションの複数のインスタンスをデプロイした場合は、DNS ポリシーを使用して、異なるアプリケーションインスタンス間でトラフィックの負荷を分散し、アプリケーションのトラフィック負荷を動的に割り当てることができます。

-   **Geo\-の場所ベースのトラフィック管理。** DNS ポリシーを使用すると、クライアントが接続しようとしているリソースの地理的な場所に基づいて、プライマリおよびセカンダリ DNS サーバーが DNS クライアントクエリに応答できるようになります。クライアントは、最も近いセンター. 

-   **スプリットブレイン DNS。** Split\-ブレイン DNS を使用すると、DNS レコードは同じ DNS サーバー上の異なるゾーンスコープに分割され、DNS クライアントが内部クライアントと外部クライアントのどちらであるかに基づいて応答を受信します。 Active Directory 統合ゾーンまたはスタンドアロン DNS サーバーのゾーンに対して、split\-ブレイン DNS を構成できます。

-   **除外.** 指定した条件に基づいてクエリフィルターを作成するように DNS ポリシーを構成できます。 Dns ポリシーのクエリフィルターを使用すると、dns クエリを送信する dns クエリと dns クライアントに基づいて、カスタムの方法で応答するように DNS サーバーを構成できます。 
-   **捜査.** DNS ポリシーを使用して、悪意のある DNS クライアントを、接続しようとしているコンピューターに転送するのではなく、\-存在しない IP アドレスにリダイレクトすることができます。

-   **時間ベースのリダイレクト。** DNS ポリシーを使用すると、1日の時間に基づく DNS ポリシーを使用して、アプリケーションの異なる地理的に分散したインスタンスにアプリケーショントラフィックを分散させることができます。 
  
Active Directory 統合された DNS ゾーンに DNS ポリシーを使用することもできます。

詳細については、「 [DNS ポリシーシナリオガイド](deploy/DNS-Policies-Overview.md)」を参照してください。

## <a name="response-rate-limiting"></a>応答率の制限

サーバーが同じクライアントを対象とする複数の要求を受け取った場合に、DNS クライアントへの要求への応答方法を制御するために、RRL 設定を構成できます。 これにより、だれかが DNS サーバーを使用してサービス拒否 (Dos) 攻撃を送信するのを防ぐことができます。 たとえば、bot net は、3台目のコンピューターの IP アドレスを要求元として使用して、DNS サーバーに要求を送信できます。 RRL を使用しない場合は、DNS サーバーがすべての要求に応答し、3台目のコンピューターがいっぱいになる可能性があります。 RRL を使用する場合は、次の設定を構成できます。  
  
-   **1 秒あたりの応答数**。 1秒以内にクライアントに同じ応答が与えられる最大回数です。  
  
-   **1 秒あたりのエラー数**。 1秒以内にエラー応答が同じクライアントに送信される最大回数です。  
  
-   **ウィンドウ**。 これは、要求が多すぎる場合にクライアントへの応答が中断される秒数です。  
  
-   **リーク率**。 これは、応答が中断されたときに、DNS サーバーがクエリに応答する頻度です。 たとえば、サーバーがクライアントへの応答を10秒間中断し、リーク率が5の場合でも、サーバーは5つのクエリが送信されるたびに1つのクエリに応答します。 これにより、DNS サーバーがサブネットまたは FQDN に応答率制限を適用している場合でも、正当なクライアントは応答を受け取ることができます。  
  
-   **TC レート**。 これは、クライアントへの応答が中断されたときに TCP との接続を試行するようにクライアントに指示するために使用されます。 たとえば、TC レートが3で、サーバーが特定のクライアントへの応答を中断した場合、サーバーは、受信した3つのクエリごとに TCP 接続の要求を発行します。 [TC rate] の値が [リーク率] より小さいことを確認し、応答をリークする前に TCP 経由で接続するオプションをクライアントに与えます。  
  
-   **最大応答数**。 応答が中断されている間に、サーバーがクライアントに対して発行する応答の最大数です。  
  
-   **ホワイトリストドメイン**。 これは、RRL 設定から除外するドメインの一覧です。  
  
-   **ホワイトリストサブネット**。 これは、RRL 設定から除外するサブネットの一覧です。  
  
-   **ホワイトリストサーバーインターフェイス**。 これは、RRL 設定から除外する DNS サーバーインターフェイスの一覧です。  
  
## <a name="dane-support"></a>DANE のサポート

DANE のサポート \(RFC 6394 および 6698\) を使用して、DNS サーバーでホストされているドメイン名に対して証明書の発行元となる CA を DNS クライアントに指定できます。 これにより、だれかが DNS キャッシュを破壊し、DNS 名を自身の IP アドレスにポイントする man-in-the-middle 攻撃の形態を防ぐことができます。  
  
たとえば、CA1 という有名な機関の証明書を使用して、www.contoso.com で SSL を使用するセキュリティで保護された web サイトをホストするとします。 他のユーザーは、CA2 という名前の別の www.contoso.com 証明機関から証明書を取得することもできます。 次に、偽の www.contoso.com web サイトをホストするエンティティが、クライアントまたはサーバーの DNS キャッシュを破損して、www.contoto.com が偽のサイトを指すようにすることができます。 エンドユーザーには CA2 からの証明書が表示され、単に確認して、偽のサイトに接続することができます。 DANE では、クライアントは TLSA レコードを要求する contoso.com を DNS サーバーに要求し、www.contoso.com の証明書が CA1 によって発行されたことを確認します。 別の CA からの証明書が表示された場合、接続は中止されます。  
  
## <a name="unknown-record-support"></a>不明なレコードのサポート

"不明なレコード" は、DNS サーバーで .RDATA 形式が認識されない RR です。 新しく追加された不明なレコード (RFC 3597) の種類では、サポートされていないレコードの種類を Windows DNS サーバーゾーンに追加することができます。 Windows キャッシュリゾルバーには、既に不明なレコードの種類を処理する機能があります。 Windows DNS サーバーでは、不明なレコードに対してレコード固有の処理は行われませんが、クエリを受信した場合は応答に返されます。  
  
## <a name="ipv6-root-hints"></a>IPv6 のルートヒント

IANA によって発行された IPV6 ルートヒントが windows DNS サーバーに追加されました。 インターネット名クエリで、IPv6 ルートサーバーを使用して名前解決を行うことができるようになりました。

## <a name="windows-powershell-support"></a>Windows PowerShell のサポート

Windows Server 2016 では、次の新しい Windows PowerShell コマンドレットとパラメーターが導入されました。
  
-   **DnsServerRecursionScope**。 このコマンドレットは、DNS サーバー上に新しい再帰スコープを作成します。 Dns ポリシーでは、dns クエリで使用されるフォワーダーの一覧を指定するために、再帰スコープが使用されます。  
  
-   **DnsServerRecursionScope を削除**します。 このコマンドレットは、既存の再帰スコープを削除します。  
  
-   **DnsServerRecursionScope**。 このコマンドレットは、既存の再帰スコープの設定を変更します。  
  
-   **DnsServerRecursionScope**。 このコマンドレットは、既存の再帰スコープに関する情報を取得します。  
  
-   **DnsServerClientSubnet**。 このコマンドレットは、新しい DNS クライアントサブネットを作成します。 サブネットは、dns クライアントが置かれている場所を識別するために、DNS ポリシーによって使用されます。  
  
-   **DnsServerClientSubnet を削除**します。 このコマンドレットは、既存の DNS クライアントサブネットを削除します。  
  
-   **DnsServerClientSubnet**。 このコマンドレットは、既存の DNS クライアントサブネットの設定を変更します。  
  
-   **DnsServerClientSubnet**。 このコマンドレットは、既存の DNS クライアントサブネットに関する情報を取得します。  
  
-   **DnsServerQueryResolutionPolicy**。 このコマンドレットは、新しい DNS クエリ解決ポリシーを作成します。 DNS クエリ解決ポリシーは、さまざまな条件に基づいてクエリの応答方法を指定するために使用されます。  
  
-   **DnsServerQueryResolutionPolicy を削除**します。 このコマンドレットは、既存の DNS ポリシーを削除します。  
  
-   **DnsServerQueryResolutionPolicy**。 このコマンドレットは、既存の DNS ポリシーの設定を変更します。  
  
-   **DnsServerQueryResolutionPolicy**。 このコマンドレットは、既存の DNS ポリシーに関する情報を取得します。  
  
-   **DnsServerPolicy を有効に**します。 このコマンドレットは、既存の DNS ポリシーを有効にします。  
  
-   **DnsServerPolicy を無効に**します。 このコマンドレットは、既存の DNS ポリシーを無効にします。  
  
-   **DnsServerZoneTransferPolicy**。 このコマンドレットは、新しい DNS サーバーゾーン転送ポリシーを作成します。 DNS ゾーン転送ポリシーでは、異なる条件に基づいてゾーン転送を拒否するか無視するかを指定します。  
  
-   **DnsServerZoneTransferPolicy を削除**します。 このコマンドレットは、既存の DNS サーバーゾーン転送ポリシーを削除します。  
  
-   **DnsServerZoneTransferPolicy**。 このコマンドレットは、既存の DNS サーバーゾーン転送ポリシーの設定を変更します。  
  
-   **DnsServerResponseRateLimiting**。 このコマンドレットは、RRL 設定を取得します。  
  
-   **DnsServerResponseRateLimiting**。 このコマンドレットは、RRL 設定を変更します。  
  
-   **DnsServerResponseRateLimitingExceptionlist**。 このコマンドレットは、DNS サーバー上に RRL 例外リストを作成します。  
  
-   **DnsServerResponseRateLimitingExceptionlist**。 このコマンドレットは、RRL excception リストを取得します。  
  
-   **DnsServerResponseRateLimitingExceptionlist を削除**します。 このコマンドレットは、既存の RRL 例外リストを削除します。  
  
-   **DnsServerResponseRateLimitingExceptionlist**。 このコマンドレットは、RRL 例外リストを変更します。  
  
-   **DnsServerResourceRecord**。 このコマンドレットは、不明なレコードの種類をサポートするように更新されました。  
  
-   **DnsServerResourceRecord**。 このコマンドレットは、不明なレコードの種類をサポートするように更新されました。  
  
-   **DnsServerResourceRecord を削除**します。 このコマンドレットは、不明なレコードの種類をサポートするように更新されました。  
  
-   **DnsServerResourceRecord**。 このコマンドレットは、不明なレコードの種類をサポートするように更新されました

詳細については、Windows Server 2016 Windows PowerShell コマンドリファレンスの次のトピックを参照してください。

- [DnsServer モジュール](https://docs.microsoft.com/powershell/module/dnsserver/?view=win10-ps)
- [DnsClient モジュール](https://docs.microsoft.com/powershell/module/dnsclient/?view=win10-ps)

## <a name="see-also"></a>関連項目  
  
-   [DNS クライアントの新機能](What-s-New-in-DNS-Client.md)  
  

  

