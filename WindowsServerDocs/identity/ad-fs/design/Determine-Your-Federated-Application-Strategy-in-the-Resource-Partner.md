---
ms.assetid: 9eab8c43-a0f2-4d19-a5a4-e1399f0d5f25
title: リソース パートナーでのフェデレーション アプリケーション戦略を決定する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 0cc7a9202813cd3f8d45a72305d13ad197f5b04d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359163"
---
# <a name="determine-your-federated-application-strategy-in-the-resource-partner"></a>リソース パートナーでのフェデレーション アプリケーション戦略を決定する

リソースパートナー組織の新しい Active Directory フェデレーションサービス (AD FS) @no__t 0AD FS @ no__t インフラストラクチャを設計する際の重要な部分は、フェデレーションに参加するために使用されるアプリケーションとサービスの完全なセットを決定することです。これらのリソースの受信者になるアカウントパートナーを指定します。 フェデレーション アプリケーションおよびサービスの戦略を設計する前に、以下の質問について調査します。  
  
-   フェデレーションに対して ASP.NET アプリケーションまたは Windows Communication Foundation @no__t 0WCF @ no__t サービスを有効にして展開しますか?  
  
-   企業ネットワーク上のユーザーが Windows 統合認証を使用してフェデレーション アプリケーションまたはサービスにアクセスする必要がありますか。  
  
-   フェデレーション アプリケーションまたはサービスは境界ネットワークのユーザーによって使用されますか。 使用される場合、Windows 統合認証が必要ですか。  
  
-   フェデレーションアプリケーションをホストするすべての Web サーバーが Windows Server オペレーティングシステムを実行し、インターネットインフォメーションサービス \(IIS @ no__t?  
  
-   フェデレーション アプリケーションまたはサービスがリソースを提供する対象は誰ですか。  
  
これらの質問に答えることで、堅固な AD FS 設計を計画するのに役立ちます。 また、コスト効果が高くリソース効率に優れたフェデレーション アプリケーションおよびサービスの作成にも役立ちます。 組織にとって最も適切なフェデレーション アプリケーションおよびサービスを設計する方法の詳細については、このガイドの次のトピックを参照してください。  
  
-   [Active Directory ユーザーに要求に対応するアプリケーションとサービスへのアクセスを提供する](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
-   [Active Directory ユーザーに他の組織のアプリケーションとサービスへのアクセスを提供する](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)  
  
-   [要求に対応するアプリケーションやサービスへのアクセスを別の組織のユーザーに提供する](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
要求 @ no__t-0aware ASP.NET アプリケーションまたは WCF サービスを作成する方法の詳細については、「 [Windows Identity FOUNDATION SDK](https://go.microsoft.com/fwlink/?LinkId=122266)」を参照してください。  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)

