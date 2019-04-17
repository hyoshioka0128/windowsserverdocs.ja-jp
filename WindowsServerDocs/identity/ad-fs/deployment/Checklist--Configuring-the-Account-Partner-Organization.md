---
ms.assetid: 826974ea-3635-40df-aa37-77dd12a363c8
title: "アカウント パートナー組織の構成のチェックリスト-"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: df8057bf8afb51cbd9ca2ec704144b5863bdf064
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="checklist-configuring-the-account-partner-organization"></a>チェックリスト: アカウント パートナー組織の構成

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

アカウント パートナー組織には、リソース パートナー内の Web ベース アプリケーションにアクセスするユーザーが含まれています。 この組織内の管理者は、AD FS 管理スナップインを使用して、リソース パートナー組織との信頼関係を表す証明書利用者信頼を作成する必要があります。 さらに、リソース パートナーの管理者は、信頼する各アカウント パートナー組織に対して要求プロバイダー信頼を作成する必要があります。  
  
このチェックリストには、アカウント パートナー組織内の Active Directory フェデレーション サービス \(AD FS\) を展開するためのタスクが含まれます。 フェデレーション パートナーシップの特定の半分を確立するために必要なコンポーネントを構成するためのタスクも含まれています。  
  
展開する場合は、[Web SSO 設計](https://technet.microsoft.com/library/dd807033.aspx)、以下のチェックリストをする必要はありません。 ただし、正常に展開するには、このチェックリストのタスクを完了する必要がある、[Federated Web SSO Design](https://technet.microsoft.com/library/dd807050.aspx)します。  
  
> [!IMPORTANT]  
> 管理者は、リソース パートナー組織でのガイダンスに従っていることを確認[チェックリスト: Configuring the Resource Partner Organization](Checklist--Configuring-the-Resource-Partner-Organization.md)を 2 つ目のフェデレーション パートナーシップの半分が正常に作成するすべての必要な展開タスクが完了することを確認します。  
  
> [!NOTE]  
> 順序でこのチェックリストのタスクを完了します。 参照リンクでは、手順には、このトピックに戻りできるように、このチェックリストの残りのタスクを続行することができます、その手順の手順を完了します。  
  
![アカウント パートナー組織の構成](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**チェックリスト: アカウント パートナー組織の構成**  
  
||タスク|リファレンス|  
|-|--------|-------------|  
|![アカウント パートナー組織を構成します。](media/icon_checkboxo.gif)|ある場合、既存の AD FS 1.0 または 1.1 展開、運用環境で現在、新しい AD FS フェデレーション サービスに、現在のフェデレーション サービスから設定を移行する方法については右へのリンクを参照してください。 最初に、組織で AD FS を展開する場合は、AD FS を使用してこの手順をスキップして新しいアカウント パートナー組織をセットアップする方法については、このチェックリストの次の作業を続行します。|![アカウント パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 2.0 への移行の計画](https://technet.microsoft.com/library/ff678044.aspx)|  
|![アカウント パートナー組織を構成します。](media/icon_checkboxo.gif)|展開目標に基づいて、フェデレーション アプリケーションへのアクセス権を持つユーザーに提供するために必要なコンポーネントに関する情報を確認します。|![アカウント パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[提供 Your Active Directory Users Access to Your Claims-aware Applications and Services](https://technet.microsoft.com/library/dd807071.aspx)<br /><br />![アカウント パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Provide Your Active Directory Users Access アプリケーションやサービスの他の組織に](https://technet.microsoft.com/library/dd807123.aspx)<br /><br />![アカウント パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Your Claims-aware Applications and Services を組織のアクセスを別のユーザーの提供](https://technet.microsoft.com/library/dd807099.aspx)|  
|![アカウント パートナー組織を構成します。](media/icon_checkboxo.gif)|どの AD FS 設計このアカウント パートナー組織に関連付けるを決定します。|![アカウント パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Web SSO 設計](https://technet.microsoft.com/library/dd807033.aspx)<br /><br />![アカウント パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション Web SSO 設計](https://technet.microsoft.com/library/dd807050.aspx)|  
|![アカウント パートナー組織を構成します。](media/icon_checkboxo.gif)|AD FS サーバーの展開を開始する前に確認します。1。\) データベース 2 の長所と短所の AD FS 構成を保存する Windows Internal Database \(WID\) または SQL Server を選択します。\) AD FS 展開トポロジの種類とその関連するサーバーの配置とネットワーク レイアウトの推奨事項です。|![アカウント パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 展開トポロジの決定](https://technet.microsoft.com/library/gg982491.aspx)<br /><br />![アカウント パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 展開トポロジに関する考慮事項](https://technet.microsoft.com/library/gg982489.aspx)|  
|![アカウント パートナー組織を構成します。](media/icon_checkboxo.gif)|フェデレーション サーバーとフェデレーション サーバー プロキシ サーバーが、運用環境で使用する必要がありますの適切な数の決定を AD FS 容量計画のガイダンスを確認します。|![アカウント パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS サーバーの容量計画](https://technet.microsoft.com/library/gg749899.aspx)|  
|![アカウント パートナー組織を構成します。](media/icon_checkboxo.gif)|効果的に計画して、アカウント パートナーの展開の物理トポロジを実装する、フェデレーション サーバーまたはフェデレーション サーバー プロキシの 1 つまたは複数の AD FS 設計が必要かどうかを決定します。|![アカウント パートナー組織の構成](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト: フェデレーション サーバーの設定](Checklist--Setting-Up-a-Federation-Server.md)<br /><br />![アカウント パートナー組織の構成](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト:、フェデレーション サーバー プロキシのセットアップの設定](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|  
|![アカウント パートナー組織を構成します。](media/icon_checkboxo.gif)|AD FS に追加する属性ストアの種類を決定します。 次に、AD FS 管理スナップインを使用して、属性ストアを追加します。|![アカウント パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[属性ストアの役割を](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md)<br /><br />![アカウント パートナー組織の構成](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[属性ストアの追加](../../ad-fs/operations/Add-an-Attribute-Store.md)|  
|![アカウント パートナー組織を構成します。](media/icon_checkboxo.gif)|AD FS 1.0 または 1.1 フェデレーション サービスのいずれかを使用しているリソース パートナーからのクレームを消費または AD FS の以前のバージョンと相互運用する AD FS を構成する方法については右へのリンクを参照して要求を送信する必要があります。 場合、 場合も、リソース パートナー組織は、AD FS を使用して、送信または組織に信頼性情報を使用するが、この手順をスキップし、このチェックリストの次の作業を続行できます。|![アカウント パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS と相互運用性の計画 1.x](https://technet.microsoft.com/library/ff678040.aspx)|  
|![アカウント パートナー組織を構成します。](media/icon_checkboxo.gif)|アカウント パートナー組織内の最初のフェデレーション サーバーを展開した後は、AD FS 管理スナップインを使用して証明書利用者のパーティ信頼関係を作成します。 手動で、リソース パートナーに関するデータを入力するか、リソース パートナー組織の管理者に提供するしたフェデレーション メタデータ URL を使用して証明書利用者信頼を作成することができます。 フェデレーション メタデータを使用して、リソース パートナーのデータを自動的に取得することができます。 **注:**時間を節約するために自動的にデータを取得することをお勧め場合は、リソース パートナー フェデレーション メタデータを公開する、またはを使用するためのファイルのコピーを提供することができます。|![アカウント パートナー組織の構成](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[、証明書利用者信頼を手動で作成します。](../../ad-fs/operations/Create-a-Relying-Party-Trust.md)<br /><br />![アカウント パートナー組織の構成](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[、証明書利用者のパーティを使用してフェデレーション メタデータ信頼を作成します。](../../ad-fs/operations/Create-a-Relying-Party-Trust.md)|  
|![アカウント パートナー組織を構成します。](media/icon_checkboxo.gif)|組織のニーズに応じて、各証明書利用者信頼の信頼性情報が適切に発行できるようにの AD FS 管理スナップインで指定されている 1 つまたは複数の要求規則セットを作成します。|![アカウント パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[チェックリスト: Creating Claim Rules for a Relying Party Trust](Checklist--Creating-Claim-Rules-for-a-Relying-Party-Trust.md)|  
|![アカウント パートナー組織を構成します。](media/icon_checkboxo.gif)|既に存在しない場合、要求記述を作成する必要があります、組織のニーズを満たすことができます。 AD FS は、の AD FS 管理スナップインで公開されている要求記述の既定のセットが付属します。|![アカウント パートナー組織の構成](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[要求記述の追加](../../ad-fs/operations/Add-a-Claim-Description.md)|  
|![アカウント パートナー組織を構成します。](media/icon_checkboxo.gif)|組織 ID 委任を使用して、承認または「として機能」またはその他のユーザーを偽装には、指定したアカウントを制限する必要があるかどうかを決定します。 Front\ ツー エンドの Web アプリケーションが back\ ツー エンドの Web サービスとやり取りする必要があるときに多くの場合、要件になります。|![アカウント パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[When to Use Identity Delegation](https://technet.microsoft.com/library/dd807122.aspx)|  
|![アカウント パートナー組織を構成します。](media/icon_checkboxo.gif)|フェデレーションのためには、クライアント コンピューターを準備します。<br /><br />-クライアントのブラウザーの信頼済みサイトの一覧にアカウント パートナーのフェデレーション サーバーの URL を追加します。<br />使用するグループ ポリシーを適切な Secure Sockets Layer \(SSL\) 証明書をクライアント コンピューターにプッシュします。|![アカウント パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[アカウント パートナー内のクライアント コンピューターの準備](https://technet.microsoft.com/library/dd807114(v=ws.11).aspx)<br /><br />![アカウント パートナー組織の構成](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[、アカウント フェデレーション サーバーを信頼するクライアント コンピューターの構成](Configure-Client-Computers-to-Trust-the-Account-Federation-Server.md)<br /><br />![アカウント パートナー組織の構成](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[グループ ポリシーを使用して、クライアント コンピューターに証明書を配布](Distribute-Certificates-to-Client-Computers-by-Using-Group-Policy.md)| 
