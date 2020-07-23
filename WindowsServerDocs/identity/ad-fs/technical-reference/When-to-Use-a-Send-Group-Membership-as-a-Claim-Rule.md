---
ms.assetid: af16e847-47c2-461e-9df1-cc352a322043
title: "\"グループ メンバーシップを要求として送信する\" 規則を使用するタイミング"
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 43d9e8767c0a179a23d015484b09a0228829870b
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966484"
---
# <a name="when-to-use-a-send-group-membership-as-a-claim-rule"></a>"グループ メンバーシップを要求として送信する" 規則を使用するタイミング
この規則は、 \( \) 指定された Active Directory セキュリティグループのメンバーであるユーザーのみに対して、新しい出力方向の要求の値を発行する場合に Active Directory フェデレーションサービス (AD FS) AD FS で使用できます。 この規則を使用すると、次の表で説明するように、指定されたグループの中で、規則のロジックと一致するグループに対してのみ、1 つの要求が発行されます。  
  
|規則のオプション|規則のロジック|  
|---------------|--------------|  
|出力方向の要求の値|ユーザーのグループメンバーシップが*指定されたグループ*と同じであり、出力方向の要求の種類が*指定された要求の種類*と等しい場合は、既存のグループ名の値を*指定された出力方向の要求の値*に置き換えて、要求を発行します。|  
  
以下のセクションでは、要求規則の基本的な概要を説明します。 "グループ メンバーシップの送信を要求として送信する" 規則を使用するタイミングについても詳しく説明します。  
  
## <a name="about-claim-rules"></a>要求規則について  
要求規則は、入力方向の要求を受け取り、x が y の場合に条件を適用して、 \( \) 条件パラメーターに基づいて出力方向の要求を生成するビジネスロジックのインスタンスを表します。 次の一覧に、このトピックを読む前に理解しておく必要のある、要求規則に関する重要なヒントを示します。  
  
-   AD FS 管理スナップインでは \- 、要求規則テンプレートを使用してのみ要求規則を作成できます。  
  
-   要求規則は、フェデレーションサービス Active Directory などの要求プロバイダーから直接、 \( \) または要求プロバイダー信頼の受け入れ変換規則の出力から、入力方向の要求を処理します。  
  
-   要求規則は、要求発行エンジンによって、特定の規則セット内で時系列に従って処理されます。 規則に優先順位を設定すると、特定の規則セット内の先行する規則で生成された要求をさらに調整またはフィルター処理できます。  
  
-   要求規則テンプレートでは、常に入力方向の要求の種類を指定する必要があります。 ただし、1 つの規則を使用して、要求の種類が同じ複数の要求の値を処理できます。  
  
要求規則と要求規則セットの詳細については、「[要求規則の役割](The-Role-of-Claim-Rules.md)」を参照してください。 規則の処理方法の詳細については、「[要求エンジンの役割](The-Role-of-the-Claims-Engine.md)」を参照してください。 要求規則セットの処理方法の詳細については、「[要求パイプラインの役割](The-Role-of-the-Claims-Pipeline.md)」を参照してください。  
  
## <a name="outgoing-claim-value"></a>出力方向の要求の値  
"グループ メンバーシップを要求として送信する" 規則テンプレートを使用して、ユーザーが指定されたグループのメンバーであるかどうかを条件とする要求を発行できます。  
  
言い換えると、この規則テンプレートでは、 \( \) 管理者が指定した Active Directory グループに一致するグループセキュリティ ID SID がユーザーに与えられている場合にのみ、要求が発行されます。 Active Directory Domain Services AD DS に対して認証を行うすべてのユーザーに \( \) は、属している各グループの入力方向のグループ SID 要求が含まれます。 既定では、Active Directory 要求プロバイダー信頼の受付変換規則は、これらの SID 要求を通過させます。 これらのグループ Sid を要求を発行するための基礎として使用することは、AD DS でユーザーのグループを検索するよりもはるかに高速です。  
  
この規則を使用すると、選択された Active Directory グループに基づいて、要求が 1 つだけ送信されます。 たとえば、この規則テンプレートを使用して、ユーザーが Domain Admins セキュリティ グループのメンバーであれば値 "Admin" を持つグループの要求を送信する規則を作成できます。  
  
## <a name="configuring-this-rule-on-a-claims-provider-trust"></a>要求プロバイダー信頼でのこの規則の構成  
管理者は、この規則の種類を、グループ SID が要求プロバイダーから受信される場合のみ、要求プロバイダー信頼の受付変換規則の中で使用する必要があります。これは、Active Directory または AD DS 以外の要求プロバイダーでは非常に珍しいことです。  
  
## <a name="how-to-create-this-rule"></a>この規則の作成方法  
この規則を作成するには、要求規則言語を使用するか、AD FS 管理スナップインで [LDAP グループメンバーシップを要求として送信] 規則テンプレートを使用し \- ます。 この規則テンプレートには、次の構成オプションがあります。  
  
-   要求規則名を指定する  
  
-   オブジェクトピッカーを使用してユーザーのグループを選択する  
  
-   出力方向の要求の種類を選択する  
  
-   [出力 \( 方向の要求の種類] フィールドで [名前 id] が選択されている場合にのみ使用できる送信名 id 形式を選択します。\)  
  
-   出力方向の要求の値を指定する  
  
このルールを作成する方法の詳細については、「[グループメンバーシップを要求として送信するルールを作成](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ee913569(v=ws.11))する」を参照してください。  
  
## <a name="using-the-claim-rule-language"></a>要求規則言語の使用  
グループ SID 以外の入力方向の SID に基づいて要求を発行する場合は、"入力方向の要求の変換" 規則テンプレートを使用します。 ユーザーがメンバーとして属しているすべてのグループの名前を管理者が取得する場合は、"LDAP 属性を要求として送信する" 規則テンプレートと **tokenGroups** 属性を使用します。  
  
### <a name="example-how-to-issue-group-claims-based-on-the-users-group-membership"></a>例: ユーザーのグループメンバーシップに基づいてグループ要求を発行する方法  
次の規則は、入力方向のグループ SID に基づいて、ユーザーのグループ要求を発行します。  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-21-397933417-626991126-188441444-512", Issuer == "AD AUTHORITY"]  
=> issue(Type = "http://schemas.xmlsoap.org/claims/Group", Value = "administrators", Issuer = c.Issuer, OriginalIssuer = c.OriginalIssuer, ValueType = c.ValueType);  
```  
  
## <a name="additional-references"></a>その他のリファレンス  
[LDAP 属性を要求として送信するルールを作成する](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807115(v=ws.11))  
  
