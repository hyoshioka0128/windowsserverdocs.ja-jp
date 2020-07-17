---
ms.assetid: 33b80a3f-67f3-4da7-ac4a-7fd2232fbd5d
title: WID を使用するスタンドアロン フェデレーション サーバー
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 7253691cff4cc83032e4a345682ca1e43bafddc4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858775"
---
# <a name="stand-alone-federation-server-using-wid"></a>WID を使用するスタンドアロン フェデレーション サーバー

Active Directory フェデレーションサービス (AD FS) \(AD FS\) のスタンド\-アロンフェデレーションサーバーは、Windows Internal Database フェデレーションサービス WID \(を使用するように構成された\)をホストする1台のサーバーで構成されています。 この AD FS トポロジは、テスト ラボです。 できるだけしないように、運用環境での 1 つだけのフェデレーション サーバーの制限がありより多くのサーバーをスケール アップするために使用できないためです。  
  
テスト ラボに追加のフェデレーション サーバーを追加する場合、このセクションで後で説明した以外のトポロジのいずれかを展開することにより最初からフェデレーション サービスを再構築する必要があります。 テスト ラボや実証には、このトポロジを使用すること勧めそのため、\-の\-1 つのフェデレーション サーバーの適切なもので、次の図に示すように、プライベートのテスト ネットワークで概念環境です。  
  
![WID を使用するサーバー](media/FedServerWID.gif)  
  
## <a name="test-lab-considerations"></a>テスト ラボの考慮事項  
このセクションでは、対象となるユーザー、利点、およびテスト ラボ環境でこのトポロジに関連付けられている制限事項についてさまざまな考慮事項について説明します。  
  
### <a name="who-should-use-this-topology"></a>このトポロジを使用する必要がありますか。  
  
-   情報技術 \(IT\) プロフェッショナルまたは評価されるか、このテクノロジの概念実証を開発する IT アーキテクト  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>このトポロジを使用する利点とは  
  
-   簡単にテスト ラボ環境のセットアップ  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>このトポロジを使用する場合の制限事項を挙げてください。  
  
-   ファームにスケールアップする機能を \(フェデレーションサービスごとに1つのフェデレーションサーバーのみ\)  
  
-   冗長ではありません \(AD FS 構成データベースの1つのインスタンスのみが存在\)  
  

## <a name="see-also"></a>参照
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
