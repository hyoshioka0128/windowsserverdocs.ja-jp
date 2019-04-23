---
ms.assetid: 9cafa3e1-8118-4a75-a7c2-1dbe40b1a444
title: 要求規則を構成します。
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f9e0509e2f870fd0edc7f0c6a241d789945e7ccb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829413"
---
# <a name="configure-claim-rules"></a>要求規則を構成する

>適用先:Windows Server 2016、Windows Server 2012 R2

要求で\-ベースの id モデル、Active Directory フェデレーション サービスの機能は、 \(AD FS\)クレームのセットを含むトークンを発行するサービスは、フェデレーションとします。 要求規則は、AD FS が発行する要求に関して意思決定をします。 要求規則およびすべてのサーバーの構成データは、AD FS 構成データベースに格納されます。  
  
AD FS では、要求の形で提供される id 情報とその他のコンテキスト情報に基づく発行決定を行います。 大まかに言えば、AD FS が動作するは、1 つ受け取り、ルール プロセッサは、クレームのセットを入力としてし、さまざまな変換を実行しますし、出力として別のクレーム セットを返します。 

次のトピックの支援で AD FS を処理するルールを作成します。 
  
-   [パススルーまたは入力方向の要求をフィルター処理するルールを作成します。](Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim.md)  
  
-   [すべてのユーザーを許可する規則を作成します。](Create-a-Rule-to-Permit-All-Users.md)  
  
-   [許可または入力方向の要求に基づいてユーザーを拒否する規則を作成します。](Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim.md)  
  
-   [要求として LDAP 属性を送信するルールを作成します。](Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)  
  
-   [要求として送信グループ メンバーシップの規則を作成します。](Create-a-Rule-to-Send-Group-Membership-as-a-Claim.md)  
  
-   [入力方向の要求を変換する規則を作成します。](Create-a-Rule-to-Transform-an-Incoming-Claim.md)  
  
-   [メソッドの認証要求を送信するルールを作成します。](Create-a-Rule-to-Send-an-Authentication-Method-Claim.md) 
-   [AD FS 1.x の互換性のある要求を送信するルールを作成します。](Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim.md) 
  
-   [カスタム規則を使用して要求を送信するルールを作成します。](Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule.md)  

## <a name="see-also"></a>関連項目  
[AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md) 
