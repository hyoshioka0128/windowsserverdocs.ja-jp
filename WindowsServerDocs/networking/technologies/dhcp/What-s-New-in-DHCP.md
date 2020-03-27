---
title: DHCP の新機能
description: このトピックでは、Windows Server 2016 の動的ホスト構成プロトコル (DHCP) の新機能の概要について説明します。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dhcp
ms.topic: get-started-article
ms.assetid: c6f36998-5b64-45d1-b1f0-0f0d6604dbe3
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 58d849fa1003148b034cc426817b97d3a70d4421
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312695"
---
# <a name="whats-new-in-dhcp"></a>DHCP の新機能

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、Windows Server 2016 で新しく追加または変更された動的ホスト構成プロトコル (DHCP) の機能について説明します。
  
DHCP は、インターネット技術標準化委員会 (IETF) 標準であり、プライベートイントラネットなど、TCP/IP\-ベースのネットワーク上でホストを構成する際の管理負担と複雑さを軽減するように設計されています。 DHCP クライアントに TCP/IP を構成するプロセスは、DHCP サーバー サービスを使うことによって自動化されます。

次のセクションでは、DHCP の新機能と機能の変更について説明します。

## <a name="dhcp-subnet-selection-options"></a>DHCP サブネットの選択オプション

DHCP では、オプション118と 82 \(サブオプション 5\)がサポートされるようになりました。 これらのオプションを使用すると、DHCP プロキシクライアントおよびリレーエージェントが特定のサブネットの IP アドレス、および特定の IP アドレス範囲とスコープを要求できるようになります。


Dhcp オプション82、サブ\-オプション5で構成されている DHCP リレーエージェントを使用している場合、リレーエージェントは特定の IP アドレス範囲から DHCP クライアントの IP アドレスリースを要求できます。

詳細については、「 [DHCP サブネットの選択オプション](dhcp-subnet-options.md)」を参照してください。

## <a name="new-logging-events-for-dns-registration-failures-by-the-dhcp-server"></a>DHCP サーバーによる DNS 登録エラーの新しいログ記録イベント

DHCP には、DHCP サーバーの DNS レコードの登録が DNS サーバーで失敗する状況のログ記録イベントが含まれるようになりました。

詳細については、「 [DNS レコードの登録の DHCP ログイベント](dhcp-dns-events.md)」を参照してください。

## <a name="dhcp-nap-is-not-supported-in-windows-server-2016"></a>DHCP NAP は Windows Server 2016 ではサポートされていません

Windows Server 2012 R2 では、ネットワークアクセス保護 \(NAP\) は非推奨とされます。 Windows Server 2016 では、DHCP サーバーの役割は NAP をサポートしなくなりました。 詳細については、「 [Windows Server 2012 R2 で削除された機能または非推奨の機能](https://technet.microsoft.com/library/dn303411.aspx)」を参照してください。  
  
NAP サポートは、windows Server 2008 で DHCP サーバーの役割に導入され、windows 10 および Windows Server 2016 より前の Windows クライアントおよびサーバーオペレーティングシステムでサポートされています。 次の表は、Windows Server での NAP のサポートをまとめたものです。  
  
|オペレーティング システム|NAP サポート|  
|--------------------|---------------|  
| Windows Server 2008 |サポート対象|  
| Windows Server 2008 R2 |サポート対象|  
| Windows Server 2012 |サポート対象|  
| Windows Server 2012 R2 |サポート対象|  
| Windows Server 2016|サポートされない|  
  
Nap 展開では、nap をサポートするオペレーティングシステムを実行している DHCP サーバーは、nap DHCP 強制方法の NAP 強制ポイントとして機能できます。 NAP の DHCP の詳細については、「[チェックリスト: Dhcp 強制設計の実装](https://technet.microsoft.com/library/dd314186.aspx)」を参照してください。  
  
Windows Server 2016 では、DHCP サーバーは NAP ポリシーを強制しません。また、DHCP スコープを NAP\-有効にすることはできません。 また、NAP クライアントである DHCP クライアントコンピューターは、DHCP 要求と共に正常性ステートメント \(SoH\) を送信します。 DHCP サーバーで Windows Server 2016 が実行されている場合、これらの要求は SoH が存在しないかのように処理されます。 DHCP サーバーは、クライアントに通常の DHCP リースを付与します。 

Windows Server 2016 を実行しているサーバーが、NAP をサポートする NPS\) \(ネットワークポリシーサーバーに認証要求を転送する RADIUS プロキシである場合、これらの NAP クライアントは NPS によって NAP 以外の\-対応として評価され、NAP 処理は失敗します。
  
## <a name="see-also"></a>参照  
  
-   [動的ホスト構成プロトコル (DHCP)](Dynamic-Host-Configuration-Protocol--DHCP-.md)  
  

