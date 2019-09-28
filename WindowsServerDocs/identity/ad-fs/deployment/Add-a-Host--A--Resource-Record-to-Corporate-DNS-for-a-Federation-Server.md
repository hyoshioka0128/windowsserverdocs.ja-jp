---
ms.assetid: 026747c7-4c34-41c7-b7ea-27f9a7f64a35
title: 企業 DNS にフェデレーション サーバーのホスト (A) リソース レコードを追加する
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 132e71cec134d17dd73be998683c09f752fdc414
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71360333"
---
# <a name="add-a-host-a-resource-record-to-corporate-dns-for-a-federation-server"></a>企業 DNS にフェデレーション サーバーのホスト (A) リソース レコードを追加する



企業ネットワーク上のクライアントが Windows 統合認証を使用してフェデレーションサーバーに正常にアクセスできるようにするには、最初にホスト \(A @ no__t リソースレコードを会社のドメインネームシステム \(DNS @ no__t に作成し、アカウントフェデレーション @no__t サーバーのホスト名 (例: no__t @-5) を、フェデレーションサーバーまたはフェデレーションサーバークラスターの IP アドレスに指定します。 フェデレーションサーバーの企業 DNS にホスト \(A @ no__t-1 リソースレコードを追加するには、次の手順を実行します。  
  
メンバーシップ **管理者**, 、または同等の権限は、この手順を実行するために必要な最小値。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="to-add-a-host-a-resource-record-to-corporate-dns-for-a-federation-server"></a>フェデレーションサーバーの企業 DNS にホスト \(A @ no__t-1 リソースレコードを追加するには  
  
1.  企業ネットワークの DNS サーバーで、DNS スナップを開きます @ no__t-0in です。  
  
2.  コンソールツリーで、右 @ no__t をクリックして該当する前方参照ゾーンをクリックし、[**新しいホスト \(a または AAAA @ no__t**] をクリックします。  
  
3.  **[名前]** に、フェデレーションサーバーまたはフェデレーションサーバークラスターのコンピューター名のみを入力します。たとえば、完全修飾ドメイン名 \( FQDN @ no__t-2 fs.fabrikam.com には、「 **fs**」と入力します。  
  
4.  **[Ip アドレス]** に、フェデレーションサーバーまたはフェデレーションサーバークラスターの ip アドレス (たとえば、192.168.1.4) を入力します。  
  
5.  **[ホストの追加]** をクリックします。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト:フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)  
  
[フェデレーション サーバーの名前解決の要件](https://technet.microsoft.com/library/dd807055.aspx)  
  

