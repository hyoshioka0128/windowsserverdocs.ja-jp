---
ms.assetid: e2651dc8-4b31-4cd8-a400-3b8123890210
title: Active Directory のセキュリティ保護に関するベスト プラクティス
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 8935a08b9ab8f99b5f221a14b93974872f11a091
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80821295"
---
# <a name="best-practices-for-securing-active-directory"></a>Active Directory のセキュリティ保護に関するベスト プラクティス

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このドキュメントでは、専門家の視点を提供し、IT 部門の幹部がエンタープライズ Active Directory 環境を保護するために役立つ一連の実用的な手法を紹介します。 Active Directory は IT インフラストラクチャで重要な役割を果たし、相互接続されたグローバル環境におけるさまざまなネットワーク リソースの調和とセキュリティ保護を保証します。 ここで説明する方法は、主に microsoft の情報セキュリティとリスク管理 (ISRM) 組織の経験に基づいています。これは、microsoft グローバル500のお客様を選択したことを通知するだけでなく、Microsoft IT およびその他の Microsoft ビジネス部門の資産を保護する責任があります。  
  
-   [概要](../../../ad-ds/manage/component-updates/Executive-Summary.md)  
  
-   [はじめに](../../../ad-ds/manage/component-updates/Introduction.md)  
  
-   [セキュリティ侵害に至る過程](../../../ad-ds/plan/security-best-practices/Avenues-to-Compromise.md)  
  
-   [資格情報の盗難の対象になりやすいアカウント](../../../ad-ds/plan/security-best-practices/Attractive-Accounts-for-Credential-Theft.md)  
  
-   [Active Directory の攻撃対象領域の削減](../../../ad-ds/plan/security-best-practices/Reducing-the-Active-Directory-Attack-Surface.md)  
  
-   [最小特権の管理モデルの実装](../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md)  
  
-   [セキュリティで保護された管理用のホストを実装する](../../../ad-ds/plan/security-best-practices/Implementing-Secure-Administrative-Hosts.md)  
  
-   [ドメインコントローラーを攻撃から保護する](../../../ad-ds/plan/security-best-practices/Securing-Domain-Controllers-Against-Attack.md)  
  
-   [侵害の兆候の Active Directory を監視する](../../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md)  
  
-   [監査ポリシーの推奨事項](../../../ad-ds/plan/security-best-practices/Audit-Policy-Recommendations.md)  
  
-   [セキュリティ侵害の計画](../../../ad-ds/plan/security-best-practices/Planning-for-Compromise.md)  
  
-   [より安全な環境を維持する](../../../ad-ds/plan/security-best-practices/Maintaining-a-More-Secure-Environment.md)  
  
-   [付録](../../../ad-ds/plan/security-best-practices/Appendices.md)  
   
-   [付録 B: Active Directory の特権アカウントとグループ](../../../ad-ds/plan/security-best-practices/Appendix-B--Privileged-Accounts-and-Groups-in-Active-Directory.md)  
  
-   [付録 C: Active Directory の保護されたアカウントとグループ](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)  
  
-   [付録 D: Active Directory での組み込みの管理者アカウントのセキュリティ保護](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)  
  
-   [付録 E: Active Directory で Enterprise Admins グループをセキュリティ保護する](../../../ad-ds/plan/security-best-practices/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory.md)  
  
-   [付録 F: Active Directory で Domain Admins グループをセキュリティ保護する](../../../ad-ds/plan/security-best-practices/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory.md)  
  
-   [付録 G: Active Directory での管理者グループのセキュリティ保護](../../../ad-ds/plan/security-best-practices/Appendix-G--Securing-Administrators-Groups-in-Active-Directory.md)  
  
-   [付録 H: ローカル管理者アカウントとグループをセキュリティで保護する](../../../ad-ds/plan/security-best-practices/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups.md)  
  
-   [付録 I: Active Directory で保護されたアカウントとグループの管理アカウントを作成する](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md)   
  
-   [付録 L: 監視するイベント](../../../ad-ds/plan/Appendix-L--Events-to-Monitor.md)  
  
-   [付録 M: ドキュメントのリンクと推奨資料](../../../ad-ds/manage/Appendix-M--Document-Links-and-Recommended-Reading.md)  
  


