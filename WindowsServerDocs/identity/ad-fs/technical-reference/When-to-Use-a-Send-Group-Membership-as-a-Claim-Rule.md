---
ms.assetid: af16e847-47c2-461e-9df1-cc352a322043
title: "要求規則として送信グループ メンバーシップを使用する場合"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 10e027b4de463aad2b05eae40a622aebf8f12a3b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

# <a name="when-to-use-a-send-group-membership-as-a-claim-rule"></a>要求規則として送信グループ メンバーシップを使用する場合
出力方向の要求に新しい値を指定したアクティブ Directory セキュリティ グループのメンバーであるユーザーのみを発行するときに Active Directory フェデレーション サービス \(AD FS\) でこの規則を使用することができます。 この規則を使用する場合は、指定したグループに対してのみの 1 つの要求を発行して、規則のロジックに一致するように、次の表で説明されています。  
  
|規則のオプション|規則のロジック|  
|---------------|--------------|  
|出力方向の要求の値|ユーザーのグループ メンバーシップと等しい場合、*指定グループ*等しい出力方向の要求の種類と*要求の種類を指定した*、し、既存のグループ名値の置換、*指定した出力方向の要求の値*要求を発行します。|  
  
次のセクションでは、要求規則の概要を提供します。 詳細については、要求規則として、[グループのメンバーシップの送信を使用する場合もあります。  
  
## <a name="about-claim-rules"></a>要求規則について  
要求規則は、入力方向の要求を行う、条件を適用するビジネス ロジックのインスタンスを表します \ (し y\ x の場合)、条件のパラメーターに基づいて出力方向の要求を生成します。 輪郭について知っておくべきヒントの要求規則を読む前に重要な一覧を次にこのトピックの「します。  
  
-   AD FS の管理スナップインには、要求規則でのみ作成できます要求規則テンプレートを使用します。  
  
-   入力方向の要求規則プロセスを要求するか、要求プロバイダーから直接 \ (など、Active Directory または別のフェデレーション \) または受付の出力から、要求プロバイダー信頼規則を変換します。  
  
-   要求規則は、特定の規則セット内で時系列要求発行エンジンによって処理されます。 規則に対する優先順位を設定、さらに調整したり、特定の規則セット内の先行する規則で生成された要求をフィルター処理できます。  
  
-   要求規則テンプレートを使用して、入力方向の要求の種類を指定する必要が常にします。 ただし、1 つの規則を使用して要求の種類が同じで、複数の要求の値を処理することができます。  
  
詳細については、要求規則および要求規則セットを参照してください。[、要求規則の役割](The-Role-of-Claim-Rules.md)します。 規則が処理される方法の詳細については、次を参照してください。[The Role of the Claims Engine](The-Role-of-the-Claims-Engine.md)します。 要求規則セットを処理する方法の詳細については、次を参照してください。[要求パイプラインの役割](The-Role-of-the-Claims-Pipeline.md)します。  
  
## <a name="outgoing-claim-value"></a>出力方向の要求の値  
要求規則テンプレートとして使用し、[グループのメンバーシップの送信、かどうか、ユーザーは、指定したグループのメンバーを条件と要求を発行できます。  
  
つまり、要求したユーザーにグループのセキュリティがある場合にのみ、この規則テンプレートの問題は管理者によって指定された Active Directory グループと一致する \(SID\) ID です。 Active Directory Domain Services \(AD DS\) に対して認証するすべてのユーザーには、入力方向のグループに属する各グループの SID 要求があります。 既定で、Active Directory 要求プロバイダー信頼の受付変換規則は、これらのグループ SID 要求をパススルーします。 これらのグループ Sid 要求発行のベースとしては、AD DS では、ユーザーのグループを検索するよりもはるかに高速を使用します。  
  
このルールでは、1 つの要求のみを使用する場合は、送信、選択した Active Directory グループに基づいてされます。 たとえば、この規則テンプレートを使用して、ユーザーが Domain Admins セキュリティ グループのメンバーである場合、値"Admin"を持つグループの要求を送信する規則を作成することができます。  
  
## <a name="configuring-this-rule-on-a-claims-provider-trust"></a>要求プロバイダー信頼でこの規則の構成  
管理者が使用この規則の種類、要求プロバイダー信頼の受付変換規則グループ Sid がある Active Directory または AD DS を除くすべての要求プロバイダーの非常に一般的な要求プロバイダーから受信している場合にのみです。  
  
## <a name="how-to-create-this-rule"></a>このルールを作成する方法  
要求規則言語のいずれかを使用してこのルールを作成するか、またはを要求として送信 LDAP のグループ メンバーシップを使用して、AD FS の管理スナップインでテンプレートをルールします。 この規則テンプレートは、次の構成オプションを提供します。  
  
-   要求規則名を指定します。  
  
-   オブジェクト ピッカーを使用して、ユーザーのグループを選択します。  
  
-   出力方向の要求の種類を選択します。  
  
-   出力方向の名前 ID 形式を選択 \ (これは利用可能な出力方向の要求の種類 field\ から名前 ID が選択した場合にのみ)  
  
-   出力方向の要求の値を指定します。  
  
このルールを作成する方法の詳細については、次を参照してください。[グループ メンバーシップを要求として送信する規則を作成する](https://technet.microsoft.com/en-us/library/ee913569.aspx)します。  
  
## <a name="using-the-claim-rule-language"></a>要求規則言語を使用します。  
グループ SID 以外の入力方向 SID に基づいて要求を発行する場合は、トランス フォームに入力方向の要求規則テンプレートを使用します。 管理者は、ユーザーのメンバーであるすべてのグループの名前を取得するが場合、LDAP 属性を送信要求規則テンプレートとして代わりに使用と、**tokenGroups**属性です。  
  
### <a name="example-how-to-issue-group-claims-based-on-the-users-group-membership"></a>例: ユーザーのグループ メンバーシップに基づいてグループ要求を発行する方法  
次の規則は、入力方向のグループ SID に基づいて、ユーザーのグループ要求を発行します。  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-21-397933417-626991126-188441444-512", Issuer == "AD AUTHORITY"]  
=> issue(Type = "http://schemas.xmlsoap.org/claims/Group", Value = "administrators", Issuer = c.Issuer, OriginalIssuer = c.OriginalIssuer, ValueType = c.ValueType);  
```  
  
## <a name="additional-references"></a>その他の参照  
[LDAP 属性を要求として送信する規則を作成します。](https://technet.microsoft.com/library/dd807115.aspx)  
  

