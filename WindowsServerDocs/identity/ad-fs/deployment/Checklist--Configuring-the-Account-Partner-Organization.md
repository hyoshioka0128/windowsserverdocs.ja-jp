---
ms.assetid: 826974ea-3635-40df-aa37-77dd12a363c8
title: チェックリスト-アカウントパートナー組織の構成
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 73ccbfc5194b36d8612daa7175561539d7a69dff
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71360008"
---
# <a name="checklist-configuring-the-account-partner-organization"></a>チェックリスト:アカウント パートナー組織の構成

アカウントパートナー組織には、リソースパートナーの Web @ no__t ベースのアプリケーションにアクセスするユーザーが含まれています。 この組織の管理者は、リソースパートナー組織との信頼関係を表すために証明書利用者信頼を作成するために、AD FS Management snap @ no__t-0in 使用する必要があります。 さらに、リソースパートナーの管理者は、信頼する各アカウントパートナー組織に対して、要求プロバイダー信頼を作成する必要があります。  
  
このチェックリストには、アカウントパートナー組織に Active Directory フェデレーションサービス (AD FS) @no__t 0AD FS @ no__t-1 を展開するためのタスクが含まれています。 また、フェデレーションパートナーシップの1つの @ no__t-0half を確立するために必要なコンポーネントを構成するためのタスクも含まれています。  
  
[WEB SSO 設計](https://technet.microsoft.com/library/dd807033.aspx)をデプロイする場合は、このチェックリストに従う必要はありません。 ただし、[フェデレーション WEB SSO 設計](https://technet.microsoft.com/library/dd807050.aspx)を正常に展開するには、このチェックリストのタスクを完了する必要があります。  
  
> [!IMPORTANT]  
> リソースパートナー組織の管理者が @no__t のチェックリストのガイダンスに従っていることを確認します。リソースパートナー組織 @ no__t-0 を構成して、フェデレーションパートナーシップの後半を正常に作成するために必要なすべての展開タスクが完了するようにします。  
  
> [!NOTE]  
> このチェックリストのタスクは順番に実行してください。 参照リンクによって手順に移動した場合は、このチェックリストの残りのタスクを進めることができるように、その手順の作業が完了したらこのトピックに戻ります。  
  
![configure partner org @ no__t の構成-1Checklist リスト:アカウントパートナー組織の構成 @ no__t-0  
  
||タスク|参照|  
|-|--------|-------------|  
|![アカウントパートナー組織の構成](media/icon_checkboxo.gif)|現在の運用環境に既存の AD FS 1.0 または1.1 のデプロイがある場合は、現在のフェデレーションサービスから新しい AD FS フェデレーションサービスに設定を移行する方法については、右側のリンクを参照してください。 AD FS を使用して組織で初めて AD FS を展開する場合は、この手順をスキップして、このチェックリストの次の作業に進み、新しいアカウントパートナー組織のセットアップ方法についての情報を確認してください。|![configure パートナー組織](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[の組織計画 AD FS 2.0 への移行を](https://technet.microsoft.com/library/ff678044.aspx)構成する|  
|![アカウントパートナー組織の構成](media/icon_checkboxo.gif)|展開の目標に基づいて、ユーザーにフェデレーションアプリケーションへのアクセスを提供するために必要なコンポーネントに関する情報を確認します。|![configure パートナー組織を構成して、](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Active Directory ユーザーに要求に対応するアプリケーションとサービスへのアクセスを提供する](https://technet.microsoft.com/library/dd807071.aspx)<br /><br />![configure パートナー組織を構成し、](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[他の組織のアプリケーションやサービスへのアクセス権を Active Directory ユーザーに提供します](https://technet.microsoft.com/library/dd807123.aspx)。<br /><br />![configure パートナー組織を構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[し、別の組織のユーザーに要求に対応するアプリケーションとサービスへのアクセスを提供する](https://technet.microsoft.com/library/dd807099.aspx)|  
|![アカウントパートナー組織の構成](media/icon_checkboxo.gif)|このアカウントパートナー組織が関連付けられる AD FS 設計を決定します。|![configure パートナー組織の](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[WEB SSO 設計](https://technet.microsoft.com/library/dd807033.aspx)を構成する<br /><br />![configure パートナー組織の](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション WEB SSO 設計](https://technet.microsoft.com/library/dd807050.aspx)を構成する|  
|![アカウントパートナー組織の構成](media/icon_checkboxo.gif)|AD FS サーバーのデプロイを開始する前に、「」を確認してください。1. \) AD FS 構成データベースを格納するための Windows Internal Database \(WID @ no__t-2 または SQL Server を選択した場合の長所と短所。 \)AD FS 展開トポロジの種類と、それに関連付けられているサーバーの配置とネットワークレイアウトに関する推奨事項。|![configure パートナー組織で](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS の展開トポロジを決定](https://technet.microsoft.com/library/gg982491.aspx)する<br /><br />![configure パートナー組織](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 展開トポロジに関する考慮事項](https://technet.microsoft.com/library/gg982489.aspx)|  
|![アカウントパートナー組織の構成](media/icon_checkboxo.gif)|AD FS 容量計画のガイダンスを確認して、運用環境で使用する必要があるフェデレーションサーバーとフェデレーションサーバープロキシサーバーの適切な数を決定します。|@no__t-](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[0configure サーバー容量に対するアカウントパートナー組織の計画を](https://technet.microsoft.com/library/gg749899.aspx)構成する|  
|![アカウントパートナー組織の構成](media/icon_checkboxo.gif)|アカウントパートナー展開の物理的なトポロジを効果的に計画および実装するには、AD FS の設計に1つ以上のフェデレーションサーバーまたはフェデレーションサーバープロキシが必要かどうかを判断します。|![configure partner org @ no__t の構成-1Checklist リスト:フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)<br /><br />![configure partner org @ no__t の構成-1Checklist リスト:フェデレーション サーバー プロキシのセットアップ](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|  
|![アカウントパートナー組織の構成](media/icon_checkboxo.gif)|AD FS に追加する属性ストアの種類を決定します。 次に、の AD FS 管理スナップイン @ no__t を使用して、属性ストアを追加します。|![configure パートナー組織](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[の属性ストアの役割を](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md)構成する<br /><br />![configure パートナー組織の](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[属性ストアを追加](../../ad-fs/operations/Add-an-Attribute-Store.md)する|  
|![アカウントパートナー組織の構成](media/icon_checkboxo.gif)|AD FS 1.0 または1.1 フェデレーションサービスのいずれかを使用しているリソースパートナーとの間で要求を送信または使用する必要がある場合は、以前のバージョンの AD FS と相互運用できるように AD FS を構成する方法については、右側のリンクを参照してください。 リソースパートナー組織が AD FS を使って組織に要求を送信または使用している場合は、この手順をスキップして、このチェックリストの次の作業を続行できます。|@no__t-](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[0configure 1.x との相互運用性のために](https://technet.microsoft.com/library/ff678040.aspx)アカウントパートナー組織の組織計画を構成する|  
|![アカウントパートナー組織の構成](media/icon_checkboxo.gif)|アカウントパートナー組織に最初のフェデレーションサーバーを展開したら、の AD FS 管理スナップインを使用して証明書利用者の信頼関係を作成します。 証明書利用者信頼を作成するには、リソース パートナーに関するデータを手動で入力するか、リソース パートナーの組織の管理者から入手したフェデレーション メタデータ URL を使用します。 このフェデレーション メタデータを使用して、リソース パートナーに関するデータを自動的に取得することができます。 **注:** リソース パートナーによってフェデレーション メタデータが公開されている場合、またはそのデータをコピーしたファイルが提供される場合には、時間を節約するために、そのデータを自動的に取得することをお勧めします。|![configure パートナー組織](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[の構成証明書利用者信頼を手動で作成](../../ad-fs/operations/Create-a-Relying-Party-Trust.md)する<br /><br />![configure パートナー組織](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[の構成フェデレーションメタデータを使用して証明書利用者信頼を作成](../../ad-fs/operations/Create-a-Relying-Party-Trust.md)する|  
|![アカウントパートナー組織の構成](media/icon_checkboxo.gif)|組織のニーズに応じて、AD FS 管理スナップインで指定されている証明書利用者信頼ごとに1つ以上の要求規則セットを作成して、要求が適切に発行されるようにします。|![configure partner org @ no__t の構成-1Checklist リスト:証明書利用者信頼の要求規則の作成](Checklist--Creating-Claim-Rules-for-a-Relying-Party-Trust.md)|  
|![アカウントパートナー組織の構成](media/icon_checkboxo.gif)|要求の説明は、組織のニーズを満たすものが存在しない場合に作成する必要があります。 AD FS には、の AD FS 管理スナップインで公開される要求説明の既定のセットが付属しています。|![configure パートナー組織](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[の要求の説明を追加](../../ad-fs/operations/Add-a-Claim-Description.md)する|  
|![アカウントパートナー組織の構成](media/icon_checkboxo.gif)|組織で id 委任を使用して、指定されたアカウントを "操作" または他のユーザーに対して承認または制限する必要があるかどうかを判断します。 これは、フロント @ no__t-0end Web アプリケーションが back @ no__t-1end Web サービスと対話する必要がある場合に必要となることがよくあります。|@no__t-](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[0Configure 委任を使用する場合は](https://technet.microsoft.com/library/dd807122.aspx)、アカウントパートナー組織の組織を構成します。|  
|![アカウントパートナー組織の構成](media/icon_checkboxo.gif)|フェデレーションのためにクライアントコンピューターを準備する方法:<br /><br />-アカウントパートナーのフェデレーションサーバーの URL を、クライアントブラウザーの信頼済みサイトの一覧に追加します。<br />-グループポリシーを使用して、クライアントコンピューターに適切な Secure Sockets Layer \(SSL @ no__t 証明書をプッシュします。|![configure パートナー組織の組織](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[でクライアントコンピューターを準備](https://technet.microsoft.com/library/dd807114(v=ws.11).aspx)する<br /><br />![configure パートナー組織を構成する](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[アカウントフェデレーションサーバーを信頼するようにクライアントコンピューターを構成](Configure-Client-Computers-to-Trust-the-Account-Federation-Server.md)する<br /><br />@no__t-](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[0configure を使用して、アカウントパートナー組織の証明書をクライアントコンピューターに配布](Distribute-Certificates-to-Client-Computers-by-Using-Group-Policy.md)する| 
