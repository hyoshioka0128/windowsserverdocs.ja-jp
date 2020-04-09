---
ms.assetid: aca4a4fa-b12c-4eed-a499-f9aedb7d2fd6
title: 企業 DNS をフェデレーション サービスと DRS 用に構成する
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 3e3f2b36b7949e4bbde78942006e985f41abf9df
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80814266"
---
# <a name="configure-corporate-dns-for-the-federation-service-and-drs"></a>企業 DNS をフェデレーション サービスと DRS 用に構成する
  
## <a name="step-6-add-a-host-a-and-alias-cname-resource-record-to-corporate-dns-for-the-federation-service-and-drs"></a>手順 6:\) とエイリアス \(CNAME\) リソースレコードを \(して、フェデレーションサービスと DRS の企業 DNS にホストを追加する  
前の手順で構成したフェデレーションサービスとデバイス登録サービスの \(DNS\) に、次のリソースレコードを追加する必要があります。  
  
|エントリ|種類|Address|  
|---------|--------|-----------|  
|フェデレーション\_サービス\_名|\) \(ホスト|AD FS サーバーの IP アドレス、または AD FS サーバーファームの前に構成されているロードバランサーの IP アドレス|  
|enterpriseregistration|\(CNAME\) のエイリアス|フェデレーション\_サーバー\_name.contoso.com|  
  
次の手順を使用して、\) とエイリアス \(CNAME\) リソースレコードのホスト \(、フェデレーションサーバーとデバイス登録サービスの企業 DNS に追加できます。  
  
この手順を実行するには、 **Administrators**のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
#### <a name="to-add-a-host-a-and-alias-cname-resource-records-to-dns-for-your-federation-server"></a>ホスト \(\) とエイリアス \(CNAME\) リソースレコードをフェデレーションサーバーの DNS に追加するには  
  
1.  ドメインコントローラーのサーバーマネージャーで、 **[ツール]** メニューの **[dns]** をクリックして、の dns スナップ\-を開きます。  
  
2.  コンソールツリーで、[**ドメイン\_コントローラー\_名**] ノード、 **[前方参照ゾーン]** の順に展開し\-[**ドメイン\_名**] を右クリックし、[**新しいホスト \(A または AAAA\)** ] をクリックします。  
  
3.  **[名前]** ボックスに、AD FS ファームに使用する名前を入力します。  
  
4.  **[IP アドレス]** ボックスに、フェデレーション サーバーの IP アドレスを入力します。 **[ホストの追加]** をクリックします。  
  
5.  右\-[**ドメイン\_名**] ノードをクリックし、[**新しいエイリアス \(CNAME\)** ] をクリックします。  
  
6.  **[新しいリソース レコード]** ダイアログ ボックスで、 **[エイリアス名]** ボックスに「**enterpriseregistration**」と入力します。  
  
7.  [ターゲットホスト] ボックスの完全修飾ドメイン名 \(FQDN\) で、「**フェデレーション\_サービス\_ファーム\_名前. domain\_name.com**」と入力し、[ **OK]** をクリックします。  
  
    > [!IMPORTANT]  
    > 実際の展開では、会社に複数のユーザープリンシパル名 \(UPN\) サフィックスがある場合は、DNS の各 UPN サフィックスに対して複数の CNAME レコードを作成する必要があります。  
  
## <a name="see-also"></a>参照 

[AD FS 展開](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 展開ガイド](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[フェデレーション サーバー ファームの展開](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

