---
ms.assetid: 20d48afc-2623-43e9-8ed9-aeb9a0505630
title: "要求規則を構成します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 259e2b266b64a3b34c237cfe209a3558124c8ef2
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="configure-claim-rules"></a>要求規則を構成します。

>適用対象: Windows Server 2016、Windows Server 2012 R2

Claims\ ベースの id モデルでは、Active Directory フェデレーション サービス (AD FS) フェデレーション サービスとしての機能は、信頼性情報のセットを含むトークンを発行します。 要求規則では、AD FS を発行するクレームに関する決定します。 要求規則とすべてのサーバーの構成データは、AD FS 構成データベースに保存されます。  
  
AD FS では信頼性情報の形式で提供される id 情報とその他の情報に基づいて発行決定します。 大まかに言うとルールのプロセッサを 1 つを行って信頼性情報の入力として設定、いくつかの変換を実行し、出力として別の信頼性情報のセットを返しますが AD FS には動作します。 

次のトピックする際は、AD FS を処理する規則を作成します。 
  
-   [パススルーまたは入力方向の要求をフィルター処理する規則を作成します。](../../ad-fs/operations/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim.md)  
  
-   [すべてのユーザーを許可する規則を作成します。](../../ad-fs/operations/Create-a-Rule-to-Permit-All-Users.md)  
  
-   [許可または入力方向の要求に基づいてユーザーを拒否する規則を作成します。](../../ad-fs/operations/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim.md)  
  
-   [LDAP 属性を要求として送信する規則を作成します。](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)  
  
-   [要求として送信グループのメンバーシップの規則を作成します。](../../ad-fs/operations/Create-a-Rule-to-Send-Group-Membership-as-a-Claim.md)  
  
-   [入力方向の要求を変換する規則を作成します。](../../ad-fs/operations/Create-a-Rule-to-Transform-an-Incoming-Claim.md)  
  
-   [認証方法の要求を送信する規則を作成します。](../../ad-fs/operations/Create-a-Rule-to-Send-an-Authentication-Method-Claim.md)  
  
-   [カスタム規則を使用して要求を送信する規則を作成します。](../../ad-fs/operations/Create-a-Rule-to-Send-Claims-Using-a-Custom-rule.md)  

## <a name="see-also"></a>参照してください。  
[AD FS の操作](../../ad-fs/AD-FS-2016-Operations.md) 
