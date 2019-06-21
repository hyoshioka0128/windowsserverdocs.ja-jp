---
title: DNS リソース レコードの管理
description: このトピックでは、Windows Server 2016 での IP アドレス管理 (IPAM) の管理ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b66c09d-e401-4f70-9a2a-6047dd629bfa
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a2db802fa928a4051fbe409fc0ba60d774bb0428
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284052"
---
# <a name="dns-resource-record-management"></a>DNS リソース レコードの管理

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、IPAM を使用して DNS リソース レコードの管理についての情報を提供します。  
  
> [!NOTE]  
> このトピックに加えは次の DNS リソース レコードの管理のトピックはこのセクションで使用可能です。  
>   
> -   [DNS リソース レコードを追加します。](../../technologies/ipam/Add-a-DNS-Resource-Record.md)  
> -   [DNS リソース レコードを削除します。](../../technologies/ipam/Delete-DNS-Resource-Records.md)  
> -   [DNS リソース レコードのビューをフィルター処理します。](../../technologies/ipam/Filter-the-View-of-DNS-Resource-Records.md)  
> -   [特定の IP アドレスの DNS リソース レコードを表示します。](../../technologies/ipam/View-DNS-Resource-Records-for-a-Specific-IP-Address.md)  
  
## <a name="resource-record-management-overview"></a>リソース レコードの管理の概要  
Windows Server 2016 での IPAM を展開するときに、IPAM サーバーの管理コンソールに DHCP および DNS サーバーを追加するサーバーの検出を行うことができます。 IPAM サーバー、動的に DNS からデータを収集 6 時間ごとに構成されている DNS サーバーを管理します。 IPAM では、この DNS データを格納する場所のローカル データベースを保持します。 IPAM は、1 日と、次の日を示すと、サーバーのデータが収集された時刻が DNS サーバーからのデータ収集の発生時の通知を提供します。  
  
次の図に黄色のステータス バーには、IPAM の通知のユーザー インターフェイスの場所が表示されます。  
  
![IPAM 通知](../../media/DNS-Resource-Record-Management/ipam_DataCollection_01.jpg)  
  
収集された DNS データには、DNS ゾーンとリソース レコードの情報が含まれます。 優先 DNS サーバーからゾーンの情報を収集するための IPAM を構成することができます。  IPAM では、ファイル ベースと Active Directory ゾーンを収集します。  
  
> [!NOTE]  
> IPAM では、ドメインに参加している Microsoft DNS サーバーからのみデータを収集します。 IPAM では、サード パーティの DNS サーバーとドメイン非参加のサーバーがサポートされていません。  
  
IPAM によって収集される DNS リソース レコードの種類の一覧を次に示します。  
  
-   AFS データベース  
  
-   ATM アドレス  
  
-   CNAME  
  
-   DHCID  
  
-   DNAME  
  
-   ホスト A または AAAA  
  
-   ホスト情報  
  
-   ISDN  
  
-   MX  
  
-   ネーム サーバー  
  
-   ポインター (PTR)  
  
-   責任者  
  
-   経由でルーティングします。  
  
-   サービスの場所  
  
-   SOA  
  
-   SRV  
  
-   Text  
  
-   既知のサービス  
  
-   WINS  
  
-   WINS R  
  
-   X.25  
  
Windows Server 2016 では、IPAM は、IP アドレス インベントリ、DNS ゾーンと DNS リソース レコードとの統合を提供します。  
  
-   IPAM を使用すると、自動的に DNS リソース レコードからの IP アドレス インベントリを作成します。  
  
-   IP アドレス インベントリは、DNS A レコードと AAAA のリソース レコードを手動で作成できます。  
  
-   特定の DNS ゾーンの DNS リソース レコードを表示し、種類、IP アドレス、リソース レコードのデータ、およびその他のフィルター処理オプションに基づいてレコードをフィルター処理できます。  
  
-   IPAM では、IP アドレスの範囲と DNS 逆引き参照ゾーン間のマッピングが自動的に作成されます。  
  
-   IPAM では、逆引き参照ゾーンに存在し、その IP アドレスの範囲に含まれている PTR レコードの IP アドレスを作成します。 必要な場合にも手動で、このマッピングを変更することができます。  
  
IPAM では、IPAM コンソールからリソース レコードに対して次の操作を実行できます。  
  
-   DNS リソース レコードを作成します。  
  
-   DNS リソース レコードを編集します。  
  
-   DNS リソース レコードの削除  
  
-   関連付けられたリソース レコードを作成します。  
  
IPAM は、IPAM コンソールを使用してすべての DNS 構成変更を自動的に記録します。  
  
## <a name="see-also"></a>関連項目  
[IPAM の管理](Manage-IPAM.md)  
  


