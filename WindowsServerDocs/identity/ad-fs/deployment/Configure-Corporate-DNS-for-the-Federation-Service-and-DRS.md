---
ms.assetid: aca4a4fa-b12c-4eed-a499-f9aedb7d2fd6
title: "フェデレーション サービスと DRS 用に会社の DNS を構成します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 9b66bed99cbc2ac2cdf116579adaea282c45fabe
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="configure-corporate-dns-for-the-federation-service-and-drs"></a>フェデレーション サービスと DRS 用に会社の DNS を構成します。

>適用対象: Windows Server 2016、Windows Server 2012 R2
  
## <a name="step-6-add-a-host-a-and-alias-cname-resource-record-to-corporate-dns-for-the-federation-service-and-drs"></a>手順 6: ホストの追加を企業の DNS にフェデレーション サービスと DRS \(A\) とエイリアスの \(CNAME\) リソース レコード  
フェデレーション サービスの企業のドメイン ネーム システム \(DNS\) と前の手順で構成されているデバイス登録サービスを次のリソース レコードを追加する必要があります。  
  
|エントリ|種類|アドレス|  
|---------|--------|-----------|  
|federation\_service\_name|\(A\) のホスト|AD FS サーバーまたは AD FS サーバー ファームの前に構成されているロード バランサーの IP アドレスの IP アドレス|  
|enterpriseregistration|エイリアス \(CNAME\)|federation\_server\_name.contoso.com|  
  
会社の DNS にフェデレーション サーバーおよびデバイス登録サービスにホスト \(A\) とエイリアス \(CNAME\) リソース レコードを追加するのに、次の手順を使用することができます。  
  
メンバーシップ**管理者**、またはそれと同等が最小要件を次の手順を完了します。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
#### <a name="to-add-a-host-a-and-alias-cname-resource-records-to-dns-for-your-federation-server"></a>フェデレーション サーバーの DNS にホスト \(A\) とエイリアス \(CNAME\) リソース レコードを追加するには  
  
1.  ドメイン コント ローラーで、サーバー マネージャーで、上、**ツール**] メニューのをクリックして**DNS** 、DNS スナップインを開きます。  
  
2.  コンソール ツリーで、展開、 **domain\_controller\_name** ] ノードを展開**前方参照ゾーン**、右クリック**domain\_name**、] をクリックし、**新しいホスト \(A or AAAA\)**します。  
  
3.  **名**ボックスに、AD FS ファームに使用する名前を入力します。  
  
4.  **IP アドレス**ボックスに、フェデレーション サーバーの IP アドレスを入力します。 をクリックして**ホストの追加**します。  
  
5.  右クリック、 **domain\_name**ノード、およびクリック**新しいエイリアス \(CNAME\)**します。  
  
6.  **新しいリソース レコード**] ダイアログ ボックスで、「 **enterpriseregistration**で、**エイリアス名**ボックス。  
  
7.  完全修飾ドメイン名をターゲット ホスト ボックスの種類の \(FQDN\) **federation\_service\_farm\_name.domain\_name.com**、] をクリックし、 **OK**します。  
  
    > [!IMPORTANT]  
    > 現実の世界展開では、複数のユーザー プリンシパル名 \(UPN\) サフィックスがある企業作成する必要が複数の CNAME レコード DNS 内の各 UPN サフィックスごと。  
  
## <a name="see-also"></a>参照してください。 

[AD FS の展開](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 展開ガイドします。](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[フェデレーション サーバー ファームを展開します。](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

