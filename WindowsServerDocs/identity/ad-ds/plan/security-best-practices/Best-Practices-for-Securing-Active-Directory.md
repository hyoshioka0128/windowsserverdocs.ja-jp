---
ms.assetid: e2651dc8-4b31-4cd8-a400-3b8123890210
title: "Active Directory をセキュリティで保護するためのベスト プラクティス"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ecef0c173677d379524189b1769d4721ab0774a8
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="best-practices-for-securing-active-directory"></a>Active Directory をセキュリティで保護するためのベスト プラクティス

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このドキュメントでは、専門家の観点を提供し、IT 部門の幹部が企業の Active Directory 環境を保護するための実用的な手法のセットが含まれています。 Active Directory は、IT インフラストラクチャで重要な役割を果たすし、調和とグローバル、相互接続された環境でのさまざまなネットワーク リソースのセキュリティを確保します。 説明する方法については、マイクロソフト IT および Microsoft グローバル 500 お客様の選択した数を表示してだけでなく、その他の Microsoft 事業部の資産を保護する責任を負います Microsoft 情報のセキュリティとリスク管理 (ISRM) 組織のエクスペリエンスは、主に基づいています。  
  
-   [序文](https://technet.microsoft.com/library/dn487451.aspx)  
  
-   [受信確認](https://technet.microsoft.com/library/dn487445.aspx)  
  
-   [概要](../../../ad-ds/manage/component-updates/Executive-Summary.md)  
  
-   [概要](../../../ad-ds/manage/component-updates/Introduction.md)  
  
-   [セキュリティ侵害に至る過程](../../../ad-ds/plan/security-best-practices/Avenues-to-Compromise.md)  
  
-   [資格情報の盗難の魅力的なアカウント](../../../ad-ds/plan/security-best-practices/Attractive-Accounts-for-Credential-Theft.md)  
  
-   [Active Directory の攻撃対象領域を減らす](../../../ad-ds/plan/security-best-practices/Reducing-the-Active-Directory-Attack-Surface.md)  
  
-   [最低限の特権の管理モデルを実装します。](../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md)  
  
-   [セキュリティで保護された管理ホストを実装します。](../../../ad-ds/plan/security-best-practices/Implementing-Secure-Administrative-Hosts.md)  
  
-   [攻撃からドメイン コントローラーをセキュリティで保護します。](../../../ad-ds/plan/security-best-practices/Securing-Domain-Controllers-Against-Attack.md)  
  
-   [監視の Active Directory の侵害の兆候](../../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md)  
  
-   [監査ポリシーの推奨事項](../../../ad-ds/plan/security-best-practices/Audit-Policy-Recommendations.md)  
  
-   [セキュリティ侵害を計画します。](../../../ad-ds/plan/security-best-practices/Planning-for-Compromise.md)  
  
-   [安全な環境を維持します。](../../../ad-ds/plan/security-best-practices/Maintaining-a-More-Secure-Environment.md)  
  
-   [付録](../../../ad-ds/plan/security-best-practices/Appendices.md)  
   
-   [付録 b: 特権アカウントと Active Directory のグループ](../../../ad-ds/plan/security-best-practices/Appendix-B--Privileged-Accounts-and-Groups-in-Active-Directory.md)  
  
-   [付録 c: 保護されたアカウントと Active Directory のグループ](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)  
  
-   [付録 d: Active Directory の組み込み管理者アカウントをセキュリティで保護します。](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)  
  
-   [付録 e: Active Directory の Enterprise Admins グループのセキュリティ保護](../../../ad-ds/plan/security-best-practices/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory.md)  
  
-   [付録 f: Active Directory 内の Domain Admins グループのセキュリティ保護](../../../ad-ds/plan/security-best-practices/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory.md)  
  
-   [付録 g: Active Directory の Administrators グループのセキュリティ保護](../../../ad-ds/plan/security-best-practices/Appendix-G--Securing-Administrators-Groups-in-Active-Directory.md)  
  
-   [付録 h: ローカル管理者アカウントとグループのセキュリティ保護](../../../ad-ds/plan/security-best-practices/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups.md)  
  
-   [付録 i: Active Directory 内の保護されたアカウントとグループ アカウントの管理を作成します。](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md)   
  
-   [付録 l: 監視するイベント](../../../ad-ds/plan/Appendix-L--Events-to-Monitor.md)  
  
-   [付録 m: ドキュメントのリンクと推奨資料](../../../ad-ds/manage/Appendix-M--Document-Links-and-Recommended-Reading.md)  
  


