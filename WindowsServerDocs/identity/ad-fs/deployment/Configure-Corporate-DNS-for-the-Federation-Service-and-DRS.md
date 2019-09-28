---
ms.assetid: aca4a4fa-b12c-4eed-a499-f9aedb7d2fd6
title: 企業 DNS をフェデレーション サービスと DRS 用に構成する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 9f0b04f9dc050117fdefc630759c86d2b1bb1ecc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408445"
---
# <a name="configure-corporate-dns-for-the-federation-service-and-drs"></a>企業 DNS をフェデレーション サービスと DRS 用に構成する
  
## <a name="step-6-add-a-host-a-and-alias-cname-resource-record-to-corporate-dns-for-the-federation-service-and-drs"></a>手順 6:ホスト \(A @ no__t-1 と Alias \(CNAME @ no__t リソースレコードをフェデレーションサービスと DRS の企業 DNS に追加します。  
前の手順で構成したフェデレーションサービスとデバイス登録サービスについて、次のリソースレコードを会社のドメインネームシステム \(DNS @ no__t に追加する必要があります。  
  
|入力|種類|Address|  
|---------|--------|-----------|  
|フェデレーション @ no__t-0service @ no__t-1name|Host \(A @ no__t-1|AD FS サーバーの IP アドレス、または AD FS サーバーファームの前に構成されているロードバランサーの IP アドレス|  
|enterpriseregistration|エイリアス \(CNAME @ no__t|フェデレーション @ no__t-0server\_name.contoso.com|  
  
次の手順を使用して、ホスト \(A @ no__t-1 とエイリアス \(CNAME @ no__t リソースレコードをフェデレーションサーバーとデバイス登録サービスの企業 DNS に追加できます。  
  
この手順を実行するには、 **Administrators**のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
#### <a name="to-add-a-host-a-and-alias-cname-resource-records-to-dns-for-your-federation-server"></a>ホスト \(A @ no__t-1 とエイリアス \(CNAME @ no__t リソースレコードをフェデレーションサーバーの DNS に追加するには  
  
1.  ドメインコントローラーのサーバーマネージャーで、 **[ツール]** メニューの **[dns]** をクリックして、の dns スナップ @ no__t-2in 開きます。  
  
2.  コンソールツリーで、 **[ドメイン @ no__t-1controller @ no__t-2name]** ノード、 **[前方参照ゾーン]** の順に展開します。次に、 **[ドメイン @ no__t-6]** を右クリックし、[**新しいホスト \(a または AAAA @ no__t-9**] をクリックします。  
  
3.  **[名前]** ボックスに、AD FS ファームに使用する名前を入力します。  
  
4.  **[IP アドレス]** ボックスに、フェデレーション サーバーの IP アドレスを入力します。 **[ホストの追加]** をクリックします。  
  
5.  Right @ no__t- **0click @ no__t-2name**ノードをクリックし、[ **New ALIAS \(cname @ no__t-5**] をクリックします。  
  
6.  **[新しいリソース レコード]** ダイアログ ボックスで、 **[エイリアス名]** ボックスに「**enterpriseregistration**」と入力します。  
  
7.  完全修飾ドメイン名 \(FQDN @ no__t-1 [ターゲットホスト] ボックスに「 **federation @ no__t-3service @ no__t-4farm @ no__t-5name. ドメイン @ no__t-6name .com**」と入力し、[ **OK]** をクリックします。  
  
    > [!IMPORTANT]  
    > 実際の展開では、会社に複数のユーザープリンシパル名 \(UPN @ no__t サフィックスがある場合、DNS 内の各 UPN サフィックスに対して複数の CNAME レコードを作成する必要があります。  
  
## <a name="see-also"></a>関連項目 

[AD FS 展開](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 展開ガイド](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[フェデレーション サーバー ファームの展開](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

