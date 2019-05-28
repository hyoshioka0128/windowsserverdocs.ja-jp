---
ms.assetid: 8c3536b7-d091-4ee6-ad04-24713f070862
title: アカウント パートナー組織での AD FS の展開
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 93f61bc7fd147b2e0220178bcd163b6ca56279cf
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191569"
---
# <a name="deploying-ad-fs-in-the-account-partner-organization"></a>アカウント パートナー組織での AD FS の展開

Active Directory フェデレーション サービスのアカウント パートナー \(AD FS\)サポートされている属性ストアでユーザー アカウントを物理的に格納するフェデレーションの信頼関係内の組織を表します。 ストアがサポートされている属性の詳細については、次を参照してください。 [The Role of Attribute Stores](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md)します。  
  
アカウント パートナー組織のフェデレーション サーバーでは、ローカル ユーザーを認証し、承認決定を行う、リソース パートナーで使用されるセキュリティ トークンを作成します。 Web サイトと Web サービスなどの証明書利用者のパーティが簡単に自身をフェデレーション サーバーに登録し、発行済みトークンの認証とアクセス制御を使用できます。  
  
複数のフェデレーション アプリケーションまたはサービスへのアクセスをユーザーに提供する必要があるシナリオで、各アプリケーションまたはサービスがホストされている場合は別の組織で-デプロイできるように、アカウント パートナーのフェデレーション サーバーを構成することができます複数の証明書利用者のパーティです。  
  
設定して、アカウント パートナー組織を構成する方法の詳細については、次を参照してください。[チェックリスト。アカウント パートナー組織の構成](../../ad-fs/deployment/Checklist--Configuring-the-Account-Partner-Organization.md)します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [アカウント パートナー内のフェデレーション サーバーの役割を確認する](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md)  
  
-   [アカウント パートナー内のフェデレーション サーバー プロキシの役割を確認する](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Account-Partner.md)  
  
-   [アカウント パートナー内のクライアント コンピューターを準備します。](Prepare-Client-Computers-in-the-Account-Partner.md)  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
