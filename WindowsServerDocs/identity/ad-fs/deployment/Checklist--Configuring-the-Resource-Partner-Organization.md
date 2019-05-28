---
ms.assetid: 80d50a9f-428e-40fe-b6b3-9837fd9a3efc
title: リソース パートナー組織の構成のチェックリスト
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 41902de1253654eb3eac6176d6e8b7c50dc39663
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192402"
---
# <a name="checklist-configuring-the-resource-partner-organization"></a>チェックリスト:リソース パートナー組織の構成

リソース パートナー組織には、Web をホストする Web サーバーが含まれています。\-ベースのアカウント パートナー内のユーザーがアクセスするアプリケーション。 この組織の管理者は、AD FS 管理スナップインを使用する必要があります\-をアカウント パートナー組織の信頼関係を表す要求プロバイダー信頼を作成するのです。 さらに、アカウント パートナーの管理者は、信頼にする各アカウント パートナー組織の証明書利用者信頼を作成する必要があります。  
  
このチェックリストには、Active Directory フェデレーション サービスを展開するために必要なタスクが含まれた\(AD FS\)リソース パートナー組織にします。 1 つを確立するために必要なコンポーネントを構成するためのタスクも含まれています。\-フェデレーション パートナーシップの半分です。  
  
展開する場合、 [Web SSO 設計](https://technet.microsoft.com/library/dd807033.aspx)、以下のチェックリストをする必要はありません。 ただし、正常に展開するには、このチェックリストのタスクを完了する必要が行う、[フェデレーション Web SSO 設計](https://technet.microsoft.com/library/dd807050.aspx)します。  
  
> [!IMPORTANT]  
> アカウント パートナー組織の管理者のガイダンスに従っていることを確認[チェックリスト。アカウント パートナー組織の構成](Checklist--Configuring-the-Account-Partner-Organization.md)2 つ目をフェデレーション パートナーシップの半分が正常に作成するすべての必要な展開タスクが完了することを確認するには  
  
> [!NOTE]  
> このチェックリストのタスクは順番に実行してください。 参照リンクによって手順に移動した場合は、このチェックリストの残りのタスクを進めることができるように、その手順の作業が完了したらこのトピックに戻ります。  
  
![リソース パートナー組織の構成](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**チェックリスト。リソース パートナー組織の構成**  
  
||タスク|リファレンス|  
|-|--------|-------------|  
|![リソース パートナー組織を構成します。](media/icon_checkboxo.gif)|今すぐ既存の AD FS 1.0 または 1.1 デプロイを運用環境である場合は、新しい AD FS フェデレーション サービスに、現在のフェデレーション サービスからの設定を移行する方法については、右へのリンクを参照してください。 最初に、組織で AD FS を展開する AD FS を使用してするは、この手順を省略して、新しいリソース パートナー組織を設定する方法については、このチェックリストの次の作業を続行します。|![リソース パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS への移行計画](https://technet.microsoft.com/library/ff678044.aspx)|  
|![リソース パートナー組織を構成します。](media/icon_checkboxo.gif)|展開の目標に基づき、フェデレーション アプリケーションへのアクセスをユーザーに提供するために必要なコンポーネントに関する情報を確認します。|![リソース パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[提供、Active Directory ユーザーへのアクセス、クレーム対応アプリケーションとサービス](https://technet.microsoft.com/library/dd807071.aspx)<br /><br />![リソース パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[提供、Active Directory ユーザーへのアクセス、アプリケーションとその他の組織のサービス](https://technet.microsoft.com/library/dd807123.aspx)<br /><br />![リソース パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[クレーム対応アプリケーションとサービスにアクセスする別の組織のユーザーの提供](https://technet.microsoft.com/library/dd807099.aspx)|  
|![リソース パートナー組織を構成します。](media/icon_checkboxo.gif)|どの AD FS 設計このリソース パートナー組織に関連付けるかを決定します。|![リソース パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Web SSO 設計](https://technet.microsoft.com/library/dd807033.aspx)<br /><br />![リソース パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション Web SSO 設計](https://technet.microsoft.com/library/dd807050.aspx)|  
|![リソース パートナー組織を構成します。](media/icon_checkboxo.gif)|別のアプリケーションの種類を確認し、展開するには、どのアプリケーションを決定します。|![リソース パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[確認、フェデレーション アプリケーション戦略、リソース パートナー内](https://technet.microsoft.com/library/dd807077.aspx)|  
|![リソース パートナー組織を構成します。](media/icon_checkboxo.gif)|AD FS サーバーを展開する前に、次のように確認してください。1.\)か Windows Internal Database を選択することの長所と短所\(WID\)や 2 AD FS 構成データベースを格納する SQL Server。\)AD FS 展開トポロジの種類と関連付けられているサーバーの配置とネットワーク レイアウトの推奨します。|![リソース パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 展開トポロジの決定](https://technet.microsoft.com/library/gg982491.aspx)<br /><br />![リソース パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 展開トポロジに関する考慮事項](https://technet.microsoft.com/library/gg982489.aspx)|  
|![リソース パートナー組織を構成します。](media/icon_checkboxo.gif)|フェデレーション サーバーとフェデレーション サーバー プロキシ サーバーが、運用環境で使用する必要がありますの適切な数を決定する AD FS キャパシティ プランニング ガイダンスを確認します。|![リソース パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS サーバーの容量を計画します。](https://technet.microsoft.com/library/gg749899.aspx)|  
|![リソース パートナー組織を構成します。](media/icon_checkboxo.gif)|効果的に計画し、アカウント パートナーの展開の物理トポロジを実装する、1 つ以上のフェデレーション サーバーまたはフェデレーション サーバー プロキシに AD FS 設計が必要かどうかを決定します。|![リソース パートナー組織の構成](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト。フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)<br /><br />![リソース パートナー組織の構成](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト。フェデレーション サーバー プロキシのセットアップ](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|  
|![リソース パートナー組織を構成します。](media/icon_checkboxo.gif)|AD FS に追加する属性ストアの種類を決定します。 AD FS 管理スナップインを使用して、属性ストアを追加し、\-でします。|![リソース パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[属性ストアの役割を](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md)<br /><br />![リソース パートナー組織の構成](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[属性ストアの追加](../../ad-fs/operations/Add-an-Attribute-Store.md)|  
|![リソース パートナー組織を構成します。](media/icon_checkboxo.gif)|場合は、AD FS 1.0 または 1.1 フェデレーション サービスのいずれかを使用しているアカウント パートナーからの要求を使用または AD FS の以前のバージョンとの相互運用する AD FS を構成する方法については右へのリンクを参照して要求を送信する必要があります。 場合も、アカウント パートナー組織は、AD FS を使用して、送信または組織に要求を使用するが、この手順をスキップし、このチェックリストの次の作業を続行できます。|![リソース パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS との相互運用の計画 1.x](https://technet.microsoft.com/library/ff678040.aspx)|  
|![リソース パートナー組織を構成します。](media/icon_checkboxo.gif)|リソース パートナー組織内の最初のフェデレーション サーバーをデプロイした後は、AD FS 管理スナップインを使用して要求プロバイダー信頼関係を作成\-でします。 アカウント パートナーを手動でのデータを入力するか、アカウント パートナー組織の管理者に提供するフェデレーション メタデータ URL を使用して、要求プロバイダー信頼を作成できます。 このフェデレーション メタデータを使用して、リソース パートナーに関するデータを自動的に取得することができます。 **注:** アカウント パートナーは、そのフェデレーション メタデータを公開または使用するためのファイルのコピーを提供することができます、時間を節約するために自動的にデータを取得することをお勧めします。|![リソース パートナー組織の構成](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[証明書利用者信頼を手動で作成](../operations/create-a-relying-party-trust.md#to-create-a-claims-aware-relying-party-trust-manually)<br /><br />![リソース パートナー組織の構成](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[証明書利用者パーティ Trust Using Federation Metadata の作成](../operations/create-a-relying-party-trust.md#to-create-a-claims-aware-relying-party-trust-using-federation-metadata)|  
|![リソース パートナー組織を構成します。](media/icon_checkboxo.gif)|組織のニーズに応じて作成するか、またはそれぞれの要求プロバイダー信頼が指定されている複数の要求規則を設定、AD FS 管理スナップインで\-でを通じて渡される入力方向の要求が、ように変換、または適切にマップされています。リソース パートナー内の対応する要求。|![リソース パートナー組織の構成](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト。要求プロバイダー信頼の要求規則の作成](Checklist--Creating-Claim-Rules-for-a-Claims-Provider-Trust.md)|  
|![リソース パートナー組織を構成します。](media/icon_checkboxo.gif)|\(省略可能な\)するクレームの説明は、1 つは存在しない場合を作成する必要がありますが、組織のニーズを満たします。 AD FS には、公開されている要求記述の既定のセットが含まれています。 AD FS 管理スナップインで\-でします。|![リソース パートナー組織の構成](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[クレームの説明を追加](../../ad-fs/operations/Add-a-Claim-Description.md)|  
