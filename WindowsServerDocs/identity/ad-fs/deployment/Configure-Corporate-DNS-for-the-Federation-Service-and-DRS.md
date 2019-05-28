---
ms.assetid: aca4a4fa-b12c-4eed-a499-f9aedb7d2fd6
title: 企業 DNS をフェデレーション サービスと DRS 用に構成する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: cd8febf9eff300b1a83d22828874b4a577b8af36
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192320"
---
# <a name="configure-corporate-dns-for-the-federation-service-and-drs"></a>企業 DNS をフェデレーション サービスと DRS 用に構成する
  
## <a name="step-6-add-a-host-a-and-alias-cname-resource-record-to-corporate-dns-for-the-federation-service-and-drs"></a>手順 6:ホストの追加\(A\)とエイリアス\(CNAME\)をフェデレーション サービスおよび DRS の会社の DNS リソース レコード  
会社のドメイン ネーム システムに次のリソース レコードを追加する必要があります\(DNS\) federation service と前の手順で構成されているデバイス登録サービス。  
  
|入力|種類|Address|  
|---------|--------|-----------|  
|フェデレーション\_サービス\_名|ホスト\(A\)|AD FS サーバーまたは AD FS サーバー ファームの前に構成されているロード バランサーの IP アドレスの IP アドレス|  
|enterpriseregistration|エイリアス\(CNAME\)|フェデレーション\_server\_name.contoso.com|  
  
次の手順を使用するには、ホストを追加する\(A\)とエイリアス\(CNAME\)リソース レコードを会社の DNS にフェデレーション サーバーとデバイス登録サービス。  
  
メンバーシップ**管理者**、またはそれと同等がこの手順を実行する最小要件です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
#### <a name="to-add-a-host-a-and-alias-cname-resource-records-to-dns-for-your-federation-server"></a>ホストを追加する\(A\)とエイリアス\(CNAME\)フェデレーション サーバーの dns リソース レコード  
  
1.  ドメイン コント ローラーで、サーバー マネージャーで、上、**ツール** メニューのをクリックして**DNS** DNS スナップインを開く\-で。  
  
2.  コンソール ツリーで、展開、**ドメイン\_コント ローラー\_名前**ノード、展開**前方参照ゾーン**、右\-クリックして**ドメイン\_名前**、 をクリックし、**新しいホスト\(A または AAAA\)** します。  
  
3.  **名前**ボックスに、AD FS ファーム用に使用する名前を入力します。  
  
4.  **[IP アドレス]** ボックスに、フェデレーション サーバーの IP アドレスを入力します。 **[ホストの追加]** をクリックします。  
  
5.  右\- をクリックして、**ドメイン\_名前**ノード、およびクリック**新しいエイリアス\(CNAME\)** します。  
  
6.  **[新しいリソース レコード]** ダイアログ ボックスで、 **[エイリアス名]** ボックスに「**enterpriseregistration**」と入力します。  
  
7.  完全修飾ドメイン名で\(FQDN\) 、ターゲット ホスト ボックスの次のように入力します**フェデレーション\_サービス\_ファーム\_name.domain\_名.com**、し、。クリックして**OK**します。  
  
    > [!IMPORTANT]  
    > 現実世界のデプロイで複数のユーザー プリンシパル名がある企業\(UPN\)サフィックス、DNS の UPN サフィックスのごとに複数の CNAME レコードを作成する必要があります。  
  
## <a name="see-also"></a>関連項目 

[AD FS 展開](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 展開ガイドします。](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[フェデレーション サーバー ファームの展開](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

