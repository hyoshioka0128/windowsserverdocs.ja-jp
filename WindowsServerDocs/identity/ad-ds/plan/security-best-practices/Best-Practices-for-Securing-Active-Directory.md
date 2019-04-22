---
ms.assetid: e2651dc8-4b31-4cd8-a400-3b8123890210
title: Active Directory のセキュリティ保護に関するベスト プラクティス
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 972def668634e794908a3ff2933d038ae38be5d6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817083"
---
# <a name="best-practices-for-securing-active-directory"></a>Active Directory のセキュリティ保護に関するベスト プラクティス

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

このドキュメントは専門家の観点を提供し、IT 部門の幹部が企業の Active Directory 環境を保護するための実用的な手法のセットが含まれています。 Active Directory は IT インフラストラクチャで重要な役割を果たし、相互接続されたグローバル環境におけるさまざまなネットワーク リソースの調和とセキュリティ保護を保証します。 Microsoft の情報セキュリティおよびリスク管理 (ISRM) 組織のエクスペリエンスは、Microsoft IT とだけでなく、他の Microsoft 事業部の資産を保護する責任は、主に説明するメソッドに基づきます、Microsoft グローバル 500 の顧客数の選択。  
  
-   [概要](../../../ad-ds/manage/component-updates/Executive-Summary.md)  
  
-   [はじめに](../../../ad-ds/manage/component-updates/Introduction.md)  
  
-   [セキュリティ侵害に至る過程](../../../ad-ds/plan/security-best-practices/Avenues-to-Compromise.md)  
  
-   [資格情報の盗難の魅力的なアカウント](../../../ad-ds/plan/security-best-practices/Attractive-Accounts-for-Credential-Theft.md)  
  
-   [Active Directory の攻撃対象領域を減らす](../../../ad-ds/plan/security-best-practices/Reducing-the-Active-Directory-Attack-Surface.md)  
  
-   [最低限の特権の管理モデルを実装します。](../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md)  
  
-   [セキュリティで保護された管理ホストを実装します。](../../../ad-ds/plan/security-best-practices/Implementing-Secure-Administrative-Hosts.md)  
  
-   [攻撃に対してドメイン コント ローラーをセキュリティで保護します。](../../../ad-ds/plan/security-best-practices/Securing-Domain-Controllers-Against-Attack.md)  
  
-   [Active Directory のセキュリティ侵害の兆候の監視](../../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md)  
  
-   [監査ポリシーの推奨事項](../../../ad-ds/plan/security-best-practices/Audit-Policy-Recommendations.md)  
  
-   [セキュリティ侵害の計画](../../../ad-ds/plan/security-best-practices/Planning-for-Compromise.md)  
  
-   [安全な環境を維持します。](../../../ad-ds/plan/security-best-practices/Maintaining-a-More-Secure-Environment.md)  
  
-   [付録](../../../ad-ds/plan/security-best-practices/Appendices.md)  
   
-   [付録 b:Active Directory の特権アカウントとグループ](../../../ad-ds/plan/security-best-practices/Appendix-B--Privileged-Accounts-and-Groups-in-Active-Directory.md)  
  
-   [付録 c:保護されたアカウントと Active Directory のグループ](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)  
  
-   [付録 d:Active Directory でビルトイン Administrator アカウントのセキュリティ保護](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)  
  
-   [付録 e:Active Directory の Enterprise Admins グループのセキュリティ保護](../../../ad-ds/plan/security-best-practices/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory.md)  
  
-   [付録 f:Active Directory の Domain Admins グループのセキュリティ保護](../../../ad-ds/plan/security-best-practices/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory.md)  
  
-   [付録 g:Active Directory の管理者グループのセキュリティ保護](../../../ad-ds/plan/security-best-practices/Appendix-G--Securing-Administrators-Groups-in-Active-Directory.md)  
  
-   [付録 h:ローカル管理者アカウントとグループをセキュリティで保護します。](../../../ad-ds/plan/security-best-practices/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups.md)  
  
-   [付録 i:Active Directory 内の保護されたアカウントとグループ アカウントの管理の作成](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md)   
  
-   [付録 l:監視するイベント](../../../ad-ds/plan/Appendix-L--Events-to-Monitor.md)  
  
-   [付録 m:ドキュメントのリンクと推奨資料](../../../ad-ds/manage/Appendix-M--Document-Links-and-Recommended-Reading.md)  
  


