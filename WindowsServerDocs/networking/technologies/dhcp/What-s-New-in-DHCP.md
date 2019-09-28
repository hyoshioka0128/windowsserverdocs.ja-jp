---
title: DHCP の新機能
description: このトピックでは、Windows Server 2016 の動的ホスト構成プロトコル (DHCP) の新機能の概要について説明します。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dhcp
ms.topic: get-started-article
ms.assetid: c6f36998-5b64-45d1-b1f0-0f0d6604dbe3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8032b7c8e78170d57b0367775672577d9fd900e2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355452"
---
# <a name="whats-new-in-dhcp"></a>DHCP の新機能

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、Windows Server 2016 で新しく追加または変更された動的ホスト構成プロトコル (DHCP) の機能について説明します。
  
DHCP は、インターネット技術標準化委員会 (IETF) 標準であり、プライベートイントラネットなど、TCP/IP @ no__t ベースのネットワーク上でホストを構成する際の管理負担と複雑さを軽減するように設計されています。 DHCP クライアントに TCP/IP を構成するプロセスは、DHCP サーバー サービスを使うことによって自動化されます。

次のセクションでは、DHCP の新機能と機能の変更について説明します。

## <a name="dhcp-subnet-selection-options"></a>DHCP サブネットの選択オプション

DHCP では、オプション118および 82 \(sub option 5 @ no__t がサポートされるようになりました。 これらのオプションを使用すると、DHCP プロキシクライアントおよびリレーエージェントが特定のサブネットの IP アドレス、および特定の IP アドレス範囲とスコープを要求できるようになります。


Dhcp オプション82、sub @ no__t-0option 5 で構成されている DHCP リレーエージェントを使用している場合、リレーエージェントは、特定の IP アドレス範囲から DHCP クライアントの IP アドレスリースを要求できます。

詳細については、「 [DHCP サブネットの選択オプション](dhcp-subnet-options.md)」を参照してください。

## <a name="new-logging-events-for-dns-registration-failures-by-the-dhcp-server"></a>DHCP サーバーによる DNS 登録エラーの新しいログ記録イベント

DHCP には、DHCP サーバーの DNS レコードの登録が DNS サーバーで失敗する状況のログ記録イベントが含まれるようになりました。

詳細については、「 [DNS レコードの登録の DHCP ログイベント](dhcp-dns-events.md)」を参照してください。

## <a name="dhcp-nap-is-not-supported-in-windows-server-2016"></a>DHCP NAP は Windows Server 2016 ではサポートされていません

ネットワークアクセス保護 \(NAP @ no__t が Windows Server 2012 R2 で非推奨とされ、Windows Server 2016 では、DHCP サーバーの役割が NAP をサポートしなくなりました。 詳細については、「 [Windows Server 2012 R2 で削除された機能または非推奨の機能](https://technet.microsoft.com/library/dn303411.aspx)」を参照してください。  
  
NAP サポートは、windows Server 2008 で DHCP サーバーの役割に導入され、windows 10 および Windows Server 2016 より前の Windows クライアントおよびサーバーオペレーティングシステムでサポートされています。 次の表は、Windows Server での NAP のサポートをまとめたものです。  
  
|オペレーティング システム|NAP サポート|  
|--------------------|---------------|  
| Windows Server 2008 |Supported|  
| Windows Server 2008 R2 |Supported|  
| Windows Server 2012 |Supported|  
| Windows Server 2012 R2 |Supported|  
| Windows Server 2016|サポートされていません|  
  
Nap 展開では、nap をサポートするオペレーティングシステムを実行している DHCP サーバーは、nap DHCP 強制方法の NAP 強制ポイントとして機能できます。 NAP の DHCP の詳細については、「@no__t」チェックリストを参照してください。DHCP 強制設計を実装する @ no__t-0  
  
Windows Server 2016 では、DHCP サーバーは NAP ポリシーを強制しません。また、DHCP スコープを NAP @ no__t に有効にすることはできません。 また、NAP クライアントである DHCP クライアントコンピューターは、正常性ステートメント \(SoH @ no__t-1 を DHCP 要求と共に送信します。 DHCP サーバーで Windows Server 2016 が実行されている場合、これらの要求は SoH が存在しないかのように処理されます。 DHCP サーバーは、クライアントに通常の DHCP リースを付与します。 

Windows Server 2016 を実行しているサーバーがネットワークポリシーサーバーに認証要求を転送する RADIUS プロキシである場合 (NAP をサポートする @no__t 0NPS @ no__t)、これらの NAP クライアントは NPS によって NAP 以外の @ no__t 対応として評価され、NAP 処理は失敗します。
  
## <a name="see-also"></a>関連項目  
  
-   [動的ホスト構成プロトコル (DHCP)](Dynamic-Host-Configuration-Protocol--DHCP-.md)  
  

