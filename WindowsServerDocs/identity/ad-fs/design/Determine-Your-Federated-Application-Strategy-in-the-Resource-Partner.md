---
ms.assetid: 9eab8c43-a0f2-4d19-a5a4-e1399f0d5f25
title: リソース パートナーでのフェデレーション アプリケーション戦略を決定する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: aca47658cc5a20f63dbd59a26ebe135dd04def92
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59811933"
---
# <a name="determine-your-federated-application-strategy-in-the-resource-partner"></a>リソース パートナーでのフェデレーション アプリケーション戦略を決定する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

新しい Active Directory フェデレーション サービスの設計の重要な部分\(AD FS\)リソース パートナー組織のインフラストラクチャには、アプリケーションとサービスに参加するために使用する完全なセットが決定することが、フェデレーションとどのアカウント パートナーはこれらのリソースの受信者になります。 フェデレーション アプリケーションおよびサービスの戦略を設計する前に、以下の質問について調査します。  
  
-   有効化して、Windows Communication Foundation、ASP.NET アプリケーションまたは展開\(WCF\)のフェデレーション サービスですか?  
  
-   企業ネットワーク上のユーザーが Windows 統合認証を使用してフェデレーション アプリケーションまたはサービスにアクセスする必要がありますか。  
  
-   フェデレーション アプリケーションまたはサービスは境界ネットワークのユーザーによって使用されますか。 使用される場合、Windows 統合認証が必要ですか。  
  
-   すべての Windows Server オペレーティング システムとインターネット インフォメーション サービスを実行するフェデレーション アプリケーションをホストする Web サーバーが\(IIS\)でしょうか。  
  
-   フェデレーション アプリケーションまたはサービスがリソースを提供する対象は誰ですか。  
  
これらの質問に答えること堅実な AD FS 設計を計画する際に役立ちます。 また、コスト効果が高くリソース効率に優れたフェデレーション アプリケーションおよびサービスの作成にも役立ちます。 組織にとって最も適切なフェデレーション アプリケーションおよびサービスを設計する方法の詳細については、このガイドの次のトピックを参照してください。  
  
-   [クレーム対応アプリケーションとサービスに、Active Directory ユーザーのアクセスを提供します。](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
-   [アプリケーションと他の組織のサービスに、Active Directory ユーザーのアクセスを提供します。](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)  
  
-   [クレーム対応アプリケーションとサービスをユーザーに別の組織のアクセスを提供します。](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
詳細については、要求を作成する方法の詳細について\-対応の ASP.NET アプリケーションまたは WCF サービスを参照してください[Windows Identity Foundation SDK](https://go.microsoft.com/fwlink/?LinkId=122266)します。  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)

