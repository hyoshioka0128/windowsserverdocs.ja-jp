---
ms.assetid: 38c9bcd3-c6f8-4153-8e42-5fd31568c65a
title: チェックリスト-フェデレーションサーバープロキシの設定
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 43fb8db4bf494ded93e592a1346a9ba99f0aff55
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359927"
---
# <a name="checklist-setting-up-a-federation-server-proxy"></a>チェックリスト:フェデレーション サーバー プロキシのセットアップ

このチェックリストには、Active Directory フェデレーションサービス (AD FS) \(AD FS @ no__t-1 のフェデレーションサーバープロキシの役割用に、Windows Server®2012を実行しているサーバーを準備するための展開タスクが含まれています。  
  
> [!NOTE]  
> このチェックリストのタスクは順番に実行してください。 参照リンクによって手順に移動した場合は、このチェックリストの残りのタスクを進めることができるように、その手順の作業が完了したらこのトピックに戻ります。  
  
](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)** フェデレーションプロキシサーバーをセットアップする @ no__t-1Checklist リスト:フェデレーションサーバープロキシのセットアップ @ no__t-0  
  
||タスク|参照|  
|-|--------|-------------|  
|![フェデレーションプロキシサーバーの設定](media/icon_checkboxo.gif)|AD FS フェデレーションサーバープロキシの展開を開始する前に、AD FS 展開トポロジの種類と、それに関連付けられているサーバーの配置とネットワークレイアウトに関する推奨事項を確認してください。|つのフェデレーションプロキシサーバーを設定する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS の展開トポロジを決定](https://technet.microsoft.com/library/gg982491.aspx)する<br /><br />![ フェデレーションプロキシサーバーのセットアップ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーションサーバープロキシの配置の計画](https://technet.microsoft.com/library/dd807130.aspx)<br /><br />@no__t。](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーションサーバープロキシを配置する](https://technet.microsoft.com/library/dd807048.aspx)フェデレーションプロキシサーバーをセットアップする|  
|![フェデレーションプロキシサーバーの設定](media/icon_checkboxo.gif)|AD FS 容量計画のガイダンスを確認して、運用環境で使用する必要があるフェデレーションサーバープロキシの適切な数を決定します。|つのフェデレーションプロキシサーバーのセットアップ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーションサーバープロキシの容量の計画](https://technet.microsoft.com/library/gg749898.aspx)|  
|![フェデレーションプロキシサーバーの設定](media/icon_checkboxo.gif)|単一のフェデレーションサーバープロキシまたはフェデレーションサーバープロキシファームが展開に適しているかどうかを判断します。 **注:** フェデレーションサーバーでは、フェデレーションサーバープロキシの役割も実行します。|@no__t:](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーションサーバープロキシを作成する場合](https://technet.microsoft.com/library/dd807032.aspx)のフェデレーションプロキシサーバーのセットアップ<br /><br />@no__t:](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーションサーバープロキシファームを作成する場合](https://technet.microsoft.com/library/dd807082.aspx)のフェデレーションプロキシサーバーのセットアップ|  
|![フェデレーションプロキシサーバーの設定](media/icon_checkboxo.gif)|この新しいフェデレーションサーバープロキシを、アカウントパートナー組織またはリソースパートナー組織の境界ネットワーク内に作成するかどうかを決定します。|![ フェデレーションプロキシサーバーを設定する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[アカウントパートナーのフェデレーションサーバープロキシの役割を確認する](https://technet.microsoft.com/library/dd807109.aspx)<br /><br />つのフェデレーションプロキシサーバーをセットアップする](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[リソースパートナー内のフェデレーションサーバープロキシの役割を確認する](https://technet.microsoft.com/library/dd807052.aspx)|  
|![フェデレーションプロキシサーバーの設定](media/icon_checkboxo.gif)|フェデレーションサーバープロキシとなるコンピューターに AD FS をインストールする前に、「サーバー認証証明書を取得する (フェデレーションサーバープロキシファーム)」で、ファーム内のすべてのサーバー間で証明書を追加または共有することの重要性について説明します。|@no__t-](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[0Setting server proxy のフェデレーションプロキシサーバー証明書の要件](https://technet.microsoft.com/library/dd807054.aspx)の設定|  
|![フェデレーションプロキシサーバーの設定](media/icon_checkboxo.gif)|境界ネットワークのドメインネームシステム \(DNS @ no__t を更新して、フェデレーションサーバーとフェデレーションサーバープロキシの名前解決が正常に行われるようにする方法については、AD FS 設計ガイドの情報を確認してください。|@no__t-](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[0Setting server proxy のフェデレーションプロキシサーバーの名前解決要件](https://technet.microsoft.com/library/dd807055.aspx)の設定|  
|![フェデレーションプロキシサーバーの設定](media/icon_checkboxo.gif)|フェデレーションサーバープロキシがドメインに参加している必要があるかどうかを判断します。 フェデレーションサーバープロキシはドメインに参加している必要はありませんが、リモート管理およびグループポリシー機能を使用してドメインに参加している場合は、管理が容易になります。|つのフェデレーションプロキシサーバーをセットアップして](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[コンピューターをドメインに参加させる](Join-a-Computer-to-a-Domain.md)|  
|![フェデレーションプロキシサーバーの設定](media/icon_checkboxo.gif)|境界ネットワークの DNS インフラストラクチャがどのように構成されているかによって、組織内にフェデレーションサーバープロキシを展開する前に、右側にあるトピックの手順のいずれかを実行します。 **注:** 両方の手順を実行しないでください。 [フェデレーションサーバープロキシの名前解決の要件](https://technet.microsoft.com/library/dd807055.aspx)を読み、組織の要件に最も適した手順を決定します。|つのフェデレーションプロキシサーバーをセットアップする](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[境界ネットワークのみを提供する DNS ゾーンでフェデレーションサーバープロキシの名前解決を構成する](Configure-Name-Resolution-for-a-Federation-Server-Proxy-in-a-DNS-Zone-That-Serves-Only-the-Perimeter-Network.md)<br /><br />![setting プロキシサーバーの設定](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーションサーバープロキシの名前解決を、境界ネットワークとインターネットクライアントの両方を提供する DNS ゾーンで構成する](Configure-Name-Resolution-for-a-Federation-Server-Proxy-in-a-DNS-Zone-That-Serves-Both-the-Perimeter-Network-and-Internet-Clients.md)|  
|![フェデレーションプロキシサーバーの設定](media/icon_checkboxo.gif)|サーバー認証証明書を取得したら、フェデレーションサーバープロキシの既定の Web サイトのインターネットインフォメーションサービス \(IIS @ no__t にインストールする必要があります。|つのフェデレーションプロキシサーバーを設定](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[するサーバー認証証明書を既定の Web サイトにインポートする](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)|  
|![フェデレーションプロキシサーバーの設定](media/icon_checkboxo.gif)|\(Optional @ no__t-1 証明機関からサーバー認証証明書を取得する代わりに \(CA @ no__t から、IIS を使用してフェデレーションサーバープロキシのサンプル証明書を取得できます。<br /><br />IIS は、信頼されたソースからのものではない、自己 @ no__t の署名入り証明書を生成するため、次のシナリオでのみ、自己 @ no__t-1signed 入り証明書を作成するために使用します。<br /><br />-サーバーと、制限されているユーザーグループの間に Secure Sockets Layer \(SSL @ no__t チャネルを作成する必要がある場合<br />-3 番目の @ no__t-0party 証明書の問題をトラブルシューティングする必要がある場合は、次の点に注意して**ください。** 自己 @ no__t で署名されたサーバー認証証明書を使用して運用環境にフェデレーションサーバープロキシを展開することは、セキュリティのベストプラクティスではありません。|](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[ フェデレーションプロキシサーバーをセットアップする @ no__t-1 IIS:自己 @ no__t-0Signed 署名されたサーバー証明書 @ no__t-1 を作成します。|  
|![フェデレーションプロキシサーバーの設定](media/icon_checkboxo.gif)|フェデレーションサーバープロキシとなるコンピューターにフェデレーションサービスプロキシの役割サービスをインストールします。|![setting プロキシサーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーションサービスプロキシの役割サービスのインストール](Install-the-Federation-Service-Proxy-Role-Service.md)|  
|![フェデレーションプロキシサーバーの設定](media/icon_checkboxo.gif)|AD FSFederation サーバープロキシ構成ウィザードを使用して、コンピューター上の AD FS ソフトウェアを、フェデレーションサーバープロキシの役割で動作するように構成します。|つのフェデレーションプロキシサーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーションサーバープロキシの役割用にコンピューターを構成](Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)する|  
|![フェデレーションプロキシサーバーの設定](media/icon_checkboxo.gif)|イベント ビューアーを使用して、フェデレーション サーバー プロキシ サービスが起動していることを確認します。|つのフェデレーションプロキシサーバーを設定](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[するフェデレーションサーバープロキシが動作して](Verify-That-a-Federation-Server-Proxy-Is-Operational.md)いることを確認する|  
