---
title: Azure Traffic Manager を使用した高可用性地域間 AD FS デプロイ |Microsoft Docs
description: このドキュメントでは、高可用性を Azure に AD FS をデプロイする方法を学びます。
keywords: Azure traffic manager、Azure Traffic Manager、地理的な複数のデータ センター、データ センターの地理的な複数の地理的なデータ センターを使用した adfs での ad fs が azure での AD FS を展開、azure adfs, azure adfs, azure の ad fs をデプロイ、adfs のデプロイ、ad fs、azure では、adfs の展開ad fs をデプロイする azure では、azure, adfs azure, AD FS, Azure, azure で iaas、ADFS、AD FS の概要で AD FS を展開する ad fs を azure に移行
services: active-directory
documentationcenter: ''
author: anandyadavmsft
manager: mtillman
editor: ''
ms.assetid: a14bc870-9fad-45ed-acd5-a90ccd432e54
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/01/2016
ms.author: anandy;billmath
ms.openlocfilehash: 4af0386ef97694baa9ba7f1e5e7163554d79734a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874123"
---
# <a name="high-availability-cross-geographic-ad-fs-deployment-in-azure-with-azure-traffic-manager"></a>Azure Traffic Manager での高可用性地域間 AD FS のデプロイ
[Azure での AD FS デプロイ](how-to-connect-fed-azure-adfs.md)組織は、Azure での単純な AD FS インフラストラクチャをデプロイする方法についてステップ バイ ステップのガイドラインを提供します。 この記事では、次の手順を使用して Azure で地域間 AD FS の展開を作成する[Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/)します。 Azure Traffic Manager での地理的に拡散の高可用性と、組織の AD FS インフラストラクチャの高パフォーマンスの作成に役立つ、インフラストラクチャからさまざまなニーズに合わせて使用可能なルーティング方法の範囲を使用します。

地域間 AD FS インフラストラクチャを高可用性が有効にします。

* **単一障害点を排除します。** Azure Traffic Manager のフェールオーバー機能を世界中の一部のデータ センターのいずれかがダウンした場合でも、高可用性 AD FS インフラストラクチャを実現できます。
* **パフォーマンスの向上:** この記事で推奨しているデプロイを使用すると、ユーザーの認証を高速化に役立つ高性能な AD FS インフラストラクチャを提供します。 

## <a name="design-principles"></a>設計原則
![全体的な設計](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/blockdiagram.png)

基本的な設計原則は Azure での AD FS のデプロイの記事では設計の原則に記載されている同じになります。 上記の図は、別の地理的リージョンに基本的な展開の単純な拡張機能を示しています。 新しい地理的リージョンにデプロイを拡張するときに考慮すべきいくつかの点を次に示します

* **仮想ネットワーク:** 追加の AD FS インフラストラクチャをデプロイする地理的リージョンに新しい仮想ネットワークを作成する必要があります。 上記の図では、地理的リージョンごとに 2 つの仮想ネットワークとして Geo1 VNET ともう一方に Geo2 VNET を参照してください。
* **ドメイン コント ローラーと新しい地域の VNET 内の AD FS サーバー:** 認証とパフォーマンスが向上を完了するネットワーク、新しいリージョンでの AD FS サーバーは遠く離れた別のドメイン コント ローラーに接続する必要があるないように、新しい地理的リージョン内のコント ローラーのドメインを展開することをお勧めします。
* **ストレージ アカウント:** ストレージ アカウントは、リージョンに関連付けられます。 新しい地理的リージョン内のマシンをデプロイするため、リージョンで使用する新しいストレージ アカウントを作成する必要があります。  
* **ネットワーク セキュリティ グループ:** ストレージ アカウント、ネットワーク セキュリティ グループのリージョンに作成は、別の地理的リージョンで使用することはできません。 そのため、新しいネットワーク セキュリティ グループを作成 INT と DMZ サブネットの最初の地理的リージョン内と同様、新しい地理的リージョンにする必要があります。
* **パブリック IP アドレスの DNS ラベル:** Azure Traffic Manager はエンドポイントを参照できますのみ DNS ラベルを利用します。 そのため、外部ロード バランサーのパブリック IP アドレスの DNS ラベルを作成することを求められます。
* **Azure Traffic Manager:** Microsoft Azure Traffic Manager を使用すると、世界各地のデータ センターで実行されているサービス エンドポイントへのユーザー トラフィックの分散を制御できます。 Azure Traffic Manager は DNS レベルで動作します。 DNS 応答をグローバルに分散されたエンドポイントにエンドユーザーのトラフィックに使用します。 クライアントからそれらのエンドポイントに直接接続します。 パフォーマンス、重み付けと優先順位の異なるルーティング オプションと、組織のニーズに最適なルーティング オプションを簡単に選択できます。 
* **V net への vnet 間接続 2 つのリージョン間:** 自体が仮想ネットワーク間の接続確立する必要はありません。 各仮想ネットワークでは、ドメイン コント ローラーにアクセスして、AD FS および WAP サーバーをそれ自体が後、は、異なるリージョン内の仮想ネットワーク間の接続を使用しない作業できます。 

## <a name="steps-to-integrate-azure-traffic-manager"></a>Azure Traffic Manager を統合する手順
### <a name="deploy-ad-fs-in-the-new-geographical-region"></a>新しい地理的リージョン内の AD FS を展開します。
次の手順とガイドライン[Azure での AD FS デプロイ](how-to-connect-fed-azure-adfs.md)新しい地理的リージョンに同じトポロジをデプロイします。

### <a name="dns-labels-for-public-ip-addresses-of-the-internet-facing-public-load-balancers"></a>インターネット接続 (パブリック) ロード バランサーのパブリック IP アドレスの DNS ラベル
前述のように、Azure Traffic Manager のみエンドポイントとして DNS ラベルを参照でき、したがって外部ロード バランサーのパブリック IP アドレスの DNS ラベルを作成する必要はします。 次のスクリーン ショットには、パブリック IP アドレスの DNS ラベルを構成する方法を示します。 

![DNS ラベル](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfabstsdnslabel.png)

### <a name="deploying-azure-traffic-manager"></a>Azure Traffic Manager を展開します。
Traffic manager プロファイルを作成するのには、次の手順に従います。 詳細については、参照することもを[Azure Traffic Manager プロファイルの管理](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-manage-profiles)します。

1. **Traffic Manager プロファイルを作成します。** Traffic manager プロファイルの一意な名前を付けます。 プロファイルのこの名前の DNS 名の一部であり、Traffic Manager ドメイン名のラベルのプレフィックスとして機能します。 名前にプレフィックスを追加/。.trafficmanager.net に DNS ラベルを、トラフィック マネージャーを作成します。 次のスクリーン ショット、traffic manager DNS プレフィックスがためとして設定されると、結果として得られる DNS ラベルは mysts.trafficmanager.net になります。 
   
    ![Traffic Manager プロファイルの作成](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/trafficmanager01.png)
2. **トラフィック ルーティング方法。** 次の 3 つのルーティング オプションを traffic manager で利用できるがあります。
   
   * Priority 
   * パフォーマンス
   * 重み付け
     
     **パフォーマンス**は応答性の高い AD FS インフラストラクチャを実現するために推奨されるオプションです。 ただし、展開のニーズに最適なルーティング方法を選択できます。 AD FS 機能は、選択したルーティング オプションの影響は受けません。 参照してください[Traffic Manager のトラフィック ルーティング方法](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods)詳細についてはします。 サンプルで上記のスクリーン ショットを確認できます、**パフォーマンス**メソッドを選択します。
3. **エンドポイントを構成します。** トラフィック マネージャー ページで、エンドポイント をクリックし、追加を選択します。 次のスクリーン ショットのような追加のエンドポイント ページが開きます
   
   ![エンドポイントの構成](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfsendpoint.png)
   
   さまざまな入力では、次のガイドラインに従います。
   
   **種類:** Azure のパブリック IP アドレスを指していますが、Azure エンドポイントを選択します。
   
   **名前:** エンドポイントに関連付ける名前を作成します。 これは DNS 名と DNS レコードに影響を与えません。
   
   **ターゲット リソースの種類:** このプロパティの値としてパブリック IP アドレスを選択します。 
   
   **ターゲット リソース:** 自分のサブスクリプションがある使用可能な別の DNS ラベルから選択するオプションが提供されます。 構成しているエンドポイントに対応する DNS ラベルを選択します。
   
   Azure Traffic Manager でにトラフィックをルーティングする地理的リージョンごとのエンドポイントを追加します。
   詳細と traffic manager でエンドポイントを構成および追加する方法の詳細な手順についてを参照してください[エンドポイントの追加、無効化、有効化または削除](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-manage-endpoints)
4. **プローブを構成します。** Traffic manager のページでは、構成をクリックします。 [構成] ページで、HTTP ポート 80 と相対パス/adfs/probe でプローブするモニターの設定を変更する必要があります。
   
    ![プローブを構成します。](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/mystsconfig.png) 
   
   > [!NOTE]
   > **エンドポイントの状態がオンラインである構成が完了することを確認**します。 すべてのエンドポイントが「低下」状態である場合は、Azure Traffic Manager は、診断に誤りがあり、すべてのエンドポイントが到達できるトラフィックの想定をルーティングする最善の試みを行います。
   > 
   > 
5. **Azure Traffic Manager の DNS レコードを変更します。** フェデレーション サービスは、Azure Traffic Manager DNS 名を CNAME にあります。 Azure Traffic Manager が実際にまですべてのユーザーがフェデレーション サービスに到達しようように、パブリック DNS レコードで CNAME を作成します。
   
    たとえば、Traffic Manager に、フェデレーション サービス fs.fabidentity.com をポイントするは、次のように、DNS リソース レコードを更新する必要があります。
   
    <code>fs.fabidentity.com IN CNAME mysts.trafficmanager.net</code>

## <a name="test-the-routing-and-ad-fs-sign-in"></a>ルーティングをテストし、AD FS のサインイン
### <a name="routing-test"></a>ルーティング テスト
ルーティングの非常に基本的なテストは、各地理的リージョン内のマシンからのフェデレーション サービスの DNS 名に対して ping することです。 によって選択したルーティング方法、実際に ping を実行するエンドポイントを ping 表示で反映されます。 たとえば、パフォーマンス ルーティングを選択した場合クライアントのリージョンに最も近いエンドポイントに到達します。 EastAsia のリージョンと米国西部の 2 つの異なるリージョンのクライアント コンピューターから 2 つの ping のスナップショットを次に示します。 

![ルーティング テスト](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/pingtest.png)

### <a name="ad-fs-sign-in-test"></a>AD FS のサインイン テスト
AD FS をテストする最も簡単な方法は、IdpInitiatedSignon.aspx ページを使用してです。 AD FS のプロパティで IdpInitiatedSignOn を有効にする必要があることを実行するにです。 AD FS の設定を確認するのには、次の手順に従います

1. 実行、以下の設定に有効な PowerShell を使用して、AD FS サーバーでコマンドレット。 
   Set-adfsproperties EnableIdPInitiatedSignonPage $true
2. 任意の外部のコンピューター アクセス https:// から<yourfederationservicedns>/adfs/ls/IdpInitiatedSignon.aspx
3. AD FS ページが表示する次のような。
   
    ![ADFS のテスト - 認証チャレンジ](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest1.png)
   
    成功したサインインには、成功メッセージを次に示すよう。
   
    ![ADFS のテスト - 認証の成功](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest2.png)

## <a name="related-links"></a>関連リンク
* [Azure で基本的な AD FS の展開](how-to-connect-fed-azure-adfs.md)
* [Microsoft Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/)
* [Traffic Manager のトラフィック ルーティング方法](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods)

## <a name="next-steps"></a>次のステップ
* [Azure Traffic Manager プロファイルを管理します。](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-manage-profiles)
* [追加、無効化、有効にする、またはエンドポイントを削除します](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-manage-endpoints) 

