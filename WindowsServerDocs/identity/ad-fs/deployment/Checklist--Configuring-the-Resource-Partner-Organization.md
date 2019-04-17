---
ms.assetid: 80d50a9f-428e-40fe-b6b3-9837fd9a3efc
title: リソース パートナー組織の構成のチェックリスト-
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 4c73d84a6a32a90f5a5a60f0a0f6e6405ea3b729
ms.sourcegitcommit: f26d2668f57624a3865ca4ffd36a698eea7b503e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2018
---
# <a name="checklist-configuring-the-resource-partner-organization"></a>チェックリスト: リソース パートナー組織の構成

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リソース パートナー組織には、アカウント パートナー内のユーザーがアクセスする Web ベース アプリケーションをホストする Web サーバーが含まれています。 この組織内の管理者は、AD FS 管理スナップインを使用して、アカウント パートナー組織との信頼関係を表すための要求プロバイダー信頼を作成する必要があります。 さらに、アカウント パートナーの管理者は、信頼する各のアカウント パートナー組織の証明書利用者信頼を作成する必要があります。  
  
このチェックリストには、リソース パートナー組織内の Active Directory フェデレーション サービス \(AD FS\) を展開するために必要なタスクが含まれます。 フェデレーション パートナーシップの特定の半分を確立するために必要なコンポーネントを構成するためのタスクも含まれています。  
  
展開する場合は、[Web SSO 設計](https://technet.microsoft.com/library/dd807033.aspx)、以下のチェックリストをする必要はありません。 ただし、正常に展開するには、このチェックリストのタスクを完了する必要がある、[Federated Web SSO Design](https://technet.microsoft.com/library/dd807050.aspx)します。  
  
> [!IMPORTANT]  
> アカウント パートナー組織の管理者のガイダンスに従っていることを確認[チェックリスト: アカウント パートナー組織の構成](Checklist--Configuring-the-Account-Partner-Organization.md)、2 つ目のフェデレーション パートナーシップの半分が正常に作成するすべての必要な展開タスクが完了することを確認するには  
  
> [!NOTE]  
> 順序でこのチェックリストのタスクを完了します。 参照リンクでは、手順には、このトピックに戻りできるように、このチェックリストの残りのタスクを続行することができます、その手順の手順を完了します。  
  
![リソース パートナー組織の構成](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**チェックリスト: リソース パートナー組織の構成**  
  
||タスク|リファレンス|  
|-|--------|-------------|  
|![リソース パートナー組織を構成します。](media/icon_checkboxo.gif)|ある場合、既存の AD FS 1.0 または 1.1 展開、運用環境で現在、新しい AD FS フェデレーション サービスに、現在のフェデレーション サービスから設定を移行する方法については右へのリンクを参照してください。 最初に、組織で AD FS を展開する場合は、AD FS を使用してこの手順をスキップして新しいリソース パートナー組織をセットアップする方法については、このチェックリストの次の作業を続行します。|![リソース パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS への移行の計画](https://technet.microsoft.com/library/ff678044.aspx)|  
|![リソース パートナー組織を構成します。](media/icon_checkboxo.gif)|展開目標に基づいて、フェデレーション アプリケーションへのアクセス権を持つユーザーに提供するために必要なコンポーネントに関する情報を確認します。|![リソース パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[提供 Your Active Directory Users Access to Your Claims-aware Applications and Services](https://technet.microsoft.com/library/dd807071.aspx)<br /><br />![リソース パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Provide Your Active Directory Users Access アプリケーションやサービスの他の組織に](https://technet.microsoft.com/library/dd807123.aspx)<br /><br />![リソース パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Your Claims-aware Applications and Services を組織のアクセスを別のユーザーの提供](https://technet.microsoft.com/library/dd807099.aspx)|  
|![リソース パートナー組織を構成します。](media/icon_checkboxo.gif)|どの AD FS 設計このリソース パートナー組織に関連付けるを決定します。|![リソース パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Web SSO 設計](https://technet.microsoft.com/library/dd807033.aspx)<br /><br />![リソース パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション Web SSO 設計](https://technet.microsoft.com/library/dd807050.aspx)|  
|![リソース パートナー組織を構成します。](media/icon_checkboxo.gif)|別のアプリケーションの種類を確認し、展開するアプリケーションを決定します。|![リソース パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[戦略を決定する、フェデレーション アプリケーション、リソース パートナーに](https://technet.microsoft.com/library/dd807077.aspx)|  
|![リソース パートナー組織を構成します。](media/icon_checkboxo.gif)|AD FS サーバーの展開を開始する前に確認します。1。\) データベース 2 の長所と短所の AD FS 構成を保存する Windows Internal Database \(WID\) または SQL Server を選択します。\) AD FS 展開トポロジの種類とその関連するサーバーの配置とネットワーク レイアウトの推奨事項です。|![リソース パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 展開トポロジの決定](https://technet.microsoft.com/library/gg982491.aspx)<br /><br />![リソース パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 展開トポロジに関する考慮事項](https://technet.microsoft.com/library/gg982489.aspx)|  
|![リソース パートナー組織を構成します。](media/icon_checkboxo.gif)|フェデレーション サーバーとフェデレーション サーバー プロキシ サーバーが、運用環境で使用する必要がありますの適切な数の決定を AD FS 容量計画のガイダンスを確認します。|![リソース パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS サーバーの容量計画](https://technet.microsoft.com/library/gg749899.aspx)|  
|![リソース パートナー組織を構成します。](media/icon_checkboxo.gif)|効果的に計画して、アカウント パートナーの展開の物理トポロジを実装する、フェデレーション サーバーまたはフェデレーション サーバー プロキシの 1 つまたは複数の AD FS 設計が必要かどうかを決定します。|![リソース パートナー組織の構成](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト: フェデレーション サーバーの設定](Checklist--Setting-Up-a-Federation-Server.md)<br /><br />![リソース パートナー組織の構成](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト:、フェデレーション サーバー プロキシのセットアップの設定](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|  
|![リソース パートナー組織を構成します。](media/icon_checkboxo.gif)|AD FS に追加する属性ストアの種類を決定します。 次に、AD FS 管理スナップインを使用して、属性ストアを追加します。|![リソース パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[属性ストアの役割を](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md)<br /><br />![リソース パートナー組織の構成](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[属性ストアの追加](../../ad-fs/operations/Add-an-Attribute-Store.md)|  
|![リソース パートナー組織を構成します。](media/icon_checkboxo.gif)|AD FS 1.0 または 1.1 フェデレーション サービスのいずれかを使用しているアカウント パートナーからのクレームを消費または AD FS の以前のバージョンと相互運用する AD FS を構成する方法については右へのリンクを参照して要求を送信する必要があります。 場合、 場合も、アカウント パートナー組織は、AD FS を使用して、送信または組織に信頼性情報を使用するが、この手順をスキップし、このチェックリストの次の作業を続行できます。|![リソース パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS と相互運用性の計画 1.x](https://technet.microsoft.com/library/ff678040.aspx)|  
|![リソース パートナー組織を構成します。](media/icon_checkboxo.gif)|リソース パートナー組織内の最初のフェデレーション サーバーを展開した後は、AD FS 管理スナップインを使用して要求プロバイダー信頼関係を作成します。 アカウント パートナーを手動でに関するデータを入力するか、アカウント パートナー組織の管理者に提供するしたフェデレーション メタデータ URL を使用して要求プロバイダー信頼を作成することができます。 フェデレーション メタデータを使用して、リソース パートナーのデータを自動的に取得することができます。 **注:**時間を節約するために自動的にデータを取得することをお勧め場合は、アカウント パートナー フェデレーション メタデータを公開する、またはを使用するためのファイルのコピーを提供することができます。|![リソース パートナー組織の構成](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[、証明書利用者信頼を手動で作成します。](../operations/create-a-relying-party-trust.md#to-create-a-claims-aware-relying-party-trust-manually)<br /><br />![リソース パートナー組織の構成](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[、証明書利用者のパーティを使用してフェデレーション メタデータ信頼を作成します。](../operations/create-a-relying-party-trust.md#to-create-a-claims-aware-relying-party-trust-using-federation-metadata)|  
|![リソース パートナー組織を構成します。](media/icon_checkboxo.gif)|によっては、組織のニーズには、変換、またはリソース パートナーに対応する信頼性情報に適切にマップできるように、入力方向の要求が渡される、AD FS 管理スナップインで指定されている各要求プロバイダー信頼の 1 つまたは複数の要求規則セットを作成します。|![リソース パートナー組織の構成](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト: 要求プロバイダー信頼の要求規則を作成します。](Checklist--Creating-Claim-Rules-for-a-Claims-Provider-Trust.md)|  
|![リソース パートナー組織を構成します。](media/icon_checkboxo.gif)|\(Optional\) 要求記述が既に存在していないする場合に作成する必要がありますが、組織のニーズを満たします。 AD FS には、AD FS 管理スナップインで公開されている要求記述の既定のセットが含まれています。|![リソース パートナー組織の構成](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[要求記述の追加](../../ad-fs/operations/Add-a-Claim-Description.md)|  
