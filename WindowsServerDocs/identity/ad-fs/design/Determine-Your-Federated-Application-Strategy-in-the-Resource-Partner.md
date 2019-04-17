---
ms.assetid: 9eab8c43-a0f2-4d19-a5a4-e1399f0d5f25
title: "リソース パートナーのフェデレーション アプリケーション戦略を決定します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: aca47658cc5a20f63dbd59a26ebe135dd04def92
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="determine-your-federated-application-strategy-in-the-resource-partner"></a>リソース パートナーのフェデレーション アプリケーション戦略を決定します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リソース パートナー組織内の新しい Active Directory フェデレーション サービス \(AD FS\) インフラストラクチャの設計の重要な部分には、アプリケーションやサービス、フェデレーションに参加に使用され、どのアカウント パートナーとなるリソースの受信者の完全なセットが決定することができます。 フェデレーション アプリケーションおよびサービスの戦略を設計する前に、次の点を考慮します。  
  
-   有効化して展開 ASP.NET アプリケーションまたは Windows Communication Foundation \(WCF\) サービスをフェデレーションしますか。  
  
-   企業ネットワーク上のユーザーでは、フェデレーション アプリケーションまたは Windows 統合認証を通じてサービスへのアクセスが必要ですか。  
  
-   フェデレーション アプリケーションまたはサービスで使用される境界ネットワーク内のユーザーですか。 場合は、Windows 統合認証が必要ですか。  
  
-   そのフェデレーション アプリケーションをホスト、Windows Server オペレーティング システムとインターネット インフォメーション サービス \(IIS\) を実行しているすべての Web サーバーいますか。  
  
-   ユーザーは、フェデレーション アプリケーションまたはサービス リソースを提供するか。  
  
これらの質問に答えることは、単色の AD FS 設計計画に役立ちます。 それもする際はフェデレーション アプリケーションおよびサービスの戦略は、コスト効果の高いとリソースを効率的に作成します。 詳細については、最も適切なフェデレーション アプリケーションおよび組織のサービスの戦略を設計する、このガイドの次のトピックを参照してください。  
  
-   [Active Directory ユーザー アクセスを提供する、クレーム対応アプリケーションとサービス](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
-   [アプリケーションや他の組織のサービスに、Active Directory ユーザーのアクセスを提供します。](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)  
  
-   [要求対応のアプリケーションとサービスをユーザーに他の組織がアクセスを提供します。](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
Claims\ 対応 ASP.NET アプリケーションまたは WCF サービスを作成する方法の詳細については、次を参照してください。[Windows Identity Foundation SDK](https://go.microsoft.com/fwlink/?LinkId=122266)します。  
  
## <a name="see-also"></a>参照してください。
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)

