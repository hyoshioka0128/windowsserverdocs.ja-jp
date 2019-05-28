---
ms.assetid: 826974ea-3635-40df-aa37-77dd12a363c8
title: アカウント パートナー組織の構成のチェックリスト
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 5c01daa86b52f3f175d763d09b4c779affef9681
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192423"
---
# <a name="checklist-configuring-the-account-partner-organization"></a>チェックリスト:アカウント パートナー組織の構成

アカウント パートナー組織には、Web にアクセスするユーザーが含まれています。\-ベースのリソース パートナー アプリケーション。 この組織の管理者は、AD FS 管理スナップインを使用する必要があります\-をリソース パートナー組織の信頼関係を表す証明書利用者信頼を作成するのです。 さらに、リソース パートナー管理者が信頼する各アカウント パートナー組織の要求プロバイダー信頼を作成する必要があります。  
  
このチェックリストには、Active Directory フェデレーション サービスの展開のタスクが含まれています。 \(AD FS\)アカウント パートナー組織。 1 つを確立するために必要なコンポーネントを構成するためのタスクも含まれています。\-フェデレーション パートナーシップの半分です。  
  
展開する場合、 [Web SSO 設計](https://technet.microsoft.com/library/dd807033.aspx)、以下のチェックリストをする必要はありません。 ただし、正常に展開するには、このチェックリストのタスクを完了する必要が行う、[フェデレーション Web SSO 設計](https://technet.microsoft.com/library/dd807050.aspx)します。  
  
> [!IMPORTANT]  
> リソース パートナー組織の管理者のガイダンスに従っていることを確認[チェックリスト。リソース パートナー組織の構成](Checklist--Configuring-the-Resource-Partner-Organization.md)に 2 つ目をフェデレーション パートナーシップの半分が正常に作成するすべての必要な展開タスクを完了することを確認します。  
  
> [!NOTE]  
> このチェックリストのタスクは順番に実行してください。 参照リンクによって手順に移動した場合は、このチェックリストの残りのタスクを進めることができるように、その手順の作業が完了したらこのトピックに戻ります。  
  
![アカウント パートナー組織の構成](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**チェックリスト。アカウント パートナー組織の構成**  
  
||タスク|リファレンス|  
|-|--------|-------------|  
|![アカウント パートナー組織を構成します。](media/icon_checkboxo.gif)|今すぐ既存の AD FS 1.0 または 1.1 デプロイを運用環境である場合は、新しい AD FS フェデレーション サービスに、現在のフェデレーション サービスからの設定を移行する方法については、右へのリンクを参照してください。 最初に、組織で AD FS を展開する AD FS を使用してするは、この手順をスキップし、新しいアカウント パートナー組織を設定する方法については、このチェックリストの次の作業を続行します。|![アカウント パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 2.0 への移行計画](https://technet.microsoft.com/library/ff678044.aspx)|  
|![アカウント パートナー組織を構成します。](media/icon_checkboxo.gif)|展開の目標に基づき、フェデレーション アプリケーションへのアクセスをユーザーに提供するために必要なコンポーネントに関する情報を確認します。|![アカウント パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[提供、Active Directory ユーザーへのアクセス、クレーム対応アプリケーションとサービス](https://technet.microsoft.com/library/dd807071.aspx)<br /><br />![アカウント パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[提供、Active Directory ユーザーへのアクセス、アプリケーションとその他の組織のサービス](https://technet.microsoft.com/library/dd807123.aspx)<br /><br />![アカウント パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[クレーム対応アプリケーションとサービスにアクセスする別の組織のユーザーの提供](https://technet.microsoft.com/library/dd807099.aspx)|  
|![アカウント パートナー組織を構成します。](media/icon_checkboxo.gif)|どの AD FS 設計このアカウント パートナー組織に関連付けるかを決定します。|![アカウント パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Web SSO 設計](https://technet.microsoft.com/library/dd807033.aspx)<br /><br />![アカウント パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[フェデレーション Web SSO 設計](https://technet.microsoft.com/library/dd807050.aspx)|  
|![アカウント パートナー組織を構成します。](media/icon_checkboxo.gif)|AD FS サーバーを展開する前に、次のように確認してください。1.\)か Windows Internal Database を選択することの長所と短所\(WID\)や 2 AD FS 構成データベースを格納する SQL Server。\)AD FS 展開トポロジの種類と関連付けられているサーバーの配置とネットワーク レイアウトの推奨します。|![アカウント パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 展開トポロジの決定](https://technet.microsoft.com/library/gg982491.aspx)<br /><br />![アカウント パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 展開トポロジに関する考慮事項](https://technet.microsoft.com/library/gg982489.aspx)|  
|![アカウント パートナー組織を構成します。](media/icon_checkboxo.gif)|フェデレーション サーバーとフェデレーション サーバー プロキシ サーバーが、運用環境で使用する必要がありますの適切な数を決定する AD FS キャパシティ プランニング ガイダンスを確認します。|![アカウント パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS サーバーの容量を計画します。](https://technet.microsoft.com/library/gg749899.aspx)|  
|![アカウント パートナー組織を構成します。](media/icon_checkboxo.gif)|効果的に計画し、アカウント パートナーの展開の物理トポロジを実装する、1 つ以上のフェデレーション サーバーまたはフェデレーション サーバー プロキシに AD FS 設計が必要かどうかを決定します。|![アカウント パートナー組織の構成](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト。フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)<br /><br />![アカウント パートナー組織の構成](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[チェックリスト。フェデレーション サーバー プロキシのセットアップ](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|  
|![アカウント パートナー組織を構成します。](media/icon_checkboxo.gif)|AD FS に追加する属性ストアの種類を決定します。 AD FS 管理スナップインを使用して、属性ストアを追加し、\-でします。|![アカウント パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[属性ストアの役割を](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md)<br /><br />![アカウント パートナー組織の構成](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[属性ストアの追加](../../ad-fs/operations/Add-an-Attribute-Store.md)|  
|![アカウント パートナー組織を構成します。](media/icon_checkboxo.gif)|場合は、AD FS 1.0 または 1.1 フェデレーション サービスのいずれかを使用しているリソース パートナーからの要求を使用または AD FS の以前のバージョンとの相互運用する AD FS を構成する方法については右へのリンクを参照して要求を送信する必要があります。 場合も、リソース パートナー組織は、AD FS を使用して、送信または組織に要求を使用するが、この手順をスキップし、このチェックリストの次の作業を続行できます。|![アカウント パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS との相互運用の計画 1.x](https://technet.microsoft.com/library/ff678040.aspx)|  
|![アカウント パートナー組織を構成します。](media/icon_checkboxo.gif)|アカウント パートナー組織内の最初のフェデレーション サーバーをデプロイした後は、AD FS 管理スナップインを使用して証明書利用者のパーティの信頼関係を作成\-でします。 証明書利用者信頼を作成するには、リソース パートナーに関するデータを手動で入力するか、リソース パートナーの組織の管理者から入手したフェデレーション メタデータ URL を使用します。 このフェデレーション メタデータを使用して、リソース パートナーに関するデータを自動的に取得することができます。 **注:** リソース パートナーによってフェデレーション メタデータが公開されている場合、またはそのデータをコピーしたファイルが提供される場合には、時間を節約するために、そのデータを自動的に取得することをお勧めします。|![アカウント パートナー組織の構成](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[証明書利用者信頼を手動で作成](../../ad-fs/operations/Create-a-Relying-Party-Trust.md)<br /><br />![アカウント パートナー組織の構成](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[証明書利用者パーティ Trust Using Federation Metadata の作成](../../ad-fs/operations/Create-a-Relying-Party-Trust.md)|  
|![アカウント パートナー組織を構成します。](media/icon_checkboxo.gif)|作成、組織のニーズに応じて 1 つまたは複数の要求規則が指定されている各証明書利用者信頼をパーティの設定で AD FS 管理スナップイン\-で要求が適切に発行されるようにします。|![アカウント パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[チェックリスト。証明書利用者信頼の要求規則の作成](Checklist--Creating-Claim-Rules-for-a-Relying-Party-Trust.md)|  
|![アカウント パートナー組織を構成します。](media/icon_checkboxo.gif)|既に存在しない場合、クレームの説明を作成する必要があります、組織のニーズを満たします。 AD FS が公開されている要求記述の既定のセットが付属しています AD FS 管理スナップインで\-でします。|![アカウント パートナー組織の構成](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[クレームの説明を追加](../../ad-fs/operations/Add-a-Claim-Description.md)|  
|![アカウント パートナー組織を構成します。](media/icon_checkboxo.gif)|組織は id 委任を使用して、承認または「として機能する」または他のユーザーの権限を借用する指定されたアカウントを制限する必要があるかどうかを決定します。 これは、フロントときの要件では多くの場合、\-Web アプリケーションがバックエンドと対話する必要がありますを終了\-Web サービスを終了します。|![アカウント パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Id 委任を使用するタイミング](https://technet.microsoft.com/library/dd807122.aspx)|  
|![アカウント パートナー組織を構成します。](media/icon_checkboxo.gif)|フェデレーション用には、クライアント コンピューターを準備します。<br /><br />-クライアント ブラウザーの信頼済みサイト一覧に、アカウント パートナー フェデレーション サーバーの URL を追加します。<br />-を使用してグループ ポリシーを適切な Secure Sockets Layer をプッシュする\(SSL\)クライアント コンピューターに証明書。|![アカウント パートナー組織の構成](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[アカウント パートナー内のクライアント コンピューターの準備](https://technet.microsoft.com/library/dd807114(v=ws.11).aspx)<br /><br />![アカウント パートナー組織の構成](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[アカウント フェデレーション サーバーを信頼するクライアント コンピューターの構成](Configure-Client-Computers-to-Trust-the-Account-Federation-Server.md)<br /><br />![アカウント パートナー組織の構成](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[グループ ポリシーを使用してクライアント コンピューターに証明書を配布](Distribute-Certificates-to-Client-Computers-by-Using-Group-Policy.md)| 
