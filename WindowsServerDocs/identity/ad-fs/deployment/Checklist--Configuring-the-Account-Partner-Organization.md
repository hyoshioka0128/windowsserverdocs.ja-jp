---
ms.assetid: 826974ea-3635-40df-aa37-77dd12a363c8
title: チェックリスト-アカウントパートナー組織の構成
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.author: billmath
ms.openlocfilehash: e1fc3dea0d25cc428081964372dc2269d78c9d6d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87938581"
---
# <a name="checklist-configuring-the-account-partner-organization"></a>チェックリスト: アカウントパートナー組織の構成

アカウントパートナー組織には、リソースパートナーの Web ベースアプリケーションにアクセスするユーザーが含まれてい \- ます。 この組織の管理者は、リソースパートナー組織との信頼関係を表すために、AD FS 管理スナップインを使用して \- 証明書利用者信頼を作成する必要があります。 さらに、リソースパートナーの管理者は、信頼する各アカウントパートナー組織に対して、要求プロバイダー信頼を作成する必要があります。

このチェックリストには \( \) 、アカウントパートナー組織に Active Directory フェデレーションサービス (AD FS) AD FS を展開するためのタスクが含まれています。 また、フェデレーションパートナーシップの半分を確立するために必要なコンポーネントを構成するためのタスクも含まれてい \- ます。

[WEB SSO 設計](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807033(v=ws.11))をデプロイする場合は、このチェックリストに従う必要はありません。 ただし、[フェデレーション WEB SSO 設計](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807050(v=ws.11))を正常に展開するには、このチェックリストのタスクを完了する必要があります。

> [!IMPORTANT]
> リソースパートナー組織の管理者が、 [「チェックリスト: リソースパートナー組織の構成](Checklist--Configuring-the-Resource-Partner-Organization.md)」のガイダンスに従って、フェデレーションパートナーシップの後半を正常に作成するために必要なすべての展開タスクが完了するようにしてください。

> [!NOTE]
> このチェックリストのタスクは順番に実行してください。 参照リンクによって手順に移動した場合は、このチェックリストの残りのタスクを進めることができるように、その手順の作業が完了したらこのトピックに戻ります。

![アカウントパートナー](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**組織のチェックリストの構成: アカウントパートナー組織の構成**

|タスク|リファレンス|
|--------|-------------|
|現在の運用環境に既存の AD FS 1.0 または1.1 のデプロイがある場合は、現在のフェデレーションサービスから新しい AD FS フェデレーションサービスに設定を移行する方法については、右側のリンクを参照してください。 AD FS を使用して組織で初めて AD FS を展開する場合は、この手順をスキップして、このチェックリストの次の作業に進み、新しいアカウントパートナー組織のセットアップ方法についての情報を確認してください。|![アカウントパートナー組織](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[の組織計画 AD FS 2.0 への移行を](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff678044(v=ws.10))構成する|
|展開の目標に基づいて、ユーザーにフェデレーションアプリケーションへのアクセスを提供するために必要なコンポーネントに関する情報を確認します。|![アカウントパートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[要求に対応するアプリケーションとサービスへのアクセスを Active Directory ユーザーに提供](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807071(v=ws.11))します<p>![アカウントパートナー組織](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[の構成他の組織のアプリケーションとサービスへのアクセスを Active Directory ユーザーに提供する](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807123(v=ws.11))<p>![アカウントパートナー組織](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[の構成別の組織のユーザーに、要求に対応するアプリケーションとサービスへのアクセスを提供する](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807099(v=ws.11))|
|このアカウントパートナー組織が関連付けられる AD FS 設計を決定します。|![アカウントパートナー組織の](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[WEB SSO 設計](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807033(v=ws.11))を構成する<p>![アカウントパートナー組織の](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション WEB SSO 設計](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807050(v=ws.11))を構成する|
|AD FS サーバーのデプロイを開始する前に、「」を確認してください。1. \) \( \) AD FS 構成データベース 2 \) を格納するために、Windows Internal Database WID または SQL Server を選択する利点と欠点。AD FS 展開トポロジの種類と、それに関連付けられているサーバーの配置とネットワークレイアウトに関する推奨事項。|![アカウントパートナー組織](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[の構成 AD FS の展開トポロジを決定](../design/determine-your-ad-fs-deployment-topology.md)する<p>![アカウントパートナー組織](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 展開トポロジに関する考慮事項](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/gg982489(v=ws.11))を構成する|
|AD FS 容量計画のガイダンスを確認して、運用環境で使用する必要があるフェデレーションサーバーとフェデレーションサーバープロキシサーバーの適切な数を決定します。|![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS サーバー容量に対するアカウントパートナー組織の計画を](../design/planning-for-ad-fs-server-capacity.md)構成する|
|アカウントパートナー展開の物理的なトポロジを効果的に計画および実装するには、AD FS の設計に1つ以上のフェデレーションサーバーまたはフェデレーションサーバープロキシが必要かどうかを判断します。|![アカウントパートナー組織](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[の構成のチェックリスト: フェデレーションサーバーの](Checklist--Setting-Up-a-Federation-Server.md)セットアップ<p>![アカウントパートナー組織](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[の構成のチェックリスト: フェデレーションサーバープロキシの設定](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|
|AD FS に追加する属性ストアの種類を決定します。 次に、AD FS 管理スナップインを使用して、属性ストアを追加し \- ます。|![アカウントパートナー組織](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[の属性ストアの役割を](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md)構成する<p>![アカウントパートナー組織の](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[属性ストアの追加を](../../ad-fs/operations/Add-an-Attribute-Store.md)構成する|
|AD FS 1.0 または1.1 フェデレーションサービスのいずれかを使用しているリソースパートナーとの間で要求を送信または使用する必要がある場合は、以前のバージョンの AD FS と相互運用できるように AD FS を構成する方法については、右側のリンクを参照してください。 リソースパートナー組織が AD FS を使って組織に要求を送信または使用している場合は、この手順をスキップして、このチェックリストの次の作業を続行できます。|![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 1.x との相互運用性のために](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ff678040(v=ws.11))アカウントパートナー組織の組織計画を構成する|
|アカウントパートナー組織に最初のフェデレーションサーバーを展開した後、AD FS 管理スナップインを使用して証明書利用者の信頼関係を作成し \- ます。 証明書利用者信頼を作成するには、リソース パートナーに関するデータを手動で入力するか、リソース パートナーの組織の管理者から入手したフェデレーション メタデータ URL を使用します。 このフェデレーション メタデータを使用して、リソース パートナーに関するデータを自動的に取得することができます。 **注:** リソースパートナーがフェデレーションメタデータを公開する場合、または使用するためにファイルのコピーを提供できる場合は、時間を節約できるため、データを自動的に取得することをお勧めします。|![アカウントパートナー組織](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[の構成証明書利用者信頼を手動で作成](../../ad-fs/operations/Create-a-Relying-Party-Trust.md)する<p>![アカウントパートナー組織](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[の構成フェデレーションメタデータを使用して証明書利用者信頼を作成](../../ad-fs/operations/Create-a-Relying-Party-Trust.md)する|
|組織のニーズに応じて、要求が適切に発行されるように、AD FS 管理スナップインで指定されている証明書利用者信頼ごとに1つまたは複数の要求規則セットを作成し \- ます。|![アカウントパートナー組織](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[のチェックリストを構成する: 証明書利用者信頼の要求規則を作成](Checklist--Creating-Claim-Rules-for-a-Relying-Party-Trust.md)する|
|要求の説明は、組織のニーズを満たすものが存在しない場合に作成する必要があります。 AD FS には、AD FS 管理スナップインで公開される要求説明の既定のセットが付属してい \- ます。|![アカウントパートナー組織](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[の構成要求の説明の追加](../../ad-fs/operations/Add-a-Claim-Description.md)|
|組織で id 委任を使用して、指定されたアカウントを "操作" または他のユーザーに対して承認または制限する必要があるかどうかを判断します。 これは、フロント \- エンド web アプリケーションがバックエンド web サービスと対話する必要がある場合に必要となることがよくあり \- ます。|![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Id 委任を使用する場合の](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807122(v=ws.11))アカウントパートナー組織の構成|
|フェデレーションのためにクライアントコンピューターを準備する方法:<p>-アカウントパートナーのフェデレーションサーバーの URL を、クライアントブラウザーの信頼済みサイトの一覧に追加します。<br />-グループポリシーを使用して、適切な Secure Sockets Layer \( SSL \) 証明書をクライアントコンピューターにプッシュします。|![アカウントパートナー組織の構成アカウント](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[パートナーでのクライアントコンピューターの準備](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807114(v=ws.11))<p>![アカウントパートナー組織](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[の構成アカウントフェデレーションサーバーを信頼するようにクライアントコンピューターを構成](Configure-Client-Computers-to-Trust-the-Account-Federation-Server.md)する<p>![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[グループポリシーを使用して、アカウントパートナー組織の証明書をクライアントコンピューターに配布するように](Distribute-Certificates-to-Client-Computers-by-Using-Group-Policy.md)構成する|
