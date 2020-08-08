---
ms.assetid: 33b80a3f-67f3-4da7-ac4a-7fd2232fbd5d
title: WID を使用するスタンドアロン フェデレーション サーバー
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 760612e3163e4e862ba9beae94597f2a2356687c
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87972059"
---
# <a name="stand-alone-federation-server-using-wid"></a>WID を使用するスタンドアロン フェデレーション サーバー

スタンド\-Active Directory フェデレーション サービスで単独でフェデレーション サーバー \(AD FS\) Windows Internal Database を使用するように構成するフェデレーション サービスをホストする 1 台のサーバーから成る \(WID\)します。 この AD FS トポロジは、テスト ラボです。 できるだけしないように、運用環境での 1 つだけのフェデレーション サーバーの制限がありより多くのサーバーをスケール アップするために使用できないためです。

テスト ラボに追加のフェデレーション サーバーを追加する場合、このセクションで後で説明した以外のトポロジのいずれかを展開することにより最初からフェデレーション サービスを再構築する必要があります。 テスト ラボや実証には、このトポロジを使用すること勧めそのため、\-の\-1 つのフェデレーション サーバーの適切なもので、次の図に示すように、プライベートのテスト ネットワークで概念環境です。

![WID を使用するサーバー](media/FedServerWID.gif)

## <a name="test-lab-considerations"></a>テスト ラボの考慮事項
このセクションでは、対象となるユーザー、利点、およびテスト ラボ環境でこのトポロジに関連付けられている制限事項についてさまざまな考慮事項について説明します。

### <a name="who-should-use-this-topology"></a>このトポロジを使用する必要がありますか。

-   情報技術 \(IT\) プロフェッショナルまたは評価されるか、このテクノロジの概念実証を開発する IT アーキテクト

### <a name="what-are-the-benefits-of-using-this-topology"></a>このトポロジを使用する利点とは

-   簡単にテスト ラボ環境のセットアップ

### <a name="what-are-the-limitations-of-using-this-topology"></a>このトポロジを使用する場合の制限事項を挙げてください。

-   \(ファームにスケールアップする機能がフェデレーションサービスごとに1つのフェデレーションサーバーのみ\)

-   \(AD FS 構成データベースの1つのインスタンスしか存在しない\)


## <a name="see-also"></a>参照
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
