---
ms.assetid: 8f954004-40d5-4c5e-8e0d-e8700c8ec7b1
title: チェックリスト-フェデレーションサーバーのセットアップ
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.author: billmath
ms.openlocfilehash: 929b868c1afa2dd21897526938611f881dfade37
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87938558"
---
# <a name="checklist-setting-up-a-federation-server"></a>チェックリスト: フェデレーション サーバーのセットアップ

このチェックリストには、 &reg; Active Directory フェデレーションサービス (AD FS) AD FS のフェデレーションサーバーの役割用に Windows server 2012 を実行しているサーバーを準備するために必要な展開タスクが含まれてい \( \) ます。

> [!NOTE]
> このチェックリストのタスクは順番に実行してください。 参照リンクによって手順に移動した場合は、このチェックリストの残りのタスクを進めることができるように、その手順の作業が完了したらこのトピックに戻ります。

![フェデレーションサーバーのセットアップの](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**チェックリスト: フェデレーションサーバーの**セットアップ

|タスク|リファレンス|
|--------|-------------|
|AD FS フェデレーションサーバーのデプロイを開始する前に、「」を確認してください。1. \) \( \) AD FS 構成データベース 2 \) を格納するために、Windows Internal Database WID または SQL Server を選択する利点と欠点。AD FS 展開トポロジの種類と、それに関連付けられているサーバーの配置とネットワークレイアウトに関する推奨事項。|![フェデレーションサーバーのセットアップ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 展開トポロジの決定](../design/determine-your-ad-fs-deployment-topology.md)<p>![フェデレーションサーバーのセットアップ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 展開トポロジに関する考慮事項](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/gg982489(v=ws.11))|
|AD FS 容量計画のガイダンスを確認して、運用環境で使用する必要があるフェデレーションサーバーの適切な数を決定します。|![フェデレーションサーバー](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[の設定のフェデレーションサーバーの容量の計画](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/gg749917(v=ws.11))|
|組織内のフェデレーションサーバーを配置する場所について AD FS 設計ガイドの情報を確認する|![フェデレーションサーバーのセットアップ](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーションサーバーの配置の計画](../design/planning-federation-server-placement.md)<p>![フェデレーションサーバーを](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[配置する](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807127(v=ws.11))フェデレーションサーバーのセットアップ|
|スタンド \- アロンフェデレーションサーバーまたはフェデレーションサーバーファームが展開に適しているかどうかを判断します。|![フェデレーションサーバーを](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[作成する場合](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807101(v=ws.11))のフェデレーションサーバーのセットアップ<p>![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーションサーバーファームを作成する場合](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807062(v=ws.11))のフェデレーションサーバーのセットアップ|
|この新しいフェデレーションサーバーが、アカウントパートナー組織とリソースパートナー組織のどちらに作成されるかを決定します。|![フェデレーションサーバー](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[のセットアップアカウントパートナー内のフェデレーションサーバーの役割を確認](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807117(v=ws.11))する<p>![フェデレーションサーバー](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[のセットアップリソースパートナー内のフェデレーションサーバーの役割を確認](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807065(v=ws.11))する|
|フェデレーションサーバーがサービス通信証明書とトークン署名証明書を使用して \- 、クライアントとフェデレーションサーバーのプロキシ要求を安全に認証する方法に関する情報を確認します。 **注意:** Https: myserver など、修飾されていないホスト名を持つ証明書を使用することは、一般的には時間がかかりますが \/ \/ 、これらの証明書にはセキュリティ値がないため、攻撃者は AD FS フェデレーションサービスをエンタープライズクライアントに偽装できます。 このため、https: myserver.contoso.com のような完全修飾ドメイン名の fqdn を使用 \( \) し、 \/ \/ フェデレーションサービスの fqdn に発行された SSL 証明書のみを使用することをお勧めします。|![フェデレーションサーバーのフェデレーションサーバー](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[証明書の要件](../design/certificate-requirements-for-federation-servers.md)の設定|
|\( \) フェデレーションサーバーへの名前解決が正常に行われるように、企業ネットワークのドメインネームシステムの DNS を更新する方法に関する情報を確認します。|![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーションサーバーの名前解決に](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807041(v=ws.11))関するフェデレーションサーバーの要件の設定|
|フェデレーションサーバーにするコンピューターを、アカウントパートナーフォレストまたはリソースパートナーフォレスト内のドメインに参加させます。このドメインは、そのフォレストのユーザーの認証に使用されるか、または信頼する側のフォレストによって認証されます。 **注:** アカウントパートナー組織でフェデレーションサーバーをセットアップする場合は、まず、そのコンピューターをフォレスト内の任意のドメインに参加させる必要があります。この場合、フェデレーションサーバーを使用して、そのフォレストのユーザーや信頼する側のフォレストからユーザーを認証します。|![フェデレーションサーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[ドメインへのコンピューターの参加](Join-a-Computer-to-a-Domain.md)|
|フェデレーションサーバーの DNS ホスト名をフェデレーションサーバーの IP アドレスに指す、企業ネットワークの DNS に新しいリソースレコードを作成します。|![フェデレーションサーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーションサーバーの会社の DNS に&#41; リソースレコード &#40;ホストを追加する](Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md)|
|\(省略可能フェデレーションサーバーを \) フェデレーションサーバーファームに追加する場合は、最初にファーム内の最初のフェデレーションサーバーにある既存のトークン署名証明書の秘密キーをエクスポートして、 \- \( \) 他のフェデレーションサーバーが同じ証明書をインポートする必要があるときに証明書のファイル形式を使用できるようにすることが必要になる場合があります。<p>発行されたサーバー認証証明書を \( エクスポートし \) たり、ファーム内の各フェデレーションサーバーに対して一意のサーバー認証証明書を取得したりする必要がない場合、発行されたサーバー認証証明書を複数のコンピューターで再利用する場合は、秘密キーをエクスポートする必要はありません。 **注:** AD FS 管理スナップインは、 \- サービス通信証明書としてのフェデレーションサーバーのサーバー認証証明書を参照します。|![フェデレーションサーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[サーバー認証証明書の秘密キーの部分をエクスポート](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md)する|
|証明機関の CA からサーバー認証証明書または秘密キーを取得した後 \( \) \( \) 、各フェデレーションサーバーの既定の Web サイトに証明書ファイルをインポートする必要があります。 **注:** AD FS フェデレーションサーバー構成ウィザードを使用するには、この証明書を既定の Web サイトにインストールする必要があります。|![フェデレーションサーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[サーバー認証証明書を既定の Web サイトにインポートする](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)|
|\(省略可能 \) 。 CA からサーバー認証証明書を取得する代わりに、インターネットインフォメーションサービス IIS を使用して、 \( \) フェデレーションサーバーのサンプル証明書を作成できます。 **注意:** 自己 \- 署名サーバー認証証明書を使用して運用環境にフェデレーションサーバーを展開することは、セキュリティのベストプラクティスではありません。|![フェデレーションサーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[IIS: 自己 \- 署名入りのサーバー証明書を作成](https://go.microsoft.com/fwlink/?LinkID=108271)し、「[サーバー認証証明書を既定の Web サイトにインポートする](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)」の手順を完了します。|
|アカウントパートナー組織でフェデレーションサーバーファーム環境を構成する場合は、ファームが存在する AD DS Active Directory Domain Services で専用のサービスアカウントを作成して構成し、 \( \) このアカウントを使用するようにファーム内の各フェデレーションサーバーを構成する必要があります。 この手順を実行すると、企業ネットワーク上のクライアントは、Windows 統合認証を使用して、ファーム内の任意のフェデレーションサーバーに対して認証を行うことができます。|![フェデレーションサーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーションサーバーファームのサービスアカウントを手動で構成する](Manually-Configure-a-Service-Account-for-a-Federation-Server-Farm.md)|
|フェデレーションサーバーとなるコンピューターにフェデレーションサービスの役割サービスをインストールします。|![フェデレーションサーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーションサービスの役割サービスのインストール](Install-the-Federation-Service-Role-Service.md)|
|AD FS フェデレーションサーバー構成ウィザードを使用して、フェデレーションサーバーの役割で動作するようにコンピューターの AD FS ソフトウェアを構成します。<p>スタンドアロンフェデレーションサーバーをセットアップする場合 \- 、新しいファームに最初のフェデレーションサーバーを作成する場合、または既存のフェデレーションサーバーファームにコンピューターを参加させる場合は、次の手順に従います。 **注:** フェデレーション Web シングルサイン \- オン SSO 設計では、 \( \) アカウントパートナー組織に少なくとも1つのフェデレーションサーバーがあり、リソースパートナー組織に少なくとも1つのフェデレーションサーバーが必要です。|![フェデレーションサーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[スタンドアロンフェデレーションサーバーを作成](Create-a-Stand-Alone-Federation-Server.md)する<p>![フェデレーションサーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーションサーバーファームに最初のフェデレーションサーバーを作成](Create-the-First-Federation-Server-in-a-Federation-Server-Farm.md)する<p>![フェデレーションサーバーのセットアップフェデレーションサーバー](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[ファームへのフェデレーションサーバーの追加](Add-a-Federation-Server-to-a-Federation-Server-Farm.md)|
|\(省略可能 \) AD FS 管理スナップインを使用して、 \- 設計を展開するために必要な AD FS 証明書を追加して構成します。 スナップインを使用して証明書を追加または変更する場合の詳細については \- 、「[フェデレーションサーバーの証明書の要件](../design/certificate-requirements-for-federation-servers.md)」を参照してください。|![フェデレーションサーバーのセットアップ](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[トークン署名証明書の追加](Add-a-Token-Signing-Certificate.md)<p>![フェデレーションサーバーのセットアップ](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[トークン暗号化解除証明書の追加](Add-a-Token-Decrypting-Certificate.md)<p>![フェデレーションサーバーのセットアップ](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[サービス通信証明書の設定](Set-a-Service-Communications-Certificate.md)|
|これが組織内の最初のフェデレーションサーバーである場合は、AD FS の設計に準拠するようにフェデレーションサービスを構成します。|![フェデレーションサーバーのセットアップの](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト: アカウントパートナー組織の構成](Checklist--Configuring-the-Account-Partner-Organization.md)<p>![フェデレーションサーバーのセットアップの](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト: リソースパートナー組織の構成](Checklist--Configuring-the-Resource-Partner-Organization.md)|
|クライアントコンピューターから、フェデレーションサーバーが動作可能であることを確認します。|![フェデレーションサーバーのセットアップ](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーションサーバーが動作していることを確認する](Verify-That-a-Federation-Server-Is-Operational.md)|
