---
ms.assetid: 20d48afc-2623-43e9-8ed9-aeb9a0505630
title: AD FS で要求規則を構成する
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 8f01e78689e687f4ed44653dd3213ab62011359d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87967509"
---
# <a name="configure-claim-rules"></a>要求規則を構成する

要求ベースの \- id モデルでは、フェデレーションサービスとしての Active Directory フェデレーションサービス (AD FS) (AD FS) の機能は、クレームのセットを含むトークンを発行することです。 要求規則は、AD FS 問題が発生したクレームに関する決定を制御します。 要求規則とすべてのサーバー構成データは、AD FS 構成データベースに格納されます。

AD FS は、要求とその他のコンテキスト情報の形式で提供される id 情報に基づいて、発行の決定を行います。 大まかには、AD FS は、1セットの要求を入力として取得し、さまざまな変換を実行して、出力として別のクレームセットを返すことによって、ルールプロセッサとして動作します。

次のトピックは、AD FS が処理するルールを作成する際に役立ちます。

-   [入力方向の要求をパススルーまたはフィルター処理するルールを作成する](../../ad-fs/operations/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim.md)

-   [すべてのユーザーを許可する規則を作成する](../../ad-fs/operations/Create-a-Rule-to-Permit-All-Users.md)

-   [入力方向の要求に基づいてユーザーを許可または拒否する規則を作成する](../../ad-fs/operations/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim.md)

-   [LDAP 属性を要求として送信するルールを作成する](../../ad-fs/operations/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims.md)

-   [グループ メンバーシップを要求として送信する規則を作成する](../../ad-fs/operations/Create-a-Rule-to-Send-Group-Membership-as-a-Claim.md)

-   [入力方向の要求を変換する規則を作成する](../../ad-fs/operations/Create-a-Rule-to-Transform-an-Incoming-Claim.md)

-   [認証方法の要求を送信する規則を作成する](../../ad-fs/operations/Create-a-Rule-to-Send-an-Authentication-Method-Claim.md)

-   [カスタム規則を使用して要求を送信する規則を作成する](../../ad-fs/operations/Create-a-Rule-to-Send-Claims-Using-a-Custom-rule.md)

## <a name="see-also"></a>参照
[AD FS の運用](../ad-fs-operations.md)
