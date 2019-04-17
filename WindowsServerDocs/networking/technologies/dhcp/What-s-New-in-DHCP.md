---
title: DHCP の新機能
description: このトピックでは、動的ホスト構成プロトコル (DHCP) Windows Server 2016 での新機能の概要を示します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dhcp
ms.topic: get-started-article
ms.assetid: c6f36998-5b64-45d1-b1f0-0f0d6604dbe3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f67e5dfd8aefcf408a41f6fc919665419f0ff1c9
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="whats-new-in-dhcp"></a>DHCP の新機能

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、Windows Server 2016 で追加または変更されている動的ホスト構成プロトコル (DHCP) 機能について説明します。
  
DHCP は、管理の負担と、プライベート イントラネットなど、IP\ ベースのネットワーク上でホストの構成の複雑さを軽減するように設計されたインターネット技術標準化委員会 (IETF) 標準です。 DHCP サーバー サービスを使用すると、DHCP クライアントに TCP/IP を構成するプロセスは自動です。

次のセクションでは、DHCP の機能で新機能と変更に関する情報を提供します。

## <a name="dhcp-subnet-selection-options"></a>DHCP サブネットの選択オプション

DHCP は、オプション 118 と 82 \(sub-option 5\) ようになりました。 特定のサブネットと IP アドレスの範囲を特定およびスコープから IP アドレスを要求するのにには、DHCP プロキシ クライアントとリレー エージェントを許可するようにこれらのオプションを使用することができます。

DHCP オプション 118、Windows Server 2016 とリモート アクセス サーバーの役割を実行している仮想プライベート ネットワーク \(VPN\) サーバーなどで構成されている DHCP プロキシ クライアントを使用している場合、VPN サーバーは、特定の IP アドレス範囲からの VPN クライアントの IP アドレスのリースを要求できます。

DHCP オプション 82、sub\ オプション 5 で構成されている DHCP リレー エージェントを使用している場合、リレー エージェントは、特定の IP アドレス範囲からの DHCP クライアントの IP アドレスのリースを要求できます。

詳細については、次を参照してください。[DHCP サブネットの選択オプション](dhcp-subnet-options.md)します。

## <a name="new-logging-events-for-dns-registration-failures-by-the-dhcp-server"></a>新しい DHCP サーバーが DNS 登録エラーのイベント ログの記録

DHCP には、DNS サーバーで dhcp サーバーの DNS レコードの登録が失敗する場合のイベント ログ記録が含まれています。

詳細については、次を参照してください。[DNS レコードの登録に関する DHCP ログ イベント](dhcp-dns-events.md)します。

## <a name="dhcp-nap-is-not-supported-in-windows-server-2016"></a>DHCP NAP は Windows Server 2016 でサポートされていません

ネットワーク アクセス保護 \(NAP\) は Windows Server 2012 R2 で推奨されていませんし、Windows Server 2016 では、DHCP サーバーの役割はサポートしなくなりました NAP します。 詳細については、次を参照してください。[Features Removed or Deprecated in Windows Server 2012 R2](https://technet.microsoft.com/library/dn303411.aspx)します。  
  
NAP サポートは、Windows Server 2008 では、DHCP サーバーの役割に導入されたし、Windows 10 および Windows Server 2016 の前に、Windows クライアントおよびサーバー オペレーティング システムではサポートされています。 次の表は、Windows Server での NAP のサポートをまとめたものです。  
  
|オペレーティング システム|NAP のサポート|  
|--------------------|---------------|  
| Windows Server 2008 |サポートされています。|  
| Windows Server 2008 R2 |サポートされています。|  
| Windows Server 2012 |サポートされています。|  
| Windows Server 2012 R2 |サポートされています。|  
| Windows Server 2016|サポートされていません|  
  
NAP の展開では、NAP をサポートするオペレーティング システムを実行している DHCP サーバーは、DHCP の NAP 強制方法の NAP 強制ポイントとして機能できます。 DHCP NAP の詳細については、次を参照してください。[チェックリスト: DHCP 実施設計の実装](https://technet.microsoft.com/library/dd314186.aspx)します。  
  
Windows Server 2016 での DHCP サーバーは、NAP ポリシーを強制せず、DHCP スコープが NAP\ 有効にすることはできません。 NAP クライアントでもある DHCP クライアント コンピューターは、DHCP 要求と共にヘルス \(SoH\) のステートメントを送信します。 DHCP サーバーが Windows Server 2016 を実行している場合、SoH が存在しない場合、これらの要求が処理されます。 DHCP サーバーは、通常 DHCP リースをクライアントに付与します。 

Windows Server 2016 を実行しているサーバーが RADIUS プロキシに NAP をサポートするネットワーク ポリシー サーバー \(NPS\) 認証要求を転送する場合は、これらの NAP クライアントは非 NAP\ 対応、および NAP が失敗した場合の処理としての NPS によって評価されます。
  
## <a name="see-also"></a>参照してください。  
  
-   [動的ホスト構成プロトコル (DHCP)](Dynamic-Host-Configuration-Protocol--DHCP-.md)  
  

