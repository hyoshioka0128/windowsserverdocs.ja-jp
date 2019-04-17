---
ms.assetid: 026747c7-4c34-41c7-b7ea-27f9a7f64a35
title: "企業 DNS をフェデレーション サーバーのホスト (A) リソース レコードを追加します。"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 425cfe794095f1515eb3fae2f1a5e5db90ba3d00
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="add-a-host-a-resource-record-to-corporate-dns-for-a-federation-server"></a>企業 DNS をフェデレーション サーバーのホスト (A) リソース レコードを追加します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012


企業上のクライアントでは、Windows 統合認証を使用してフェデレーション サーバーに正常にアクセスするネットワーク、ホスト \(A\) リソース レコード最初に作成する必要が、アカウント フェデレーション サーバーのホスト名を解決する企業のドメイン ネーム システム \(DNS\) \ (たとえば、fs.fabrikam.com\) をフェデレーション サーバーまたはフェデレーション サーバー クラスターの IP アドレスです。 次の手順を使用すると、会社の DNS にフェデレーション サーバーをホスト \(A\) リソース レコードを追加します。  
  
メンバーシップ**管理者**、相当するものでは、この手順を完了するために必要な最低限またはします。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="to-add-a-host-a-resource-record-to-corporate-dns-for-a-federation-server"></a>会社の DNS にフェデレーション サーバーに、ホスト \(A\) リソース レコードを追加するには  
  
1.  企業ネットワークの DNS サーバー、DNS スナップインを開きます。  
  
2.  コンソール ツリーで、適切な前方参照ゾーンを右クリックしをクリックして**新しいホスト \(A or AAAA\)**します。  
  
3.  **名**、フェデレーション サーバーまたはフェデレーション サーバー クラスターのコンピューター名のみを入力たとえば、完全修飾ドメイン名を \(FQDN\) fs.fabrikam.com、種類**fs**します。  
  
4.  **IP アドレス**、フェデレーション サーバーまたはフェデレーション サーバー クラスター、192.168.1.4 などの IP アドレスを入力します。  
  
5.  をクリックして**ホストの追加**します。  
  
## <a name="additional-references"></a>その他の参照  
[チェックリスト: フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)  
  
[フェデレーション サーバーの名前解決の要件](https://technet.microsoft.com/library/dd807055.aspx)  
  

