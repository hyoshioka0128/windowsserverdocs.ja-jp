---
ms.assetid: 46dce9d4-7293-4b1c-9710-78b04f2e347a
title: 要求規則の構成
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: e11d507f726323e774bf54f09a390b0c4b68e0a0
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192246"
---
# <a name="configuring-claim-rules"></a>要求規則の構成

要求で\-ベースの id モデル、Active Directory フェデレーション サービスの機能は、 \(AD FS\)クレームのセットを含むトークンを発行するサービスは、フェデレーションとします。 要求規則は、AD FS が発行する要求のに関して意思決定を制御します。 要求規則およびすべてのサーバーの構成データは、AD FS 構成データベースに格納されます。  
  
AD FS では、要求の形で提供される id 情報とその他のコンテキスト情報に基づく発行決定を行います。 大まかに言えば、AD FS が動作するは、1 つ受け取り、ルール プロセッサは、クレームのセットを入力としてし、さまざまな変換を実行しますし、出力として別のクレーム セットを返します。  
  
-   [パススルーまたは入力方向の要求をフィルター処理するルールを作成します。](../../ad-fs/operations/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim.md)  
  
-   [すべてのユーザーを許可する規則を作成する](../../ad-fs/operations/Create-a-Rule-to-Permit-All-Users.md)  

-   [AD FS 1.x の互換性のある要求を送信するルールを作成します。](../../ad-fs/operations/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md)
  
-   [入力方向の要求に基づいてユーザーを許可または拒否する規則を作成する](../../ad-fs/operations/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim.md)  
  
-   [要求として LDAP 属性を送信するルールを作成します。](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)  
  
-   [グループ メンバーシップを要求として送信する規則を作成する](../../ad-fs/operations/Create-a-Rule-to-Send-Group-Membership-as-a-Claim.md)  
  
-   [入力方向の要求を変換する規則を作成する](../../ad-fs/operations/Create-a-Rule-to-Transform-an-Incoming-Claim.md)  
  
-   [認証方法の要求を送信する規則を作成する](../../ad-fs/operations/Create-a-Rule-to-Send-an-Authentication-Method-Claim.md)  
  
-   [カスタム規則を使用して要求を送信する規則を作成する](../../ad-fs/operations/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule.md)  

## <a name="additional-references"></a>その他の参照情報  

[AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md)
