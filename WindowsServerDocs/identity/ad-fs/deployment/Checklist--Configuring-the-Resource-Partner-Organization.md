---
ms.assetid: 80d50a9f-428e-40fe-b6b3-9837fd9a3efc
title: チェックリスト-リソースパートナー組織の構成
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 342214d03441b7394baa5f0219e448622b389225
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408539"
---
# <a name="checklist-configuring-the-resource-partner-organization"></a>チェックリスト:リソースパートナー組織の構成

リソースパートナー組織には、アカウントパートナーのユーザーがアクセスする Web @ no__t ベースのアプリケーションをホストする Web サーバーが含まれています。 この組織の管理者は、アカウントパートナー組織との信頼関係を表すために要求プロバイダー信頼を作成するために、AD FS 管理スナップ @ no__t-0in 使用する必要があります。 さらに、アカウントパートナー管理者は、信頼する各アカウントパートナー組織に対して、証明書利用者信頼を作成する必要があります。  
  
このチェックリストには、リソースパートナー組織で Active Directory フェデレーションサービス (AD FS) \(AD FS @ no__t-1 を展開するために必要なタスクが含まれています。 また、フェデレーションパートナーシップの1つの @ no__t-0half を確立するために必要なコンポーネントを構成するためのタスクも含まれています。  
  
[WEB SSO 設計](https://technet.microsoft.com/library/dd807033.aspx)をデプロイする場合は、このチェックリストに従う必要はありません。 ただし、[フェデレーション WEB SSO 設計](https://technet.microsoft.com/library/dd807050.aspx)を正常に展開するには、このチェックリストのタスクを完了する必要があります。  
  
> [!IMPORTANT]  
> アカウントパートナー組織の管理者が @no__t のチェックリストのガイダンスに従っていることを確認します。アカウントパートナー組織 @ no__t-0 を構成して、フェデレーションパートナーシップの後半を正常に作成するために必要なすべての展開タスクが完了するようにします。  
  
> [!NOTE]  
> このチェックリストのタスクは順番に実行してください。 参照リンクによって手順に移動した場合は、このチェックリストの残りのタスクを進めることができるように、その手順の作業が完了したらこのトピックに戻ります。  
  
![ リソースパートナー組織 @ no__t の構成-1Checklist リスト:リソースパートナー組織の構成 @ no__t-0  
  
||タスク|参照|  
|-|--------|-------------|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|現在の運用環境に既存の AD FS 1.0 または1.1 のデプロイがある場合は、現在のフェデレーションサービスから新しい AD FS フェデレーションサービスに設定を移行する方法については、右側のリンクを参照してください。 AD FS を使用して組織内で初めて AD FS を展開する場合は、この手順をスキップし、このチェックリストの次のタスクに進んで、新しいリソースパートナー組織を設定する方法についての情報を確認できます。|![configure パートナー組織](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[を構成 AD FS への移行を計画](https://technet.microsoft.com/library/ff678044.aspx)する|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|展開の目標に基づいて、ユーザーにフェデレーションアプリケーションへのアクセスを提供するために必要なコンポーネントに関する情報を確認します。|![configure リソースパートナー組織](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[は、Active Directory ユーザーに要求に対応するアプリケーションとサービスへのアクセスを提供](https://technet.microsoft.com/library/dd807071.aspx)します<br /><br />![configure リソースパートナー組織は、](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Active Directory ユーザーに他の組織のアプリケーションとサービスへのアクセスを提供します](https://technet.microsoft.com/library/dd807123.aspx)。<br /><br />![configure リソースパートナー組織](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[は、別の組織のユーザーに、要求に対応するアプリケーションとサービスへのアクセスを提供し](https://technet.microsoft.com/library/dd807099.aspx)ます。|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|このリソースパートナー組織が関連付けられる AD FS 設計を決定します。|![configure パートナー組織の](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[WEB SSO 設計](https://technet.microsoft.com/library/dd807033.aspx)を構成する<br /><br />![ リソースパートナー組織の](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション WEB SSO 設計](https://technet.microsoft.com/library/dd807050.aspx)を構成する|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|さまざまなアプリケーションの種類を確認し、展開するアプリケーションを決定します。|![configure パートナー組織で、リソース](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[パートナーのフェデレーションアプリケーション戦略を決定](https://technet.microsoft.com/library/dd807077.aspx)する|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|AD FS サーバーのデプロイを開始する前に、「」を確認してください。1. \) AD FS 構成データベースを格納するための Windows Internal Database \(WID @ no__t-2 または SQL Server を選択した場合の長所と短所。 \)AD FS 展開トポロジの種類と、それに関連付けられているサーバーの配置とネットワークレイアウトに関する推奨事項。|![configure パートナー組織で](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS デプロイトポロジを決定](https://technet.microsoft.com/library/gg982491.aspx)する<br /><br />![configure パートナー組織](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 展開トポロジに関する考慮事項](https://technet.microsoft.com/library/gg982489.aspx)|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|AD FS 容量計画のガイダンスを確認して、運用環境で使用する必要があるフェデレーションサーバーとフェデレーションサーバープロキシサーバーの適切な数を決定します。|@no__t-](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[0configure サーバー容量に対するリソースパートナー組織の計画を](https://technet.microsoft.com/library/gg749899.aspx)構成する|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|アカウントパートナー展開の物理的なトポロジを効果的に計画および実装するには、AD FS の設計に1つ以上のフェデレーションサーバーまたはフェデレーションサーバープロキシが必要かどうかを判断します。|![ リソースパートナー組織 @ no__t の構成-1Checklist リスト:フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)<br /><br />![ リソースパートナー組織 @ no__t の構成-1Checklist リスト:フェデレーション サーバー プロキシのセットアップ](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|AD FS に追加する属性ストアの種類を決定します。 次に、の AD FS 管理スナップイン @ no__t を使用して、属性ストアを追加します。|![configure パートナー組織](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[の属性ストアの役割を](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md)構成する<br /><br />![configure リソースパートナー組織の](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[属性ストアの追加](../../ad-fs/operations/Add-an-Attribute-Store.md)|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|AD FS 1.0 または1.1 フェデレーションサービスを使用しているアカウントパートナーから要求を送信または使用する必要がある場合は、以前のバージョンの AD FS と相互運用できるように AD FS を構成する方法については、右側のリンクを参照してください。 アカウントパートナー組織が AD FS を使って組織に要求を送信または使用している場合は、この手順をスキップして、このチェックリストの次の作業を続行することもできます。|@no__t-](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[0configure 1.x との相互運用性のために](https://technet.microsoft.com/library/ff678040.aspx)リソースパートナー組織の計画を構成する|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|リソースパートナー組織に最初のフェデレーションサーバーを展開した後、の AD FS 管理スナップイン @ no__t を使用して、要求プロバイダーの信頼関係を作成します。 要求プロバイダー信頼を作成するには、アカウントパートナーに関するデータを手動で入力するか、アカウントパートナー組織の管理者が提供するフェデレーションメタデータ URL を使用します。 このフェデレーション メタデータを使用して、リソース パートナーに関するデータを自動的に取得することができます。 **注:** アカウントパートナーがフェデレーションメタデータを公開する場合、または使用するためにファイルのコピーを提供できる場合は、時間を節約できるため、データを自動的に取得することをお勧めします。|![configure パートナー組織](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[で証明書利用者信頼を手動で作成](../operations/create-a-relying-party-trust.md#to-create-a-claims-aware-relying-party-trust-manually)する<br /><br />![configure パートナー組織](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[で、フェデレーションメタデータを使用して証明書利用者信頼を作成](../operations/create-a-relying-party-trust.md#to-create-a-claims-aware-relying-party-trust-using-federation-metadata)する|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|組織のニーズに応じて、要求プロバイダー AD FS 信頼ごとに1つまたは複数の要求規則セットを作成します。これにより、入力方向の要求が no__t に渡され、変換されるか、適切にマップされます。リソースパートナー内の対応する要求。|![ リソースパートナー組織 @ no__t の構成-1Checklist リスト:要求プロバイダー信頼の要求規則の作成](Checklist--Creating-Claim-Rules-for-a-Claims-Provider-Trust.md)|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|\(Optional @ no__t-1 組織のニーズを満たす要求の説明が存在しない場合は、要求の説明を作成する必要があります。 AD FS には、の AD FS 管理スナップインで公開される要求説明の既定のセットが含まれています。|![configure リソースパートナー組織](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[の要求の説明の追加](../../ad-fs/operations/Add-a-Claim-Description.md)|  
