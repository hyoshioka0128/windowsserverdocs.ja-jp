---
title: Azure Traffic Manager を使用した Azure への高可用性のクロス地理的 AD FS デプロイ |Microsoft Docs
description: 高可用性を実現するために AD FS を Azure にデプロイする方法。
services: active-directory
author: anandyadavmsft
manager: mtillman
ms.prod: windows-server
ms.assetid: a14bc870-9fad-45ed-acd5-a90ccd432e54
ms.topic: get-started-article
ms.date: 09/01/2016
ms.author: anandy;billmath
ms.openlocfilehash: 9bfb59fadd2cf6b07d3c47ab69f0fe67974706a3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855205"
---
# <a name="high-availability-cross-geographic-ad-fs-deployment-in-azure-with-azure-traffic-manager"></a>Azure Traffic Manager を使用した Azure への高可用性の地理的な AD FS デプロイ
Azure[での AD FS デプロイ](how-to-connect-fed-azure-adfs.md)では、azure で組織の単純な AD FS インフラストラクチャをデプロイする方法について、手順を追ったガイドラインを提供します。 この記事では、azure [Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/)を使用して azure に AD FS の地理的なデプロイを作成する次の手順について説明します。 Azure Traffic Manager は、インフラストラクチャのさまざまなニーズに合わせて使用できるルーティング方法の範囲を利用することで、地理的に分散した高可用性と高パフォーマンスの AD FS インフラストラクチャを組織に作成するのに役立ちます。

可用性の高い地理的 AD FS インフラストラクチャでは、次のことが可能です。

* **単一障害点の排除:** Azure Traffic Manager のフェールオーバー機能を使用すると、世界中のデータセンターの1つがダウンした場合でも、高可用性の AD FS インフラストラクチャを実現できます。
* **パフォーマンスの向上:** この記事で推奨されているデプロイを使用して、ユーザーの認証を高速化するのに役立つ高パフォーマンス AD FS インフラストラクチャを提供できます。 

## <a name="design-principles"></a>設計原則
![全体の設計](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/blockdiagram.png)

基本的な設計原則は、「Azure でのデプロイ AD FS」に記載されている設計原則と同じです。 上の図は、別の地理的領域に対する基本的なデプロイの単純な拡張を示しています。 デプロイを新しい地理的リージョンに拡張する際に考慮すべき点を以下に示します。

* **仮想ネットワーク:** 追加の AD FS インフラストラクチャをデプロイする地理的リージョンに新しい仮想ネットワークを作成する必要があります。 上の図では、各地理的リージョンの2つの仮想ネットワークとして Geo1 VNET と Geo2 VNET が表示されています。
* **新しい地理的 VNET のドメインコントローラーと AD FS サーバー:** 新しい地理的リージョンにドメインコントローラーをデプロイすることをお勧めします。これにより、新しいリージョンの AD FS サーバーは、認証を完了するために、他のネットワーク内のドメインコントローラーに接続しなくても、パフォーマンスを向上させることができます。
* **ストレージアカウント:** ストレージアカウントは、リージョンに関連付けられています。 新しい地理的リージョンにマシンをデプロイするため、リージョンで使用する新しいストレージアカウントを作成する必要があります。  
* **ネットワークセキュリティグループ:** ストレージアカウントと同様に、リージョンで作成されたネットワークセキュリティグループを別の地理的リージョンで使用することはできません。 そのため、新しい地理的リージョンの INT および DMZ サブネットの最初の地理的リージョンに似た新しいネットワークセキュリティグループを作成する必要があります。
* **パブリック IP アドレスの DNS ラベル:** Azure Traffic Manager は、DNS ラベルを使用してのみエンドポイントを参照できます。 そのため、外部ロードバランサーのパブリック IP アドレスの DNS ラベルを作成する必要があります。
* **Azure Traffic Manager:** Microsoft Azure Traffic Manager を使用すると、世界各地のさまざまなデータセンターで実行されているサービスエンドポイントへのユーザートラフィックの分散を制御できます。 Azure Traffic Manager は DNS レベルで動作します。 DNS 応答を使用して、エンドユーザーのトラフィックをグローバルに分散されたエンドポイントに送信します。 その後、クライアントはこれらのエンドポイントに直接接続します。 パフォーマンス、重み付け、優先順位のルーティングオプションが異なるため、組織のニーズに最適なルーティングオプションを簡単に選択できます。 
* **2 つのリージョン間の仮想ネットワーク接続 (v):** 仮想ネットワーク自体が接続されている必要はありません。 各仮想ネットワークにはドメインコントローラーへのアクセス権があり、それ自体に AD FS と WAP サーバーがあるため、異なるリージョンの仮想ネットワーク間に接続しなくても動作できます。 

## <a name="steps-to-integrate-azure-traffic-manager"></a>Azure Traffic Manager を統合する手順
### <a name="deploy-ad-fs-in-the-new-geographical-region"></a>新しい地理的リージョンに AD FS をデプロイする
[Azure での AD FS デプロイ](how-to-connect-fed-azure-adfs.md)の手順とガイドラインに従って、新しい地理的リージョンに同じトポロジをデプロイします。

### <a name="dns-labels-for-public-ip-addresses-of-the-internet-facing-public-load-balancers"></a>インターネット接続 (パブリック) ロードバランサーのパブリック IP アドレスの DNS ラベル
前述のように、Azure Traffic Manager では、エンドポイントとして DNS ラベルのみを参照できるため、外部ロードバランサーのパブリック IP アドレスの DNS ラベルを作成することが重要です。 次のスクリーンショットは、パブリック IP アドレスの DNS ラベルを構成する方法を示しています。 

![DNS ラベル](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfabstsdnslabel.png)

### <a name="deploying-azure-traffic-manager"></a>Azure Traffic Manager のデプロイ
Traffic manager プロファイルを作成するには、次の手順に従います。 詳細については、「 [Azure Traffic Manager プロファイルを管理](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-manage-profiles)する」を参照してください。

1. **Traffic Manager プロファイルを作成します。** Traffic manager プロファイルに一意の名前を付けます。 このプロファイルの名前は DNS 名の一部であり、Traffic Manager のドメイン名ラベルのプレフィックスとして機能します。 名前にプレフィックスを追加/ .trafficmanager.net に DNS ラベルを、トラフィック マネージャーを作成します。 次のスクリーンショットは、mysts として設定されている traffic manager の DNS プレフィックスを示しています。その結果、DNS ラベルは mysts.trafficmanager.net になります。 
   
    ![プロファイル作成の Traffic Manager](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/trafficmanager01.png)
2. **トラフィックのルーティング方法:** Traffic manager には、次の3つのルーティングオプションを使用できます。
   
   * 優先順位 
   * パフォーマンス テスト
   * 強調
     
     応答性の高い AD FS インフラストラクチャを実現するには、**パフォーマンス**が推奨されます。 ただし、デプロイのニーズに最適なルーティング方法を選択できます。 AD FS 機能は、選択したルーティングオプションの影響を受けません。 詳細については、「 [Traffic Manager トラフィックルーティング方法](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods)」を参照してください。 上のサンプルのスクリーンショットでは、選択された**パフォーマンス**の方法を確認できます。
3. **エンドポイントを構成する:** [Traffic manager] ページで、[エンドポイント] をクリックし、[追加] を選択します。 これにより、次のスクリーンショットのような [エンドポイントの追加] ページが開きます。
   
   ![エンドポイントの構成](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfsendpoint.png)
   
   さまざまな入力については、次のガイドラインに従ってください。
   
   **種類:** Azure のパブリック IP アドレスを指すように、[Azure エンドポイント] を選択します。
   
   **名前:** エンドポイントに関連付ける名前を作成します。 これは DNS 名ではなく、DNS レコードには影響しません。
   
   **ターゲットリソースの種類:** このプロパティの値として [パブリック IP アドレス] を選択します。 
   
   **ターゲットリソース:** これにより、サブスクリプションで使用できるさまざまな DNS ラベルから選択することができます。 構成しているエンドポイントに対応する DNS ラベルを選択します。
   
   Azure Traffic Manager がトラフィックをルーティングする地理的リージョンごとにエンドポイントを追加します。
   Traffic manager でエンドポイントを追加または構成する方法の詳細と詳細な手順については、「[エンドポイントの追加、無効化、有効化、または削除](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-manage-endpoints)」を参照してください。
4. **プローブの構成:** [Traffic manager] ページで、[構成] をクリックします。 [構成] ページで、モニターの設定を HTTP ポート80と相対パス/adfs/probe でプローブに変更する必要があります。
   
    ![プローブの構成](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/mystsconfig.png) 
   
   > [!NOTE]
   > **構成が完了したら、エンドポイントの状態がオンラインになっていることを確認**します。 すべてのエンドポイントが "低下" 状態の場合、Azure Traffic Manager は、診断が正しくなく、すべてのエンドポイントに到達可能であると仮定して、トラフィックのルーティングを最適に実行します。
   > 
   > 
5. **Azure Traffic Manager の DNS レコードの変更:** フェデレーションサービスは、Azure Traffic Manager DNS 名の CNAME である必要があります。 パブリック DNS レコードに CNAME を作成して、フェデレーションサービスに到達しようとしている人が実際に Azure Traffic Manager に到達するようにします。
   
    たとえば、フェデレーションサービス fs.fabidentity.com を Traffic Manager に指定するには、DNS リソースレコードを次のように更新する必要があります。
   
    <code>fs.fabidentity.com IN CNAME mysts.trafficmanager.net</code>

## <a name="test-the-routing-and-ad-fs-sign-in"></a>ルーティングと AD FS サインインをテストする
### <a name="routing-test"></a>ルーティングテスト
ルーティングの非常に基本的なテストでは、各リージョンのコンピューターからフェデレーションサービスの DNS 名に対して ping を実行します。 選択したルーティング方法によっては、実際に ping を実行するエンドポイントが ping の表示に反映されます。 たとえば、パフォーマンスルーティングを選択した場合、クライアントのリージョンに最も近いエンドポイントに到達します。 2つの異なるリージョンクライアントコンピューターからの2つの ping のスナップショットを次に示します。1つは EastAsia region、もう1つは米国西部です。 

![ルーティングテスト](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/pingtest.png)

### <a name="ad-fs-sign-in-test"></a>AD FS サインインテスト
AD FS をテストする最も簡単な方法は、Idpinitiatedstartup.aspx ページを使用することです。 これを可能にするには、AD FS プロパティで IdpInitiatedSignOn オンを有効にする必要があります。 AD FS のセットアップを確認するには、次の手順に従います。

1. PowerShell を使用して、AD FS サーバーで次のコマンドレットを実行し、[有効] に設定します。 
   Set-adfsproperties-EnableIdPInitiatedSignonPage $true
2. 任意の外部コンピューターアクセス https://<yourfederationservicedns>/adfs/ls/IdpInitiatedSignon.aspx
3. 次のような AD FS ページが表示されます。
   
    ![ADFS テスト-認証チャレンジ](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest1.png)
   
    サインインに成功すると、次のように成功メッセージが表示されます。
   
    ![ADFS のテスト-認証の成功](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest2.png)

## <a name="related-links"></a>関連リンク
* [Azure での基本的な AD FS デプロイ](how-to-connect-fed-azure-adfs.md)
* [Microsoft Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/)
* [トラフィックルーティング方法の Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods)

## <a name="next-steps"></a>次のステップ:
* [Azure Traffic Manager プロファイルを管理する](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-manage-profiles)
* [エンドポイントの追加、無効化、有効化、または削除](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-manage-endpoints) 

