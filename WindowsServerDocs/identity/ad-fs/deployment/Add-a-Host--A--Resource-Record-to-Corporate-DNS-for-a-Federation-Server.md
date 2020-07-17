---
ms.assetid: 026747c7-4c34-41c7-b7ea-27f9a7f64a35
title: 企業 DNS にフェデレーション サーバーのホスト (A) リソース レコードを追加する
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 47d619803133a29bd0217b738577c93522f1ab59
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80815025"
---
# <a name="add-a-host-a-resource-record-to-corporate-dns-for-a-federation-server"></a>企業 DNS にフェデレーション サーバーのホスト (A) リソース レコードを追加する



企業ネットワーク上のクライアントが Windows 統合認証を使用してフェデレーションサーバーに正常にアクセスできるようにするには、まず、アカウントフェデレーションサーバーのホスト名 (たとえば、fs.fabrikam.com \(をフェデレーションサーバーまたはフェデレーションサーバークラスターの IP アドレスに解決するための DNS\) \(、\) リソースレコードのホスト \(を作成する必要があります。\) 次の手順を使用して、\) リソースレコード \(ホストをフェデレーションサーバーの企業 DNS に追加できます。  
  
**Administrators**、またはそれと同等のメンバーシップが、この手順を実行するために最低限必要なメンバーシップです。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="to-add-a-host-a-resource-record-to-corporate-dns-for-a-federation-server"></a>フェデレーションサーバーの企業 DNS に\) リソースレコード \(ホストを追加するには  
  
1.  企業ネットワークの DNS サーバーで、の DNS スナップ\-を開きます。  
  
2.  コンソールツリーで、該当する前方参照ゾーンを右\-クリックし、[**新しいホスト \(A または AAAA\)** ] をクリックします。  
  
3.  **[名前]** に、フェデレーションサーバーまたはフェデレーションサーバークラスターのコンピューター名のみを入力します。たとえば、完全修飾ドメイン名 \(FQDN\) fs.fabrikam.com の場合は、「 **fs**」と入力します。  
  
4.  **[Ip アドレス]** に、フェデレーションサーバーまたはフェデレーションサーバークラスターの ip アドレス (たとえば、192.168.1.4) を入力します。  
  
5.  **[ホストの追加]** をクリックします。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト: フェデレーションサーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)  
  
[フェデレーション サーバーの名前解決の要件](https://technet.microsoft.com/library/dd807055.aspx)  
  

