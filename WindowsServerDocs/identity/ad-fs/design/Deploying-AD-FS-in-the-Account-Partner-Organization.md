---
ms.assetid: 8c3536b7-d091-4ee6-ad04-24713f070862
title: アカウント パートナー組織での AD FS の展開
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 63c080904482814f9f62451e8e7cfa4862d19927
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359248"
---
# <a name="deploying-ad-fs-in-the-account-partner-organization"></a>アカウント パートナー組織での AD FS の展開

Active Directory フェデレーションサービス (AD FS) \(AD FS\) のアカウントパートナーは、サポートされている属性ストアにユーザーアカウントを物理的に格納するフェデレーションの信頼関係にある組織を表します。 サポートされている属性ストアの詳細については、「[属性ストアの役割](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md)」を参照してください。  
  
アカウントパートナー組織のフェデレーションサーバーは、ローカルユーザーを認証し、リソースパートナーが承認の決定を行うときに使用するセキュリティトークンを作成します。 これにより、Web サイトや Web サービスなどの証明書利用者は、自身をフェデレーションサーバーに簡単に登録し、発行されたトークンを使用して認証とアクセス制御を行うことができます。  
  
複数のフェデレーションアプリケーションまたはサービスへのアクセスをユーザーに提供する必要があるシナリオでは、各アプリケーションまたはサービスが別の組織によってホストされている場合、アカウントパートナーフェデレーションサーバーを構成して、展開できるようにすることができます。複数の証明書利用者。  
  
アカウント パートナー組織のセットアップ方法と構成方法の詳細については、「 [Checklist: Configuring the Account Partner Organization](../../ad-fs/deployment/Checklist--Configuring-the-Account-Partner-Organization.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [アカウント パートナー内のフェデレーション サーバーの役割を確認する](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md)  
  
-   [アカウント パートナー内のフェデレーション サーバー プロキシの役割を確認する](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Account-Partner.md)  
  
-   [アカウントパートナーでクライアントコンピューターを準備する](Prepare-Client-Computers-in-the-Account-Partner.md)  
  
## <a name="see-also"></a>参照
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
