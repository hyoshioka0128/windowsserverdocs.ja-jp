---
ms.assetid: 46dce9d4-7293-4b1c-9710-78b04f2e347a
title: 要求規則の構成
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 9634f4004fbb3354020ce025cd403b15f77b6cbc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359697"
---
# <a name="configuring-claim-rules"></a>要求規則の構成

要求 @ no__t ベースの id モデルでは、フェデレーションサービスとして \(AD FS @ no__t を Active Directory フェデレーションサービス (AD FS) の関数は、一連の要求を含むトークンを発行します。 要求規則は、AD FS 問題が発生したクレームに関する決定を制御します。 要求規則とすべてのサーバー構成データは、AD FS 構成データベースに格納されます。  
  
AD FS は、要求とその他のコンテキスト情報の形式で提供される id 情報に基づいて、発行の決定を行います。 大まかには、AD FS は、1セットの要求を入力として取得し、さまざまな変換を実行して、出力として別のクレームセットを返すことによって、ルールプロセッサとして動作します。  
  
-   [入力方向の要求をパススルーまたはフィルター処理するルールを作成する](../../ad-fs/operations/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim.md)  
  
-   [すべてのユーザーを許可する規則を作成する](../../ad-fs/operations/Create-a-Rule-to-Permit-All-Users.md)  

-   [AD FS 1.x と互換性のある要求を送信するルールを作成する](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)
  
-   [入力方向の要求に基づいてユーザーを許可または拒否する規則を作成する](../../ad-fs/operations/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim.md)  
  
-   [LDAP 属性を要求として送信するルールを作成する](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)  
  
-   [グループ メンバーシップを要求として送信する規則を作成する](../../ad-fs/operations/Create-a-Rule-to-Send-Group-Membership-as-a-Claim.md)  
  
-   [入力方向の要求を変換する規則を作成する](../../ad-fs/operations/Create-a-Rule-to-Transform-an-Incoming-Claim.md)  
  
-   [認証方法の要求を送信する規則を作成する](../../ad-fs/operations/Create-a-Rule-to-Send-an-Authentication-Method-Claim.md)  
  
-   [カスタム規則を使用して要求を送信する規則を作成する](../../ad-fs/operations/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule.md)  

## <a name="additional-references"></a>その他の参照情報  

[AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md)
