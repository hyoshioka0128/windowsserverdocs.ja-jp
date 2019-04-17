---
title: DNS リソース レコードの管理
description: このトピックでは、Windows Server 2016 での IP アドレス管理 (IPAM) の管理ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b66c09d-e401-4f70-9a2a-6047dd629bfa
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 5ed781ef37243b80ea9da8aad27a29046b8dc8c9
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="dns-resource-record-management"></a>DNS リソース レコードの管理

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、IPAM を使用して DNS リソース レコードの管理に関する情報を提供します。  
  
> [!NOTE]  
> このトピックに加えは次の DNS リソース レコードの管理のトピックはこのセクションで利用できます。  
>   
> -   [DNS リソース レコードを追加します。](../../technologies/ipam/Add-a-DNS-Resource-Record.md)  
> -   [DNS リソース レコードを削除します。](../../technologies/ipam/Delete-DNS-Resource-Records.md)  
> -   [DNS リソース レコードのビューをフィルター処理します。](../../technologies/ipam/Filter-the-View-of-DNS-Resource-Records.md)  
> -   [特定の IP アドレスの DNS リソース レコードを表示します。](../../technologies/ipam/View-DNS-Resource-Records-for-a-Specific-IP-Address.md)  
  
## <a name="resource-record-management-overview"></a>リソース レコードの管理の概要  
Windows Server 2016 で IPAM を展開するときに、IPAM サーバーの管理コンソールに DHCP サーバーと DNS サーバーを追加するサーバーの検出を行うことができます。 IPAM サーバー、動的に DNS データを収集 6 時間おきように構成されている DNS サーバーから管理します。 IPAM では、この DNS データを保存する場所をローカル データベースを維持します。 IPAM は、1 日と時刻は次の日を知らせるだけでなく、サーバーのデータが収集された DNS サーバーからのデータ収集が実行される時間の通知を提供します。  
  
次の図に黄色のステータス バーは、IPAM 通知のユーザー インターフェイスの場所を示します。  
  
![IPAM 通知](../../media/DNS-Resource-Record-Management/ipam_DataCollection_01.jpg)  
  
収集される DNS データには、DNS ゾーンとリソース レコードの情報が含まれます。 優先 DNS サーバーからゾーン情報を収集するための IPAM を構成することができます。  IPAM では、ファイル ベースと Active Directory ゾーンを収集します。  
  
> [!NOTE]  
> IPAM では、ドメインに参加している Microsoft DNS サーバーからのみデータを収集します。 IPAM では、サード パーティの DNS サーバーと非ドメインに参加しているサーバーがサポートされていません。  
  
IPAM によって収集される DNS リソース レコードの種類の一覧を次に示します。  
  
-   AFS データベース  
  
-   ATM アドレス  
  
-   CNAME  
  
-   DHCID  
  
-   DNAME  
  
-   ホスト A または AAAA  
  
-   ホストの情報  
  
-   ISDN  
  
-   MX  
  
-   ネーム サーバー  
  
-   ポインター (PTR)  
  
-   責任者  
  
-   経由してルーティングします。  
  
-   サービスの場所  
  
-   SOA  
  
-   SRV  
  
-   テキスト  
  
-   既知のサービス  
  
-   WINS  
  
-   WINS R  
  
-   X.25  
  
Windows Server 2016 では、IPAM は、IP アドレス インベントリ、DNS ゾーン、および DNS リソース レコード間の統合を提供します。  
  
-   IPAM を使用するには、IP アドレス インベントリの DNS リソース レコードからを自動的に作成します。  
  
-   DNS の A レコードと AAAA リソースのレコードから IP アドレス インベントリを手動で作成することができます。  
  
-   特定の DNS ゾーンの DNS リソース レコードを表示し、種類、IP アドレス、リソース レコードのデータ、およびその他のフィルタ リング オプションに基づいてレコードをフィルター処理できます。  
  
-   IPAM では、IP アドレスの範囲と DNS 逆引き参照ゾーン間のマッピングが自動的に作成します。  
  
-   IPAM では、IP アドレスの逆引き参照ゾーンに存在し、その IP アドレスの範囲に含まれている PTR レコードを作成します。 必要な場合は、このマッピングも手動で変更できます。  
  
IPAM では、IPAM コンソールからリソース レコードでは、次の操作を実行することができます。  
  
-   DNS リソース レコードを作成します。  
  
-   DNS リソース レコードを編集します。  
  
-   DNS リソース レコードを削除します。  
  
-   関連するリソース レコードを作成します。  
  
IPAM では、IPAM コンソールを使用してすべての DNS 構成の変更が自動的に記録されます。  
  
## <a name="see-also"></a>参照してください。  
[IPAM を管理します。](Manage-IPAM.md)  
  


