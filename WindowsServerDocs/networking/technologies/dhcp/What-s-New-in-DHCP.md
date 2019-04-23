---
title: DHCP の新機能
description: このトピックでは、動的ホスト構成プロトコル (DHCP) で Windows Server 2016 の新機能の概要を示します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dhcp
ms.topic: get-started-article
ms.assetid: c6f36998-5b64-45d1-b1f0-0f0d6604dbe3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 73cc5134f7af5063c912ad578fa7d660b3194aa1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840233"
---
# <a name="whats-new-in-dhcp"></a>DHCP の新機能

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、Windows Server 2016 で追加または変更している動的ホスト構成プロトコル (DHCP) 機能について説明します。
  
DHCP は、管理上の負担とホストの TCP/IP 構成の複雑さを軽減するように設計されたインターネット技術標準化委員会 (IETF) 標準\-ベースのプライベート イントラネットなどのネットワーク。 DHCP クライアントに TCP/IP を構成するプロセスは、DHCP サーバー サービスを使うことによって自動化されます。

次のセクションは、機能、DHCP の新機能と変更に関する情報を提供します。

## <a name="dhcp-subnet-selection-options"></a>DHCP サブネットの選択オプション

DHCP オプション 118 および 82 サポート\(サブ オプション 5\)します。 これらのオプションを使用すると、特定のサブネットと、特定の IP アドレス範囲とスコープから IP アドレスを要求するのにには、DHCP プロキシ クライアントとリレー エージェントを許可します。


DHCP オプション 82 で構成されている DHCP リレー エージェントを使用している場合は、サブ\-オプション 5、リレー エージェントは、特定の IP アドレス範囲からの DHCP クライアントの IP アドレスのリースを要求することができます。

詳細については、次を参照してください。 [DHCP サブネットの選択オプション](dhcp-subnet-options.md)します。

## <a name="new-logging-events-for-dns-registration-failures-by-the-dhcp-server"></a>新しい DHCP サーバーによって DNS 登録エラーのイベントのログ記録

DHCP には、DNS サーバーで dhcp サーバーの DNS レコードの登録が失敗する状況のログ イベントが含まれています。

詳細については、次を参照してください。 [DHCP DNS レコードの登録のためのイベントのログ記録](dhcp-dns-events.md)します。

## <a name="dhcp-nap-is-not-supported-in-windows-server-2016"></a>DHCP NAP は Windows Server 2016 でサポートされていません

ネットワーク アクセス保護\(NAP\)は Windows Server 2012 R2 で非推奨し、Windows Server 2016、DHCP サーバーの役割で NAP をサポートしていません。 詳細については、次を参照してください。 [Features Removed or Deprecated in Windows Server 2012 R2](https://technet.microsoft.com/library/dn303411.aspx)します。  
  
NAP サポートは、Windows Server 2008 では、DHCP サーバーの役割が導入され、Windows 10 および Windows Server 2016 より前の Windows クライアントとサーバー オペレーティング システムではサポートされてです。 次の表では、Windows Server における NAP のサポートをまとめたものです。  
  
|オペレーティング システム|NAP サポート|  
|--------------------|---------------|  
| Windows Server 2008 |サポートされている|  
| Windows Server 2008 R2 |サポートされている|  
| Windows Server 2012 |サポートされている|  
| Windows Server 2012 R2 |サポートされている|  
| Windows Server 2016|サポートされていません|  
  
NAP の展開で NAP をサポートするオペレーティング システムを実行している DHCP サーバーは、NAP DHCP 強制方法の NAP 強制ポイントとして機能できます。 DHCP の NAP の詳細については、次を参照してください。[チェックリスト。DHCP 強制の設計を実装する](https://technet.microsoft.com/library/dd314186.aspx)します。  
  
Windows Server 2016 での DHCP サーバーを適用しない NAP のポリシーと、DHCP スコープで NAP をすることはできません\-を有効にします。 NAP クライアントでもある DHCP クライアント コンピューターの正常性ステートメントを送信する\(SoH\) DHCP 要求にします。 DHCP サーバーで Windows Server 2016 が実行されている場合、これらの要求は、SoH が存在しないかのように処理されます。 DHCP サーバーは、通常 DHCP リースをクライアントに付与します。 

Windows Server 2016 を実行しているサーバーが RADIUS プロキシ、ネットワーク ポリシー サーバーに認証要求を転送する場合は\(NPS\) NAP をサポートする、非 NAP として機能する NPS によって、これらの NAP クライアントが評価\-対応、およびNAP の処理に失敗します。
  
## <a name="see-also"></a>関連項目  
  
-   [動的ホスト構成プロトコル (DHCP)](Dynamic-Host-Configuration-Protocol--DHCP-.md)  
  

