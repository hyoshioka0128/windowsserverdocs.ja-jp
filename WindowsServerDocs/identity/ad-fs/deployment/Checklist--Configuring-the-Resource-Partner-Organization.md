---
ms.assetid: 80d50a9f-428e-40fe-b6b3-9837fd9a3efc
title: チェックリスト-リソースパートナー組織の構成
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 6a66758f02d3b1edfa35168df95f0c765ca8949e
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966364"
---
# <a name="checklist-configuring-the-resource-partner-organization"></a>チェックリスト: リソースパートナー組織の構成

リソースパートナー組織には、アカウントパートナーのユーザーがアクセスする Web ベースアプリケーションをホストする Web サーバーが含まれてい \- ます。 この組織の管理者は、AD FS 管理スナップインを使用して、 \- 要求プロバイダー信頼を作成し、アカウントパートナー組織との信頼関係を表す必要があります。 さらに、アカウントパートナー管理者は、信頼する各アカウントパートナー組織に対して、証明書利用者信頼を作成する必要があります。  
  
このチェックリストには、 \( リソースパートナー組織に Active Directory フェデレーションサービス (AD FS) AD FS を展開するために必要なタスクが含まれてい \) ます。 また、フェデレーションパートナーシップの半分を確立するために必要なコンポーネントを構成するためのタスクも含まれてい \- ます。  
  
[WEB SSO 設計](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807033(v=ws.11))をデプロイする場合は、このチェックリストに従う必要はありません。 ただし、[フェデレーション WEB SSO 設計](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807050(v=ws.11))を正常に展開するには、このチェックリストのタスクを完了する必要があります。  
  
> [!IMPORTANT]  
> アカウントパートナー組織の管理者が、 [「チェックリスト: アカウントパートナー組織の構成](Checklist--Configuring-the-Account-Partner-Organization.md)」に記載されているガイダンスに従って、フェデレーションパートナーシップの後半を正常に作成するために必要なすべての展開タスクが完了するようにしてください。  
  
> [!NOTE]  
> このチェックリストのタスクは順番に実行してください。 参照リンクによって手順に移動した場合は、このチェックリストの残りのタスクを進めることができるように、その手順の作業が完了したらこのトピックに戻ります。  
  
![リソースパートナー](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**組織のチェックリストの構成: リソースパートナー組織の構成**  
  
||タスク|リファレンス|  
|-|--------|-------------|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|現在の運用環境に既存の AD FS 1.0 または1.1 のデプロイがある場合は、現在のフェデレーションサービスから新しい AD FS フェデレーションサービスに設定を移行する方法については、右側のリンクを参照してください。 AD FS を使用して組織内で初めて AD FS を展開する場合は、この手順をスキップし、このチェックリストの次のタスクに進んで、新しいリソースパートナー組織を設定する方法についての情報を確認できます。|![リソースパートナー組織](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[の構成の AD FS への移行の計画](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff678044(v=ws.10))|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|展開の目標に基づいて、ユーザーにフェデレーションアプリケーションへのアクセスを提供するために必要なコンポーネントに関する情報を確認します。|![リソースパートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[: Active Directory ユーザーが要求に対応するアプリケーションとサービスにアクセスできるようにし](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807071(v=ws.11))ます。<p>![リソースパートナー組織](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[の構成他の組織のアプリケーションとサービスへのアクセスを Active Directory ユーザーに提供する](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807123(v=ws.11))<p>![リソースパートナー組織](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[の構成別の組織のユーザーに、要求に対応するアプリケーションとサービスへのアクセスを提供する](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807099(v=ws.11))|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|このリソースパートナー組織が関連付けられる AD FS 設計を決定します。|![リソースパートナー組織の](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[WEB SSO 設計](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807033(v=ws.11))を構成する<p>![リソースパートナー組織の](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション WEB SSO 設計](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807050(v=ws.11))の構成|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|さまざまなアプリケーションの種類を確認し、展開するアプリケーションを決定します。|![リソースパートナー組織の構成リソースパートナー](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[でのフェデレーションアプリケーション戦略の決定](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807077(v=ws.11))|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|AD FS サーバーのデプロイを開始する前に、「」を確認してください。1. \) \( \) AD FS 構成データベース 2 \) を格納するために、Windows Internal Database WID または SQL Server を選択する利点と欠点。AD FS 展開トポロジの種類と、それに関連付けられているサーバーの配置とネットワークレイアウトに関する推奨事項。|![リソースパートナー組織](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[の構成 AD FS デプロイトポロジの決定](../design/determine-your-ad-fs-deployment-topology.md)<p>![リソースパートナー組織](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS の展開トポロジに関する考慮事項](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/gg982489(v=ws.11))の構成|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|AD FS 容量計画のガイダンスを確認して、運用環境で使用する必要があるフェデレーションサーバーとフェデレーションサーバープロキシサーバーの適切な数を決定します。|![リソースパートナー組織](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[の AD FS サーバー容量の計画を](../design/planning-for-ad-fs-server-capacity.md)構成する|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|アカウントパートナー展開の物理的なトポロジを効果的に計画および実装するには、AD FS の設計に1つ以上のフェデレーションサーバーまたはフェデレーションサーバープロキシが必要かどうかを判断します。|![リソースパートナー組織](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[の構成のチェックリスト: フェデレーションサーバーの](Checklist--Setting-Up-a-Federation-Server.md)セットアップ<p>![リソースパートナー組織](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[の構成のチェックリスト: フェデレーションサーバープロキシの設定](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|AD FS に追加する属性ストアの種類を決定します。 次に、AD FS 管理スナップインを使用して、属性ストアを追加し \- ます。|![リソースパートナー組織](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[の属性ストアの役割を](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md)構成する<p>![リソースパートナー組織の](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[属性ストアの追加を](../../ad-fs/operations/Add-an-Attribute-Store.md)構成する|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|AD FS 1.0 または1.1 フェデレーションサービスを使用しているアカウントパートナーから要求を送信または使用する必要がある場合は、以前のバージョンの AD FS と相互運用できるように AD FS を構成する方法については、右側のリンクを参照してください。 アカウントパートナー組織が AD FS を使って組織に要求を送信または使用している場合は、この手順をスキップして、このチェックリストの次の作業を続行することもできます。|![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 1.x との相互運用性のために](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ff678040(v=ws.11))リソースパートナー組織の計画を構成する|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|リソースパートナー組織に最初のフェデレーションサーバーを展開した後、AD FS 管理スナップインを使用して、要求プロバイダーの信頼関係を作成し \- ます。 要求プロバイダー信頼を作成するには、アカウントパートナーに関するデータを手動で入力するか、アカウントパートナー組織の管理者が提供するフェデレーションメタデータ URL を使用します。 このフェデレーション メタデータを使用して、リソース パートナーに関するデータを自動的に取得することができます。 **注:** アカウントパートナーがフェデレーションメタデータを公開する場合、または使用するためにファイルのコピーを提供できる場合は、時間を節約できるため、データを自動的に取得することをお勧めします。|![リソースパートナー組織](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[の構成証明書利用者信頼を手動で作成](../operations/create-a-relying-party-trust.md#to-create-a-claims-aware-relying-party-trust-manually)する<p>![リソースパートナー組織](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[の構成フェデレーションメタデータを使用して証明書利用者信頼を作成](../operations/create-a-relying-party-trust.md#to-create-a-claims-aware-relying-party-trust-using-federation-metadata)する|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|組織のニーズに応じて、AD FS 管理スナップインで指定されている要求プロバイダー信頼ごとに1つまたは複数の要求規則セットを作成し \- ます。これにより、入力方向の要求は、リソースパートナーの対応する要求に適切に渡されるか、変換されるか、またはマップされます。|![リソースパートナー組織](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[のチェックリストの構成: 要求プロバイダー信頼の要求規則の作成](Checklist--Creating-Claim-Rules-for-a-Claims-Provider-Trust.md)|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|\(必要に応じて、 \) 組織のニーズを満たす要求の説明が存在しない場合は、要求の説明を作成する必要があります。 AD FS には、AD FS 管理スナップインで公開される要求説明の既定のセットが含まれてい \- ます。|![リソースパートナー組織](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[の構成要求の説明の追加](../../ad-fs/operations/Add-a-Claim-Description.md)|  
