---
ms.assetid: 33b80a3f-67f3-4da7-ac4a-7fd2232fbd5d
title: "WID を使用するスタンドアロン フェデレーション サーバー"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 9ec4150a7d3adfaac786219d253e1d0898c18204
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="stand-alone-federation-server-using-wid"></a>WID を使用するスタンドアロン フェデレーション サーバー

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Active Directory フェデレーション サービス \(AD FS\) でスタンドアロンのフェデレーション サーバーは、Windows Internal Database \(WID\) を使用するフェデレーション サービスのホストが構成されている 1 台のサーバーで構成されます。 この AD FS トポロジは、テスト ラボです。 お勧めしません運用環境で、1 つだけのフェデレーション サーバーの制限があり、複数のサーバーに拡張するために使用できないためです。  
  
テスト ラボに別のフェデレーション サーバーを追加する場合は、このセクションで後で説明した以外のトポロジのいずれかを展開することにより最初からフェデレーション サービスを再構築する必要があります。 そのため、1 つのフェデレーション サーバーがで適切なもので、次の図に示すように、プライベートのテスト ネットワークで、テスト ラボや proof\ の概念 of\ 環境のこのトポロジを使用することをお勧めします。  
  
![WID を使用するサーバー](media/FedServerWID.gif)  
  
## <a name="test-lab-considerations"></a>テスト ラボの考慮事項  
このセクションでは、対象となるユーザー、利点、およびテスト ラボ環境でこのトポロジに関連付けられている制限事項についてさまざまな考慮事項について説明します。  
  
### <a name="who-should-use-this-topology"></a>このトポロジを使用している必要がありますか。  
  
-   情報技術 \(IT\) プロフェッショナルまたは評価されるか、このテクノロジの概念実証を開発する IT アーキテクト  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>このトポロジを使用する利点は何ですか。  
  
-   簡単にテスト ラボ環境のセットアップ  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>このトポロジを使用する場合の制限事項とは何ですか。  
  
-   フェデレーション サービスごとに 1 つだけのフェデレーション サーバー \ (、farm\ に拡張する機能がない)  
  
-   重複していない \ (AD FS 構成データベース exists\ の単一インスタンスのみ)  
  

## <a name="see-also"></a>参照してください。
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)
