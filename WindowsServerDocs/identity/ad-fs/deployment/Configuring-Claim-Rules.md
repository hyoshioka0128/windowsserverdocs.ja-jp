---
ms.assetid: 46dce9d4-7293-4b1c-9710-78b04f2e347a
title: "要求規則の構成"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 6494f584edd5f84a5987707953f79edbce15cc02
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="configuring-claim-rules"></a>要求規則の構成

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Claims\ ベースの id モデルでは、フェデレーション サービスとして Active Directory フェデレーション サービス \(AD FS\) の機能は、信頼性情報のセットを含むトークンを発行します。 要求規則では、AD FS を発行する要求のに関して意思決定します。 要求規則とすべてのサーバーの構成データは、AD FS 構成データベースに保存されます。  
  
AD FS では信頼性情報の形式で提供される id 情報とその他の情報に基づいて発行決定します。 大まかに言うとルールのプロセッサを 1 つを行って信頼性情報の入力として設定、いくつかの変換を実行し、出力として別の信頼性情報のセットを返しますが AD FS には動作します。  
  
-   [パススルーまたは入力方向の要求をフィルター処理する規則を作成します。](../../ad-fs/operations/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim.md)  
  
-   [すべてのユーザーを許可する規則を作成します。](../../ad-fs/operations/Create-a-Rule-to-Permit-All-Users.md)  

-   [AD FS 1.x の互換性のある要求を送信する規則を作成します。](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)
  
-   [許可または入力方向の要求に基づいてユーザーを拒否する規則を作成します。](../../ad-fs/operations/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim.md)  
  
-   [LDAP 属性を要求として送信する規則を作成します。](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)  
  
-   [要求として送信グループのメンバーシップの規則を作成します。](../../ad-fs/operations/Create-a-Rule-to-Send-Group-Membership-as-a-Claim.md)  
  
-   [入力方向の要求を変換する規則を作成します。](../../ad-fs/operations/Create-a-Rule-to-Transform-an-Incoming-Claim.md)  
  
-   [認証方法の要求を送信する規則を作成します。](../../ad-fs/operations/Create-a-Rule-to-Send-an-Authentication-Method-Claim.md)  
  
-   [カスタム規則を使用して要求を送信する規則を作成します。](../../ad-fs/operations/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule.md)  

## <a name="additional-references"></a>その他の参照  

[AD FS の操作](../../ad-fs/AD-FS-2016-Operations.md)
