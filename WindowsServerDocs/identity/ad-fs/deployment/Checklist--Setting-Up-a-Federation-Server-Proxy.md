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
# <a name="checklist-setting-up-a-federation-server-proxy"></a>チェックリスト: フェデレーション サーバー プロキシのセットアップ

このチェックリストには、Active Directory フェデレーションサービス (AD FS) \(AD FS\)のフェデレーションサーバープロキシの役割用に、Windows Server®2012を実行しているサーバーを準備するための展開タスクが含まれています。  
  
> [!NOTE]  
> このチェックリストのタスクは順番に実行してください。 参照リンクによって手順に移動した場合は、このチェックリストの残りのタスクを進めることができるように、その手順の作業が完了したらこのトピックに戻ります。  
  
フェデレーションプロキシサーバーのセットアップの ![](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**チェックリスト: フェデレーションサーバープロキシの**セットアップ  
  
||タスク|リファレンス|  
|-|--------|-------------|  
|![フェデレーションプロキシサーバーの設定](media/icon_checkboxo.gif)|AD FS フェデレーションサーバープロキシの展開を開始する前に、AD FS 展開トポロジの種類と、それに関連付けられているサーバーの配置とネットワークレイアウトに関する推奨事項を確認してください。|フェデレーションプロキシサーバーのセットアップ ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS の展開トポロジを決定](https://technet.microsoft.com/library/gg982491.aspx)する<br /><br />フェデレーションプロキシサーバーのセットアップ ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーションサーバープロキシの配置の計画](https://technet.microsoft.com/library/dd807130.aspx)<br /><br />](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーションサーバープロキシを配置する](https://technet.microsoft.com/library/dd807048.aspx)フェデレーションプロキシサーバーをセットアップ ![には|  
|![フェデレーションプロキシサーバーの設定](media/icon_checkboxo.gif)|AD FS 容量計画のガイダンスを確認して、運用環境で使用する必要があるフェデレーションサーバープロキシの適切な数を決定します。|フェデレーションプロキシサーバーのセットアップ ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーションサーバープロキシの容量の計画](https://technet.microsoft.com/library/gg749898.aspx)|  
|![フェデレーションプロキシサーバーの設定](media/icon_checkboxo.gif)|単一のフェデレーションサーバープロキシまたはフェデレーションサーバープロキシファームが展開に適しているかどうかを判断します。 **注:** フェデレーションサーバーでは、フェデレーションサーバープロキシの役割も実行します。|](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーションサーバープロキシを作成するとき](https://technet.microsoft.com/library/dd807032.aspx)にフェデレーションプロキシサーバーをセットアップ ![には<br /><br />](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーションサーバープロキシファームを作成するとき](https://technet.microsoft.com/library/dd807082.aspx)に、フェデレーションプロキシサーバーをセットアップ ![には|  
|![フェデレーションプロキシサーバーの設定](media/icon_checkboxo.gif)|この新しいフェデレーションサーバープロキシを、アカウントパートナー組織またはリソースパートナー組織の境界ネットワーク内に作成するかどうかを決定します。|フェデレーションプロキシサーバーの設定 ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[アカウントパートナーのフェデレーションサーバープロキシの役割を確認する](https://technet.microsoft.com/library/dd807109.aspx)<br /><br />フェデレーションプロキシサーバーの設定 ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[リソースパートナー内のフェデレーションサーバープロキシの役割を確認する](https://technet.microsoft.com/library/dd807052.aspx)|  
|![フェデレーションプロキシサーバーの設定](media/icon_checkboxo.gif)|フェデレーションサーバープロキシとなるコンピューターに AD FS をインストールする前に、「サーバー認証証明書を取得する (フェデレーションサーバープロキシファーム)」で、ファーム内のすべてのサーバー間で証明書を追加または共有することの重要性について説明します。|](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーションサーバープロキシのフェデレーションプロキシサーバー証明書の要件](https://technet.microsoft.com/library/dd807054.aspx)の設定 ![|  
|![フェデレーションプロキシサーバーの設定](media/icon_checkboxo.gif)|境界ネットワークのドメインネームシステム \(DNS\) を更新して、フェデレーションサーバーとフェデレーションサーバープロキシの名前解決が正常に行われるようにする方法については、AD FS 設計ガイドの情報を確認してください。|](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーションサーバープロキシのフェデレーションプロキシサーバーの名前解決要件](https://technet.microsoft.com/library/dd807055.aspx)を設定 ![には|  
|![フェデレーションプロキシサーバーの設定](media/icon_checkboxo.gif)|フェデレーションサーバープロキシがドメインに参加している必要があるかどうかを判断します。 フェデレーションサーバープロキシはドメインに参加している必要はありませんが、リモート管理およびグループポリシー機能を使用してドメインに参加している場合は、管理が容易になります。|フェデレーションプロキシサーバーのセットアップ ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[コンピューターのドメインへの参加](Join-a-Computer-to-a-Domain.md)|  
|![フェデレーションプロキシサーバーの設定](media/icon_checkboxo.gif)|境界ネットワークの DNS インフラストラクチャがどのように構成されているかによって、組織内にフェデレーションサーバープロキシを展開する前に、右側にあるトピックの手順のいずれかを実行します。 **注:** 両方の手順を実行しないでください。 [フェデレーションサーバープロキシの名前解決の要件](https://technet.microsoft.com/library/dd807055.aspx)を読み、組織の要件に最も適した手順を決定します。|フェデレーションプロキシサーバーの設定 ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[境界ネットワークのみを提供する DNS ゾーンでフェデレーションサーバープロキシの名前解決を構成する](Configure-Name-Resolution-for-a-Federation-Server-Proxy-in-a-DNS-Zone-That-Serves-Only-the-Perimeter-Network.md)<br /><br />フェデレーションプロキシサーバーの設定 ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[境界ネットワークとインターネットクライアントの両方を提供する DNS ゾーンでフェデレーションサーバープロキシの名前解決を構成](Configure-Name-Resolution-for-a-Federation-Server-Proxy-in-a-DNS-Zone-That-Serves-Both-the-Perimeter-Network-and-Internet-Clients.md)する|  
|![フェデレーションプロキシサーバーの設定](media/icon_checkboxo.gif)|サーバー認証証明書を取得したら、フェデレーションサーバープロキシの既定の Web サイトでインターネットインフォメーションサービス \(IIS\) にインストールする必要があります。|フェデレーションプロキシサーバーのセットアップ ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[サーバー認証証明書を既定の Web サイトにインポートする](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)|  
|![フェデレーションプロキシサーバーの設定](media/icon_checkboxo.gif)|\(オプション\) 証明機関 \(CA\)からサーバー認証証明書を取得する代わりに、IIS を使用してフェデレーションサーバープロキシのサンプル証明書を取得することができます。<br /><br />IIS は、信頼されたソースから送信されない自己\-署名入り証明書を生成するため、次のシナリオでのみ自己\-署名入り証明書を作成するために使用します。<br /><br />-サーバーと、制限されているユーザーグループの間の SSL\) チャネル \(Secure Sockets Layer を作成する必要がある場合<br />-\-サードパーティの証明書に関する問題のトラブルシューティングが必要な場合は、自己\-署名されたサーバー認証証明書を使用して運用環境にフェデレーションサーバープロキシを**展開すること**は、セキュリティのベストプラクティスではありません。|フェデレーションプロキシサーバーのセットアップ ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[IIS: 自己\-署名されたサーバー証明書を作成する](https://go.microsoft.com/fwlink/?LinkID=108271)|  
|![フェデレーションプロキシサーバーの設定](media/icon_checkboxo.gif)|フェデレーションサーバープロキシとなるコンピューターにフェデレーションサービスプロキシの役割サービスをインストールします。|フェデレーションプロキシサーバーのセットアップ ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーションサービスプロキシの役割サービスをインストール](Install-the-Federation-Service-Proxy-Role-Service.md)する|  
|![フェデレーションプロキシサーバーの設定](media/icon_checkboxo.gif)|AD FSFederation サーバープロキシ構成ウィザードを使用して、コンピューター上の AD FS ソフトウェアを、フェデレーションサーバープロキシの役割で動作するように構成します。|フェデレーションプロキシサーバーのセットアップ ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーションサーバープロキシの役割用にコンピューターを構成](Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)する|  
|![フェデレーションプロキシサーバーの設定](media/icon_checkboxo.gif)|イベント ビューアーを使用して、フェデレーション サーバー プロキシ サービスが起動していることを確認します。|フェデレーションプロキシサーバーのセットアップ ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーションサーバープロキシが動作して](Verify-That-a-Federation-Server-Proxy-Is-Operational.md)いることを確認する|  
