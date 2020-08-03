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
ms.openlocfilehash: 0ffb9a33fa5c06c9fa79846c21937ffddb2776cd
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2020
ms.locfileid: "87520021"
---
# <a name="checklist-setting-up-a-federation-server-proxy"></a>チェックリスト: フェデレーション サーバー プロキシのセットアップ

このチェックリストには &reg; Active Directory フェデレーションサービス (AD FS) AD FS のフェデレーションサーバープロキシの役割用に、Windows server 2012 を実行しているサーバーを準備するための展開タスクが含まれてい \( \) ます。

> [!NOTE]
> このチェックリストのタスクは順番に実行してください。 参照リンクによって手順に移動した場合は、このチェックリストの残りのタスクを進めることができるように、その手順の作業が完了したらこのトピックに戻ります。

![フェデレーションプロキシサーバーの設定の](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**チェックリスト: フェデレーションサーバープロキシの設定**

|タスク|リファレンス|
|--------|-------------|
|AD FS フェデレーションサーバープロキシの展開を開始する前に、AD FS 展開トポロジの種類と、それに関連付けられているサーバーの配置とネットワークレイアウトに関する推奨事項を確認してください。|![フェデレーションプロキシサーバーを設定すると](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[、AD FS の展開トポロジが決まり](../design/determine-your-ad-fs-deployment-topology.md)ます。<p>![フェデレーションプロキシサーバーのセットアップ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーションサーバープロキシの配置の計画](../design/planning-federation-server-proxy-placement.md)<p>![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーションサーバープロキシを配置する](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807048(v=ws.11))フェデレーションプロキシサーバーの設定|
|AD FS 容量計画のガイダンスを確認して、運用環境で使用する必要があるフェデレーションサーバープロキシの適切な数を決定します。|![フェデレーションプロキシサーバーのセットアップ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーションサーバープロキシの容量の計画](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/gg749898(v=ws.11))|
|単一のフェデレーションサーバープロキシまたはフェデレーションサーバープロキシファームが展開に適しているかどうかを判断します。 **注:** フェデレーションサーバーでは、フェデレーションサーバープロキシの役割も実行します。|![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーションサーバープロキシを作成する場合](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807032(v=ws.11))のフェデレーションプロキシサーバーの設定<p>![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーションサーバープロキシファームを作成する場合](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807082(v=ws.11))のフェデレーションプロキシサーバーの設定|
|この新しいフェデレーションサーバープロキシを、アカウントパートナー組織またはリソースパートナー組織の境界ネットワーク内に作成するかどうかを決定します。|![フェデレーションプロキシサーバーの設定](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[アカウントパートナーのフェデレーションサーバープロキシの役割を確認](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807109(v=ws.11))する<p>![フェデレーションプロキシサーバーの設定](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[リソースパートナー内のフェデレーションサーバープロキシの役割を確認する](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807052(v=ws.11))|
|フェデレーションサーバープロキシとなるコンピューターに AD FS をインストールする前に、「サーバー認証証明書を取得する (フェデレーションサーバープロキシファーム)」で、ファーム内のすべてのサーバー間で証明書を追加または共有することの重要性について説明します。|![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーションサーバープロキシのフェデレーションプロキシサーバー証明書の要件](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807054(v=ws.11))の設定|
|境界ネットワークのドメインネームシステム DNS を更新して、 \( \) フェデレーションサーバーとフェデレーションサーバープロキシの名前解決が正常に行われるようにする方法については、AD FS 設計ガイドの情報を確認してください。|![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーションサーバープロキシのフェデレーションプロキシサーバーの名前解決要件](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807055(v=ws.11))の設定|
|フェデレーションサーバープロキシがドメインに参加している必要があるかどうかを判断します。 フェデレーションサーバープロキシはドメインに参加している必要はありませんが、リモート管理およびグループポリシー機能を使用してドメインに参加している場合は、管理が容易になります。|![フェデレーションプロキシサーバーの設定](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[ドメインへのコンピューターの参加](Join-a-Computer-to-a-Domain.md)|
|境界ネットワークの DNS インフラストラクチャがどのように構成されているかによって、組織内にフェデレーションサーバープロキシを展開する前に、右側にあるトピックの手順のいずれかを実行します。 **注:** 両方の手順を実行しないでください。 [フェデレーションサーバープロキシの名前解決の要件](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807055(v=ws.11))を読み、組織の要件に最も適した手順を決定します。|![フェデレーションプロキシサーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[境界ネットワークのみを提供する DNS ゾーンでフェデレーションサーバープロキシの名前解決を構成](./configure-name-resolution-for-federation-server-proxy-in-dns-zone-serving-only-perimeter-network.md)する<p>![フェデレーションプロキシサーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[境界ネットワークとインターネットクライアントの両方を提供する DNS ゾーンでフェデレーションサーバープロキシの名前解決を構成](./configure-name-resolution-for-federation-server-proxy-in-dns-zone-serving-only-perimeter-network.md)する|
|サーバー認証証明書を取得したら、 \( \) フェデレーションサーバープロキシの既定の Web サイトでインターネットインフォメーションサービス IIS にインストールする必要があります。|![フェデレーションプロキシサーバーを設定](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[するサーバー認証証明書を既定の Web サイトにインポートする](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)|
|\(省略可能。 \) 証明機関の CA からサーバー認証証明書を取得する代わりに、IIS を使用して、 \( \) フェデレーションサーバープロキシのサンプル証明書を取得できます。<p>IIS は、 \- 信頼できる発行元からのものではない自己署名証明書を生成するため、 \- 次のシナリオでのみ、自己署名証明書を作成するために使用します。<p>-サーバーと、制限されているユーザーグループの間に Secure Sockets Layer の \( SSL チャネルを作成する必要がある場合 \)<br />-サードパーティの証明書に関する問題のトラブルシューティングが必要な場合は、自己署名された \- **Caution:** \- サーバー認証証明書を使用して運用環境にフェデレーションサーバープロキシを展開することは、セキュリティのベストプラクティスではありません。|![フェデレーションプロキシサーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[IIS: 自己 \- 署名サーバー証明書の作成](https://go.microsoft.com/fwlink/?LinkID=108271)|
|フェデレーションサーバープロキシとなるコンピューターにフェデレーションサービスプロキシの役割サービスをインストールします。|![フェデレーションプロキシサーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーションサービスプロキシの役割サービスのインストール](Install-the-Federation-Service-Proxy-Role-Service.md)|
|AD FSFederation サーバープロキシ構成ウィザードを使用して、コンピューター上の AD FS ソフトウェアを、フェデレーションサーバープロキシの役割で動作するように構成します。|![フェデレーションプロキシサーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーションサーバープロキシの役割用にコンピューターを構成](Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)する|
|イベント ビューアーを使用して、フェデレーション サーバー プロキシ サービスが起動していることを確認します。|![フェデレーションプロキシサーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーションサーバープロキシが動作していることを確認する](Verify-That-a-Federation-Server-Proxy-Is-Operational.md)|
