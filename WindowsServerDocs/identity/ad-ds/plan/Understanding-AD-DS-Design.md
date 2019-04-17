---
ms.assetid: d590c90e-9adf-4305-b226-eb2a5743337b
title: "AD DS の設計を理解します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 09afe3d19add87327d05bfafba6e0492a278b968
ms.sourcegitcommit: 1c3e6375b2e8eb01cfd299d0e9478fee46905c99
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2018
---
# <a name="understanding-ad-ds-design"></a>AD DS の設計を理解します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

組織は、スケーラブルで安全であり、および管理しやすいインフラストラクチャの作成中にユーザーとリソースの管理を簡略化するために、Windows Server の Active Directory ドメイン サービス (AD DS) を使用できます。 AD DS を使用して、ブランチ オフィス、Microsoft Exchange Server では、複数フォレスト環境など、ネットワーク インフラストラクチャを管理することができます。  
  
AD DS 展開プロジェクトは、3 つのフェーズ。設計段階や展開段階で、運用フェーズします。 設計フェーズでは、設計チームは、ディレクトリ サービスを使用する組織内の各部署のニーズに合わせて、AD DS 論理構造の設計を作成します。 設計が承認されると、展開チームは、ラボ環境での設計をテストし、実稼働環境での設計を実装します。 展開チームによるテストを実行し、可能性のあるに影響を与える設計段階、ためには、暫定的な活動の設計と展開の両方が重なっていることを勧めします。 展開が完了したら、運用チームは、ディレクトリ サービスの管理を担当します。  
  
このガイドで説明されている Windows Server AD DS の設計と展開戦略は、広範なラボとパイロット プログラムのテスト、およびお客様の環境に実装の成功に基づいていますが、AD DS の設計をカスタマイズする必要があります、特定の複雑な環境に合わせて展開します。  
  
-   ブランチ オフィス環境に AD DS の展開に関する詳細については、次を参照してください。、Read-Only ドメイン コントローラー (RODC) ブランチ オフィスの計画ガイド ([https://go.microsoft.com/fwlink/?LinkId=100207](https://go.microsoft.com/fwlink/?LinkId=100207))。  
  
-   Exchange 環境に AD DS の展開に関する詳細についてを参照してください Exchange 2007 の Active Directory の計画 ([https://go.microsoft.com/fwlink/?LinkId=88904](https://go.microsoft.com/fwlink/?LinkId=88904))。  
  
-   複数フォレスト環境で AD DS の展開に関する詳細については、Windows 2000 および Windows Server 2003 での複数のフォレストにに関する考慮事項を参照してください ([https://go.microsoft.com/fwlink/?LinkId=88905](https://go.microsoft.com/fwlink/?LinkId=88905))。  
  


