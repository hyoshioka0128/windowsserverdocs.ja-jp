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
# <a name="checklist-configuring-the-resource-partner-organization"></a>チェックリスト: リソースパートナー組織の構成

リソースパートナー組織には、アカウントパートナーのユーザーがアクセスする Web\-ベースのアプリケーションをホストする Web サーバーが含まれています。 この組織の管理者は、の AD FS 管理スナップ\-を使用して、アカウントパートナー組織との信頼関係を表す要求プロバイダー信頼を作成する必要があります。 さらに、アカウントパートナー管理者は、信頼する各アカウントパートナー組織に対して、証明書利用者信頼を作成する必要があります。  
  
このチェックリストには Active Directory フェデレーションサービス (AD FS) \(AD FS\) をリソースパートナー組織に展開するために必要なタスクが含まれています。 また、フェデレーションパートナーシップの 1\-半分を確立するために必要なコンポーネントを構成するためのタスクも含まれています。  
  
[WEB SSO 設計](https://technet.microsoft.com/library/dd807033.aspx)をデプロイする場合は、このチェックリストに従う必要はありません。 ただし、[フェデレーション WEB SSO 設計](https://technet.microsoft.com/library/dd807050.aspx)を正常に展開するには、このチェックリストのタスクを完了する必要があります。  
  
> [!IMPORTANT]  
> アカウントパートナー組織の管理者が、 [「チェックリスト: アカウントパートナー組織の構成](Checklist--Configuring-the-Account-Partner-Organization.md)」に記載されているガイダンスに従って、フェデレーションパートナーシップの後半を正常に作成するために必要なすべての展開タスクが完了するようにしてください。  
  
> [!NOTE]  
> このチェックリストのタスクは順番に実行してください。 参照リンクによって手順に移動した場合は、このチェックリストの残りのタスクを進めることができるように、その手順の作業が完了したらこのトピックに戻ります。  
  
リソースパートナー](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**組織のチェックリストを構成 ![: リソースパートナー組織の構成**  
  
||タスク|リファレンス|  
|-|--------|-------------|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|現在の運用環境に既存の AD FS 1.0 または1.1 のデプロイがある場合は、現在のフェデレーションサービスから新しい AD FS フェデレーションサービスに設定を移行する方法については、右側のリンクを参照してください。 AD FS を使用して組織内で初めて AD FS を展開する場合は、この手順をスキップし、このチェックリストの次のタスクに進んで、新しいリソースパートナー組織を設定する方法についての情報を確認できます。|リソースパートナー組織の構成 ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS への移行を計画](https://technet.microsoft.com/library/ff678044.aspx)する|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|展開の目標に基づいて、ユーザーにフェデレーションアプリケーションへのアクセスを提供するために必要なコンポーネントに関する情報を確認します。|リソースパートナー組織の構成 ![、](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Active Directory ユーザーが要求に対応するアプリケーションとサービスにアクセスできるようにし](https://technet.microsoft.com/library/dd807071.aspx)ます。<br /><br />リソースパートナー組織の構成 ![、](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Active Directory ユーザーが他の組織のアプリケーションやサービスにアクセスできるようにします](https://technet.microsoft.com/library/dd807123.aspx)。<br /><br />リソースパートナー組織の構成 ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[別の組織のユーザーに、要求に対応するアプリケーションとサービスへのアクセスを提供する](https://technet.microsoft.com/library/dd807099.aspx)|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|このリソースパートナー組織が関連付けられる AD FS 設計を決定します。|リソースパートナー組織の](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[WEB SSO 設計](https://technet.microsoft.com/library/dd807033.aspx)を構成 ![には<br /><br />リソースパートナー組織の](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション WEB SSO 設計](https://technet.microsoft.com/library/dd807050.aspx)を構成 ![には|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|さまざまなアプリケーションの種類を確認し、展開するアプリケーションを決定します。|リソースパートナーの構成 ![リソースパートナー](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[でのフェデレーションアプリケーション戦略の決定](https://technet.microsoft.com/library/dd807077.aspx)|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|AD FS サーバーのデプロイを開始する前に、「」を確認してください。1. Windows Internal Database \(WID\) または SQL Server を選択して、AD FS 構成データベース2を格納するという\) の長所と短所があります。\) AD FS 展開トポロジの種類と、それに関連付けられているサーバーの配置とネットワークレイアウトに関する推奨事項を紹介します。|リソースパートナー組織の構成 ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS の展開トポロジを決定](https://technet.microsoft.com/library/gg982491.aspx)する<br /><br />リソースパートナー組織 AD FS の](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[展開トポロジに関する考慮事項](https://technet.microsoft.com/library/gg982489.aspx)を ![構成する|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|AD FS 容量計画のガイダンスを確認して、運用環境で使用する必要があるフェデレーションサーバーとフェデレーションサーバープロキシサーバーの適切な数を決定します。|](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS サーバー容量に対する](https://technet.microsoft.com/library/gg749899.aspx)リソースパートナー組織計画を構成 ![|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|アカウントパートナー展開の物理的なトポロジを効果的に計画および実装するには、AD FS の設計に1つ以上のフェデレーションサーバーまたはフェデレーションサーバープロキシが必要かどうかを判断します。|![リソースパートナー組織](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[のチェックリストの構成: フェデレーションサーバーの](Checklist--Setting-Up-a-Federation-Server.md)セットアップ<br /><br />![リソースパートナー組織](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[のチェックリストの構成: フェデレーションサーバープロキシの設定](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|AD FS に追加する属性ストアの種類を決定します。 次に、の AD FS 管理スナップ\-を使用して、属性ストアを追加します。|リソースパートナー組織の構成 ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[属性ストアの役割](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md)<br /><br />リソースパートナー組織の構成 ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[属性ストアの追加](../../ad-fs/operations/Add-an-Attribute-Store.md)|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|AD FS 1.0 または1.1 フェデレーションサービスを使用しているアカウントパートナーから要求を送信または使用する必要がある場合は、以前のバージョンの AD FS と相互運用できるように AD FS を構成する方法については、右側のリンクを参照してください。 アカウントパートナー組織が AD FS を使って組織に要求を送信または使用している場合は、この手順をスキップして、このチェックリストの次の作業を続行することもできます。|](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 1.x との相互運用性のために](https://technet.microsoft.com/library/ff678040.aspx)リソースパートナー組織の計画を構成 ![には|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|リソースパートナー組織に最初のフェデレーションサーバーを展開した後、の AD FS 管理スナップ\-を使用して、要求プロバイダーの信頼関係を作成します。 要求プロバイダー信頼を作成するには、アカウントパートナーに関するデータを手動で入力するか、アカウントパートナー組織の管理者が提供するフェデレーションメタデータ URL を使用します。 このフェデレーション メタデータを使用して、リソース パートナーに関するデータを自動的に取得することができます。 **注:** アカウントパートナーがフェデレーションメタデータを公開する場合、または使用するためにファイルのコピーを提供できる場合は、時間を節約できるため、データを自動的に取得することをお勧めします。|リソースパートナー組織の構成 ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[証明書利用者信頼を手動で作成](../operations/create-a-relying-party-trust.md#to-create-a-claims-aware-relying-party-trust-manually)する<br /><br />リソースパートナー組織の構成 ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[フェデレーションメタデータを使用して証明書利用者信頼を作成](../operations/create-a-relying-party-trust.md#to-create-a-claims-aware-relying-party-trust-using-federation-metadata)する|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|組織のニーズに応じて、AD FS 管理スナップ\-で指定されている要求プロバイダー信頼ごとに1つ以上の要求規則セットを作成します。これにより、入力方向の要求は、リソースパートナーの対応する要求に対してパススルー、変換、または適切にマップされます。|リソースパートナー組織](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[のチェックリストを構成 ![: 要求プロバイダー信頼の要求規則を作成する](Checklist--Creating-Claim-Rules-for-a-Claims-Provider-Trust.md)|  
|![リソースパートナー組織の構成](media/icon_checkboxo.gif)|必要に応じて、組織のニーズを満たす要求の説明が存在しない場合は、要求の説明を作成する必要があり\) \(ます。 AD FS には、の AD FS 管理スナップ\-インで公開される要求説明の既定のセットが含まれています。|リソースパートナー組織の構成 ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[要求の説明の追加](../../ad-fs/operations/Add-a-Claim-Description.md)|  
