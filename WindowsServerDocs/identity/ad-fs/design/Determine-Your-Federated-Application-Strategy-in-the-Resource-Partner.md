---
ms.assetid: 9eab8c43-a0f2-4d19-a5a4-e1399f0d5f25
title: リソース パートナーでのフェデレーション アプリケーション戦略を決定する
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: b7b50d93ef09259cd6d1893eda4fd5c651b8e688
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853155"
---
# <a name="determine-your-federated-application-strategy-in-the-resource-partner"></a>リソース パートナーでのフェデレーション アプリケーション戦略を決定する

リソースパートナー組織での新しい Active Directory フェデレーションサービス (AD FS) \(AD FS\) インフラストラクチャの設計の重要な部分は、フェデレーションに参加するために使用されるアプリケーションとサービスの完全なセットと、それらのリソースの受信者になるアカウントパートナーを決定することです。 フェデレーション アプリケーションおよびサービスの戦略を設計する前に、以下の質問について調査します。  
  
-   フェデレーション用の WCF\) サービス \(ASP.NET アプリケーションまたは Windows Communication Foundation を有効にしてデプロイしますか?  
  
-   企業ネットワーク上のユーザーが Windows 統合認証を使用してフェデレーション アプリケーションまたはサービスにアクセスする必要がありますか。  
  
-   フェデレーション アプリケーションまたはサービスは境界ネットワークのユーザーによって使用されますか。 使用される場合、Windows 統合認証が必要ですか。  
  
-   フェデレーションアプリケーションをホストするすべての Web サーバーが Windows Server オペレーティングシステムを実行しており、IIS\)をインターネットインフォメーションサービス \(。  
  
-   フェデレーション アプリケーションまたはサービスがリソースを提供する対象は誰ですか。  
  
これらの質問に答えることで、堅固な AD FS 設計を計画するのに役立ちます。 また、コスト効果が高くリソース効率に優れたフェデレーション アプリケーションおよびサービスの作成にも役立ちます。 組織にとって最も適切なフェデレーション アプリケーションおよびサービスを設計する方法の詳細については、このガイドの次のトピックを参照してください。  
  
-   [Active Directory ユーザーに要求に対応するアプリケーションとサービスへのアクセスを提供する](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
-   [Active Directory ユーザーに他の組織のアプリケーションとサービスへのアクセスを提供する](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)  
  
-   [要求に対応するアプリケーションやサービスへのアクセスを別の組織のユーザーに提供する](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
要求\-対応 ASP.NET アプリケーションまたは WCF サービスを作成する方法の詳細については、「 [Windows Identity FOUNDATION SDK](https://go.microsoft.com/fwlink/?LinkId=122266)」を参照してください。  
  
## <a name="see-also"></a>参照
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)

