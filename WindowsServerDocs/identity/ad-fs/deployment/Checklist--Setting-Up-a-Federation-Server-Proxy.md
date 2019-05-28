---
ms.assetid: 38c9bcd3-c6f8-4153-8e42-5fd31568c65a
title: チェックリストのフェデレーション サーバー プロキシを設定します。
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: c8cd5cbe2ce0c7985a56f8444edfa7c71ee17c2d
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192347"
---
# <a name="checklist-setting-up-a-federation-server-proxy"></a>チェックリスト:フェデレーション サーバー プロキシのセットアップ

このチェックリストには、Active Directory フェデレーション サービスでフェデレーション サーバー プロキシ役割用の Windows Server® 2012 を実行するサーバーを準備するための展開タスクが含まれています。 \(AD FS\)します。  
  
> [!NOTE]  
> このチェックリストのタスクは順番に実行してください。 参照リンクによって手順に移動した場合は、このチェックリストの残りのタスクを進めることができるように、その手順の作業が完了したらこのトピックに戻ります。  
  
![フェデレーション プロキシ サーバーを設定する](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**チェックリスト。フェデレーション サーバー プロキシを設定します。**  
  
||タスク|リファレンス|  
|-|--------|-------------|  
|![フェデレーション プロキシ サーバーを設定します。](media/icon_checkboxo.gif)|AD FS フェデレーション サーバー プロキシの展開を開始する前に、AD FS 展開トポロジの種類および関連付けられているサーバーの配置とネットワークのレイアウトに関する推奨事項を確認します。|![フェデレーション プロキシ サーバーを設定する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 展開トポロジの決定](https://technet.microsoft.com/library/gg982491.aspx)<br /><br />![フェデレーション プロキシ サーバーを設定する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション サーバー プロキシの配置の計画](https://technet.microsoft.com/library/dd807130.aspx)<br /><br />![フェデレーション プロキシ サーバーを設定する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション サーバー プロキシを配置する場所](https://technet.microsoft.com/library/dd807048.aspx)|  
|![フェデレーション プロキシ サーバーを設定します。](media/icon_checkboxo.gif)|実稼働環境で使用する必要があります、フェデレーション サーバー プロキシの適切な数を決定する AD FS キャパシティ プランニング ガイダンスを確認します。|![フェデレーション プロキシ サーバーを設定する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[のフェデレーション サーバー プロキシのキャパシティ プランニング](https://technet.microsoft.com/library/gg749898.aspx)|  
|![フェデレーション プロキシ サーバーを設定します。](media/icon_checkboxo.gif)|1 つのフェデレーション サーバー プロキシまたはフェデレーション サーバー プロキシ ファームは、展開に適しているかどうかを決定します。 **注:** フェデレーション サーバーでは、フェデレーション サーバー プロキシの役割も実行します。|![フェデレーション プロキシ サーバーを設定する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション サーバー プロキシを作成する場合](https://technet.microsoft.com/library/dd807032.aspx)<br /><br />![フェデレーション プロキシ サーバーを設定する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション サーバー プロキシ ファームを作成する場合](https://technet.microsoft.com/library/dd807082.aspx)|  
|![フェデレーション プロキシ サーバーを設定します。](media/icon_checkboxo.gif)|この新しいフェデレーション サーバー プロキシは、アカウント パートナー組織とリソース パートナー組織の境界ネットワークに作成されるかどうかを決定します。|![フェデレーション プロキシ サーバーを設定する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[アカウント パートナー フェデレーション サーバー プロキシの役割を確認します。](https://technet.microsoft.com/library/dd807109.aspx)<br /><br />![フェデレーション プロキシ サーバーを設定する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[リソース パートナーのフェデレーション サーバー プロキシの役割を確認します。](https://technet.microsoft.com/library/dd807052.aspx)|  
|![フェデレーション プロキシ サーバーを設定します。](media/icon_checkboxo.gif)|サーバー認証証明書を取得することの重要性について、AD FS をフェデレーション サーバー プロキシとなるコンピューターにインストールする前に: フェデレーション サーバー プロキシ ファーム-を追加するか、ファーム内のすべてのサーバー間で証明書を共有します。|![フェデレーション プロキシ サーバーを設定する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション サーバー プロキシの証明書の要件](https://technet.microsoft.com/library/dd807054.aspx)|  
|![フェデレーション プロキシ サーバーを設定します。](media/icon_checkboxo.gif)|ドメイン ネーム システムを更新する方法について、AD FS 設計ガイドの情報を確認して\(DNS\)境界ネットワークのフェデレーション サーバーとフェデレーション サーバー プロキシには、その正常な名前解決が行われるようにします。|![フェデレーション プロキシ サーバーを設定する](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション サーバー プロキシの名前解決の要件](https://technet.microsoft.com/library/dd807055.aspx)|  
|![フェデレーション プロキシ サーバーを設定します。](media/icon_checkboxo.gif)|フェデレーション サーバー プロキシをドメインに参加する必要があるかどうかを決定します。 フェデレーション サーバー プロキシは、ドメインに参加させる必要はありませんはドメインに参加するとき、リモート管理とグループ ポリシーの機能を管理しやすくします。|![フェデレーション プロキシ サーバーを設定する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[コンピューターをドメインに参加させる](Join-a-Computer-to-a-Domain.md)|  
|![フェデレーション プロキシ サーバーを設定します。](media/icon_checkboxo.gif)|境界ネットワーク内の DNS インフラストラクチャの構成方法に応じて完了右側のトピックの手順のいずれか、組織のフェデレーション サーバー プロキシを展開する前にします。 **注:** どちらの手順を実行しません。 読み取り[フェデレーション サーバー プロキシの名前解決要件](https://technet.microsoft.com/library/dd807055.aspx)を最適などの手順が、組織の要件に適したを判断します。|![フェデレーション プロキシ サーバーを設定する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[境界ネットワークのみを提供する DNS ゾーンにフェデレーション サーバー プロキシの名前解決を構成します。](Configure-Name-Resolution-for-a-Federation-Server-Proxy-in-a-DNS-Zone-That-Serves-Only-the-Perimeter-Network.md)<br /><br />![フェデレーション プロキシ サーバーを設定する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[DNS ゾーンことはどちらも、境界ネットワークとインターネット クライアントでのフェデレーション サーバー プロキシの名前解決を構成します。](Configure-Name-Resolution-for-a-Federation-Server-Proxy-in-a-DNS-Zone-That-Serves-Both-the-Perimeter-Network-and-Internet-Clients.md)|  
|![フェデレーション プロキシ サーバーを設定します。](media/icon_checkboxo.gif)|サーバー認証証明書を取得した後は、インターネット インフォメーション サービスでインストールする必要があります\(IIS\)フェデレーション サーバー プロキシの既定の Web サイトにします。|![フェデレーション プロキシ サーバーを設定する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[既定の Web サイトにサーバー認証証明書のインポート](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)|  
|![フェデレーション プロキシ サーバーを設定します。](media/icon_checkboxo.gif)|\(省略可能な\)証明機関からのサーバー認証証明書を取得するための代替として\(CA\)IIS を使用して、フェデレーション サーバー プロキシのサンプルの証明書を取得することができます。<br /><br />IIS は、自己を生成するため\-は信頼できるソースからではなく、自己の作成に使用される署名証明書\-次のシナリオでのみ証明書に署名します。<br /><br />Secure Sockets Layer を作成する必要が- \(SSL\)サーバーとユーザーの制限、既知のグループ間のチャネル<br />-3 つ目のトラブルシューティングがある場合\-パーティ証明書の問題**注意が必要です。** 自己を使用して、実稼働環境でフェデレーション サーバー プロキシの展開にセキュリティのベスト プラクティスではない\-署名済み、サーバー認証証明書。|![フェデレーション プロキシ サーバーを設定する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[IIS:自動作成\-サーバー証明書の署名](https://go.microsoft.com/fwlink/?LinkID=108271)|  
|![フェデレーション プロキシ サーバーを設定します。](media/icon_checkboxo.gif)|フェデレーション サーバー プロキシとなるコンピューターに、フェデレーション サービス プロキシ役割サービスをインストールします。|![フェデレーション プロキシ サーバーを設定する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーション サービス プロキシ役割サービスのインストール](Install-the-Federation-Service-Proxy-Role-Service.md)|  
|![フェデレーション プロキシ サーバーを設定します。](media/icon_checkboxo.gif)|AD FSFederation サーバー プロキシ構成ウィザードを使用してフェデレーション サーバー プロキシの役割で動作するコンピューターの AD FS ソフトウェアを構成します。|![フェデレーション プロキシ サーバーを設定する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーション サーバー プロキシ ロール用コンピューターの構成](Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)|  
|![フェデレーション プロキシ サーバーを設定します。](media/icon_checkboxo.gif)|イベント ビューアーを使用して、フェデレーション サーバー プロキシ サービスが起動していることを確認します。|![フェデレーション プロキシ サーバーを設定する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[いることを確認、フェデレーション サーバー プロキシが正常に動作](Verify-That-a-Federation-Server-Proxy-Is-Operational.md)|  
