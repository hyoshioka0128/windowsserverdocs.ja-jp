---
ms.assetid: 20d48afc-2623-43e9-8ed9-aeb9a0505630
title: 要求規則を構成します。
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e7eedd907c07c2aaef1670c5db3a6892ca3e650d
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189630"
---
# <a name="configure-claim-rules"></a>要求規則を構成する

要求で\-ベースの id モデルでは、Active Directory フェデレーション サービス (AD FS) フェデレーション サービスとしての機能は、一連の要求を含むトークンを発行します。 要求規則は、AD FS が発行する要求に関して意思決定をします。 要求規則およびすべてのサーバーの構成データは、AD FS 構成データベースに格納されます。  
  
AD FS では、要求の形で提供される id 情報とその他のコンテキスト情報に基づく発行決定を行います。 大まかに言えば、AD FS が動作するは、1 つ受け取り、ルール プロセッサは、クレームのセットを入力としてし、さまざまな変換を実行しますし、出力として別のクレーム セットを返します。 

次のトピックの支援で AD FS を処理するルールを作成します。 
  
-   [パススルーまたは入力方向の要求をフィルター処理するルールを作成します。](../../ad-fs/operations/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim.md)  
  
-   [すべてのユーザーを許可する規則を作成する](../../ad-fs/operations/Create-a-Rule-to-Permit-All-Users.md)  
  
-   [入力方向の要求に基づいてユーザーを許可または拒否する規則を作成する](../../ad-fs/operations/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim.md)  
  
-   [要求として LDAP 属性を送信するルールを作成します。](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)  
  
-   [グループ メンバーシップを要求として送信する規則を作成する](../../ad-fs/operations/Create-a-Rule-to-Send-Group-Membership-as-a-Claim.md)  
  
-   [入力方向の要求を変換する規則を作成する](../../ad-fs/operations/Create-a-Rule-to-Transform-an-Incoming-Claim.md)  
  
-   [認証方法の要求を送信する規則を作成する](../../ad-fs/operations/Create-a-Rule-to-Send-an-Authentication-Method-Claim.md)  
  
-   [カスタム規則を使用して要求を送信する規則を作成する](../../ad-fs/operations/Create-a-Rule-to-Send-Claims-Using-a-Custom-rule.md)  

## <a name="see-also"></a>関連項目  
[AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md) 
