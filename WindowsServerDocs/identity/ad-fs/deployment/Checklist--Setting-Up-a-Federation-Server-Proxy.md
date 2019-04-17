---
ms.assetid: 38c9bcd3-c6f8-4153-8e42-5fd31568c65a
title: "フェデレーション サーバー プロキシのセットアップのチェックリスト-"
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 997ee901172eb2d873ad02fa8ce39da09c5171c7
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="checklist-setting-up-a-federation-server-proxy"></a>チェックリスト: フェデレーション サーバー プロキシのセットアップ

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このチェックリストには、Active Directory フェデレーション サービス \(AD FS\) でフェデレーション サーバー プロキシの役割用の Windows Server® 2012 を実行するサーバーを準備するための展開タスクが含まれます。  
  
> [!NOTE]  
> 順序でこのチェックリストのタスクを完了します。 参照リンクでは、手順には、このトピックに戻りできるように、このチェックリストの残りのタスクを続行することができます、その手順の手順を完了します。  
  
![フェデレーション プロキシ サーバーのセットアップ](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**チェックリスト: フェデレーション サーバー プロキシのセットアップ**  
  
||タスク|リファレンス|  
|-|--------|-------------|  
|![フェデレーション プロキシ サーバーのセットアップ](media/icon_checkboxo.gif)|AD FS フェデレーション サーバー プロキシの展開を開始する前に、AD FS 展開トポロジの種類とそれに関連付けられているサーバーの配置とネットワーク レイアウトの推奨事項を確認します。|![フェデレーション プロキシ サーバーのセットアップ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 展開トポロジの決定](https://technet.microsoft.com/library/gg982491.aspx)<br /><br />![フェデレーション プロキシ サーバーのセットアップ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション サーバー プロキシの配置の計画](https://technet.microsoft.com/library/dd807130.aspx)<br /><br />![フェデレーション プロキシ サーバーのセットアップ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション サーバー プロキシを配置する場所](https://technet.microsoft.com/library/dd807048.aspx)|  
|![フェデレーション プロキシ サーバーのセットアップ](media/icon_checkboxo.gif)|実稼働環境で使用する必要があります、フェデレーション サーバー プロキシの適切な数を特定する AD FS 容量計画のガイダンスを確認します。|![フェデレーション プロキシ サーバーのセットアップ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[のフェデレーション サーバー プロキシの容量計画](https://technet.microsoft.com/library/gg749898.aspx)|  
|![フェデレーション プロキシ サーバーのセットアップ](media/icon_checkboxo.gif)|1 つのフェデレーション サーバー プロキシまたはフェデレーション サーバー プロキシ ファームが展開に優れたかどうかを決定します。 **注:**フェデレーション サーバーは、フェデレーション サーバー プロキシの役割も実行します。|![フェデレーション プロキシ サーバーのセットアップ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[をフェデレーション サーバー プロキシを作成する場合](https://technet.microsoft.com/library/dd807032.aspx)<br /><br />![フェデレーション プロキシ サーバーのセットアップ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[をフェデレーション サーバー プロキシ ファームを作成する場合](https://technet.microsoft.com/library/dd807082.aspx)|  
|![フェデレーション プロキシ サーバーのセットアップ](media/icon_checkboxo.gif)|この新しいフェデレーション サーバー プロキシをアカウント パートナーの組織とリソース パートナー組織の境界ネットワークで作成するかどうかを決定します。|![フェデレーション プロキシ サーバーのセットアップ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[アカウント パートナー内のフェデレーション サーバー プロキシの役割を確認します。](https://technet.microsoft.com/library/dd807109.aspx)<br /><br />![フェデレーション プロキシ サーバーのセットアップ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[リソース パートナー内のフェデレーション サーバー プロキシの役割を確認します。](https://technet.microsoft.com/en-us/library/dd807052.aspx)|  
|![フェデレーション プロキシ サーバーのセットアップ](media/icon_checkboxo.gif)|フェデレーション サーバー プロキシとなるコンピューターに AD FS をインストールする前に、サーバー認証証明書を取得することの重要性を読んで: フェデレーション サーバー プロキシ ファームの-追加や、ファーム内のすべてのサーバー間で証明書を共有します。|![フェデレーション プロキシ サーバーのセットアップ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション サーバー プロキシの証明書の要件](https://technet.microsoft.com/library/dd807054.aspx)|  
|![フェデレーション プロキシ サーバーのセットアップ](media/icon_checkboxo.gif)|AD FS 設計ガイドでフェデレーション サーバーとフェデレーション サーバー プロキシの正常な名前解決が発生することができるように、境界ネットワーク内のドメイン ネーム システム \(DNS\) を更新する方法に関する情報を確認します。|![フェデレーション プロキシ サーバーのセットアップ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション サーバー プロキシの名前解決の要件](https://technet.microsoft.com/library/dd807055.aspx)|  
|![フェデレーション プロキシ サーバーのセットアップ](media/icon_checkboxo.gif)|フェデレーション サーバー プロキシをドメインに参加する必要があるかどうかを決定します。 フェデレーション サーバー プロキシは、ドメインに参加させる必要はありませんが、ドメインに参加しているときにリモート管理およびグループ ポリシーの機能と管理を簡単にです。|![フェデレーション プロキシ サーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[コンピューターをドメインに参加させる](Join-a-Computer-to-a-Domain.md)|  
|![フェデレーション プロキシ サーバーのセットアップ](media/icon_checkboxo.gif)|境界ネットワーク内の DNS インフラストラクチャの構成方法に応じてで完了」の手順のいずれか、組織内のフェデレーション サーバー プロキシを展開する前に直接します。 **注:**の両方の手順を実行しないでください。 読み取り[フェデレーション サーバー プロキシの名前解決要件](https://technet.microsoft.com/library/dd807055.aspx)を最適などの手順に適した、組織の要件を決定します。|![フェデレーション プロキシ サーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[、境界ネットワークのみを提供する DNS ゾーンでフェデレーション サーバー プロキシの名前解決を構成します。](Configure-Name-Resolution-for-a-Federation-Server-Proxy-in-a-DNS-Zone-That-Serves-Only-the-Perimeter-Network.md)<br /><br />![フェデレーション プロキシ サーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[DNS ゾーンことはどちらも、境界ネットワークとインターネット クライアントでのフェデレーション サーバー プロキシの名前解決を構成します。](Configure-Name-Resolution-for-a-Federation-Server-Proxy-in-a-DNS-Zone-That-Serves-Both-the-Perimeter-Network-and-Internet-Clients.md)|  
|![フェデレーション プロキシ サーバーのセットアップ](media/icon_checkboxo.gif)|サーバー認証証明書を取得した後は、フェデレーション サーバー プロキシの既定の Web サイトのインターネット インフォメーション サービス \(IIS\) でインストールする必要があります。|![フェデレーション プロキシ サーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[サーバー認証証明書を既定の Web サイトにインポートします。](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)|  
|![フェデレーション プロキシ サーバーのセットアップ](media/icon_checkboxo.gif)|証明機関から、サーバー認証証明書を取得する代わりに \(Optional\) \(CA\)、IIS を使用してフェデレーション サーバー プロキシの証明書をサンプルを取得します。<br /><br />IIS、自己署名証明書を信頼できる発行元から提供されないため、使用して、次のシナリオでのみ、自己署名証明書を作成します。<br /><br />-する必要がある場合、サーバーとユーザーの制限付き、既知のグループ間の Secure Sockets Layer \(SSL\) チャネルを作成するには<br />-Third\ パーティー証明書の問題のトラブルシューティングを行う必要がある場合**注意:**サーバー認証証明書を使用して、自己署名、運用環境でフェデレーション サーバー プロキシの展開にセキュリティのベスト プラクティスではありません。|![フェデレーション プロキシ サーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[IIS: Self\-Signed サーバー証明書を作成します。](https://go.microsoft.com/fwlink/?LinkID=108271)|  
|![フェデレーション プロキシ サーバーのセットアップ](media/icon_checkboxo.gif)|フェデレーション サーバー プロキシとなるコンピューターに、フェデレーション サービス プロキシ役割サービスをインストールします。|![フェデレーション プロキシ サーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーション サービス プロキシ役割サービスのインストール](Install-the-Federation-Service-Proxy-Role-Service.md)|  
|![フェデレーション プロキシ サーバーのセットアップ](media/icon_checkboxo.gif)|AD FSFederation サーバー プロキシ構成ウィザードを使用して、フェデレーション サーバー プロキシの役割で動作するコンピューターで AD FS ソフトウェアを構成します。|![フェデレーション プロキシ サーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーション サーバー プロキシの役割のコンピューターを構成します。](Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)|  
|![フェデレーション プロキシ サーバーのセットアップ](media/icon_checkboxo.gif)|イベント ビューアーを使用して、フェデレーション サーバー プロキシ サービスが開始されたことを確認します。|![フェデレーション プロキシ サーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[いることを確認、フェデレーション サーバー プロキシが正常に動作](Verify-That-a-Federation-Server-Proxy-Is-Operational.md)|  
