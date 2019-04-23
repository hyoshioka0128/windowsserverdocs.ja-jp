---
ms.assetid: d590c90e-9adf-4305-b226-eb2a5743337b
title: AD DS の設計とは
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: c94f6ddd19e3178243545b0cc71f6f4c7bb4dbec
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828793"
---
# <a name="understanding-ad-ds-design"></a>AD DS の設計とは

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

組織は、スケーラブルで安全性、および管理しやすいインフラストラクチャを作成するときに、ユーザーおよびリソースの管理を合理化するのに、Windows server Active Directory Domain Services (AD DS) を使用できます。 AD DS を使用して、ブランチ オフィス、Microsoft Exchange Server では、複数のフォレスト環境など、ネットワーク インフラストラクチャを管理することができます。  
  
AD DS の展開プロジェクトは、3 つのフェーズ: 設計フェーズや展開段階で、操作のフェーズ。 設計フェーズでは、デザイン チームは、ディレクトリ サービスを使用する組織内の各部門のニーズに最適な AD DS の論理構造の設計を作成します。 設計が承認されると、展開チームは、ラボ環境で設計をテストし、運用環境で設計を実装します。 展開チームがテストを実行して、デザイン フェーズを潜在的に影響、ため、設計と展開の両方と重複する中間のアクティビティになります。 デプロイが完了したら、運用チームは、ディレクトリ サービスの保守を担当します。  
  
このガイドで説明されている Windows Server AD DS の設計と展開戦略は、広範なラボとパイロット プログラムをテストし、お客様の環境で正常な実装に基づいていますが、AD DS、デザインをカスタマイズする必要があり、特定の複雑な環境に合うように展開します。
  
- AD DS、ブランチ オフィス環境の展開の詳細については、次を参照してください。、[読み取り専用ドメイン コント ローラー (RODC) のブランチ オフィスの計画ガイド](https://go.microsoft.com/fwlink/?LinkId=100207)します。  
- Exchange 環境で AD DS の展開に関する詳細については、記事を参照してください。 [Exchange 2007 の Active Directory の計画](https://go.microsoft.com/fwlink/?LinkId=88904)します。  
- 複数フォレスト環境で AD DS の展開に関する詳細については、記事を参照してください。 [Windows 2000 および Windows Server 2003 での複数のフォレストにに関する考慮事項](https://go.microsoft.com/fwlink/?LinkId=88905)します。  
