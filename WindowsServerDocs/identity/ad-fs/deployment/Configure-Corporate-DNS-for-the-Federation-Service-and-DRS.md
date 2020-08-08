---
ms.assetid: aca4a4fa-b12c-4eed-a499-f9aedb7d2fd6
title: 企業 DNS をフェデレーション サービスと DRS 用に構成する
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: de0313a65234c637018b0c7b2d7a7c9212464077
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87938430"
---
# <a name="configure-corporate-dns-for-the-federation-service-and-drs"></a>企業 DNS をフェデレーション サービスと DRS 用に構成する

## <a name="step-6-add-a-host-a-and-alias-cname-resource-record-to-corporate-dns-for-the-federation-service-and-drs"></a>手順 6: \( \) \( フェデレーションサービスと DRS のホスト a とエイリアス CNAME \) リソースレコードを会社の DNS に追加する
\( \) 前の手順で構成したフェデレーションサービスとデバイス登録サービスの企業ドメインネームシステム DNS には、次のリソースレコードを追加する必要があります。

|入力|種類|Address|
|---------|--------|-----------|
|フェデレーション \_ サービス \_ 名|ホスト \( A\)|AD FS サーバーの IP アドレス、または AD FS サーバーファームの前に構成されているロードバランサーの IP アドレス|
|enterpriseregistration|エイリアス \( CNAME\)|フェデレーション \_ サーバー \_ name.contoso.com|

ホスト \( a \) とエイリアス \( CNAME \) リソースレコードをフェデレーションサーバーとデバイス登録サービスの企業 DNS に追加するには、次の手順を実行します。

この手順を実行するには、 **Administrators**のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。  適切なアカウントおよびグループメンバーシップの使用方法の詳細については、「[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)」を参照してください。

#### <a name="to-add-a-host-a-and-alias-cname-resource-records-to-dns-for-your-federation-server"></a>ホスト \( a \) とエイリアス \( CNAME \) リソースレコードをフェデレーションサーバーの DNS に追加するには

1.  ドメインコントローラーで、サーバーマネージャーの [**ツール**] メニューの [ **dns** ] をクリックし、dns スナップインを開き \- ます。

2.  コンソールツリーで、[**ドメイン \_ コントローラー \_ 名**] ノード、[**前方参照ゾーン**] の順に展開し、[ \- **ドメイン \_ 名**] を右クリックして、[**新しいホスト \( A または \) AAAA**] をクリックします。

3.  [**名前**] ボックスに、AD FS ファームに使用する名前を入力します。

4.  **[IP アドレス]** ボックスに、フェデレーション サーバーの IP アドレスを入力します。 **[ホストの追加]** をクリックします。

5.  [ \- **ドメイン \_ 名**] ノードを右クリックし、[**新しい \( エイリアス \) CNAME**] をクリックします。

6.  **[新しいリソース レコード]** ダイアログ ボックスで、**[エイリアス名]** ボックスに「**enterpriseregistration**」と入力します。

7.  [ \( ターゲットホスト] ボックスの完全修飾ドメイン名 FQDN に \) 「**フェデレーション \_ サービス \_ ファーム \_ 名. ドメイン \_ Name.com**」と入力し、[ **OK]** をクリックします。

    > [!IMPORTANT]
    > 実際の展開では、会社に複数のユーザープリンシパル名の upn サフィックスがある場合、 \( \) DNS 内の各 upn サフィックスに対して複数の CNAME レコードを作成する必要があります。

## <a name="see-also"></a>参照

[AD FS 展開](../../ad-fs/AD-FS-Deployment.md)

[Windows Server 2012 R2 AD FS の展開ガイド](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)

[フェデレーション サーバー ファームの展開](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)


