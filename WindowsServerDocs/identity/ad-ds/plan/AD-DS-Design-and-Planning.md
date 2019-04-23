---
ms.assetid: a91339ef-6ad4-445f-8ecc-a95fbcc04296
title: Active Directory の設計と計画について
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 24fc96aae268d9847bd3b32460ada33d2c6e0d65
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848693"
---
# <a name="ad-ds-design-and-planning"></a>Active Directory の設計と計画について

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

環境内で Windows Server Active Directory ドメインのサービス (AD DS) を展開することで、シングル サインオン (SSO) 機能を AD DS は、集中管理された、委任された管理モデルの利点を実行できます。 組織の展開タスクと現在の環境を特定した後は、組織のニーズを満たす AD DS の展開戦略を作成できます。  
  
## <a name="about-this-guide"></a>このガイドについて

このガイドでは、組織と作成する特定の設計の要件に基づいて、AD DS の展開戦略を開発するための推奨事項を提供します。 このガイドはためインフラストラクチャ専門家やシステム アーキテクトを使用します。 このガイドを読む前に、機能レベルでの AD DS のしくみをよく理解が必要です。 反映される組織の要件の理解は、AD DS 展開戦略でも必要です。  
  
このガイドでは、一連の Windows Server 2008 AD DS 展開可能な開始点をいくつかのタスクについて説明します。 ガイドでは、環境に最適な展開戦略を決定するのに役立ちます。  
  
テストおよび 100,000 未満のユーザーと 1,000 人未満のサイトに含まれる環境を具体的には検証されてこのガイドで紹介する戦略は、ほぼすべてサーバー オペレーティング システムの展開に適した、最低 28.8 キロ ビット/秒 (Kbps) のネットワーク接続。 お客様の環境がこれらの条件を満たしていない場合より複雑な環境での AD DS 展開エクスペリエンスを使用するコンサルティング会社を使用して検討してください。  
  
AD DS の展開プロセスのテストの詳細については、この記事を参照してください。[のテストと展開プロセスを検証](https://go.microsoft.com/fwlink/?LinkId=100206)です。  
  
## <a name="in-this-guide"></a>このガイドについて

[AD DS の設計を理解します。](Understanding-AD-DS-Design.md)  
  
[AD DS の設計と展開の要件を識別します。](Identifying-Your-AD-DS-Design-and-Deployment-Requirements.md)  
  
[AD DS の展開戦略に要件のマッピング](Mapping-Your-Requirements-to-an-AD-DS-Deployment-Strategy.md)  
  
[Windows Server 2008 AD DS の論理構造の設計](Designing-the-Logical-Structure.md)  
  
[Windows Server 2008 AD DS のサイト トポロジの設計](Designing-the-Site-Topology.md)  
  
[AD DS の高度な機能を有効にします。](Enabling-Advanced-Features-for-AD-DS.md)  
  
[AD DS 展開戦略の例を評価します。](Evaluating-AD-DS-Deployment-Strategy-Examples.md)  
  
[付録 a:重要な AD DS の用語を確認します。](Appendix-A--Reviewing-Key-AD-DS-Terms.md)  
