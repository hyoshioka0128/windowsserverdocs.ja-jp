---
ms.assetid: af16e847-47c2-461e-9df1-cc352a322043
title: "\"グループ メンバーシップを要求として送信する\" 規則を使用するタイミング"
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: ea537aa61cd7bfbe05ed1dd151eddd4a0bfc5ca7
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188302"
---
# <a name="when-to-use-a-send-group-membership-as-a-claim-rule"></a>"グループ メンバーシップを要求として送信する" 規則を使用するタイミング
この規則を使用するには Active Directory フェデレーション サービスで\(AD FS\)指定された Active Directory セキュリティ グループのメンバーであるユーザーのみを対象の新しい出力方向の要求値を発行する場合。 この規則を使用すると、次の表で説明するように、指定されたグループの中で、規則のロジックと一致するグループに対してのみ、1 つの要求が発行されます。  
  
|規則のオプション|規則のロジック|  
|---------------|--------------|  
|出力方向の要求の値|ユーザーのグループ メンバーシップが*指定したグループ*と一致し、出力方向の要求の種類が*指定した出力方向の要求*と一致する場合は、既存のグループ名の値を*指定した出力方向の要求の値*に置き換えて要求を発行します。|  
  
以下のセクションでは、要求規則の基本的な概要を説明します。 "グループ メンバーシップの送信を要求として送信する" 規則を使用するタイミングについても詳しく説明します。  
  
## <a name="about-claim-rules"></a>要求規則について  
要求規則が入力方向の要求を実行を条件を適用するビジネス ロジックのインスタンスを表します\(x、y if\)条件パラメーターに基づいて出力方向の要求を生成します。 次の一覧に、このトピックを読む前に理解しておく必要のある、要求規則に関する重要なヒントを示します。  
  
-   AD FS 管理スナップインで\-要求規則テンプレートを使用してルールを作成することができますのみを要求  
  
-   要求規則プロセスが受信要求の要求プロバイダーから直接、 \(Active Directory または別のフェデレーション サービスなど\)または変換要求プロバイダー信頼規則、受け入れの出力から。  
  
-   要求規則は、要求発行エンジンによって、特定の規則セット内で時系列に従って処理されます。 規則に優先順位を設定すると、特定の規則セット内の先行する規則で生成された要求をさらに調整またはフィルター処理できます。  
  
-   要求規則テンプレートでは、常に入力方向の要求の種類を指定する必要があります。 ただし、1 つの規則を使用して、要求の種類が同じ複数の要求の値を処理できます。  
  
詳細については、要求規則および要求規則セットについてを参照してください。 [、要求規則の役割](The-Role-of-Claim-Rules.md)します。 ルールの処理方法の詳細については、次を参照してください。[要求エンジンの役割](The-Role-of-the-Claims-Engine.md)します。 要求規則セットを処理する方法の詳細については、次を参照してください。[要求パイプラインの役割](The-Role-of-the-Claims-Pipeline.md)します。  
  
## <a name="outgoing-claim-value"></a>出力方向の要求の値  
"グループ メンバーシップを要求として送信する" 規則テンプレートを使用して、ユーザーが指定されたグループのメンバーであるかどうかを条件とする要求を発行できます。  
  
つまり、この規則テンプレートは要求を発行のユーザーがグループのセキュリティ ID がある場合のみ\(SID\)管理者が指定した Active Directory グループに一致します。 Active Directory ドメイン サービスに対して認証するすべてのユーザー \(AD DS\)入力方向のグループ SID 要求を各グループに属していることになります。 既定では、Active Directory 要求プロバイダー信頼の受付変換規則は、これらの SID 要求を通過させます。 これらのグループ SID を要求発行のベースにするほうが、AD DS でユーザーのグループを調べるよりもはるかに高速です。  
  
この規則を使用すると、選択された Active Directory グループに基づいて、要求が 1 つだけ送信されます。 たとえば、この規則テンプレートを使用して、ユーザーが Domain Admins セキュリティ グループのメンバーであれば値 "Admin" を持つグループの要求を送信する規則を作成できます。  
  
## <a name="configuring-this-rule-on-a-claims-provider-trust"></a>要求プロバイダー信頼でのこの規則の構成  
管理者は、この規則の種類を、グループ SID が要求プロバイダーから受信される場合のみ、要求プロバイダー信頼の受付変換規則の中で使用する必要があります。これは、Active Directory または AD DS 以外の要求プロバイダーでは非常に珍しいことです。  
  
## <a name="how-to-create-this-rule"></a>この規則の作成方法  
要求規則言語のいずれかを使用しているルールを作成するか、AD FS 管理での要求規則テンプレートとして送信する LDAP グループ メンバーシップを使用してスナップ\-でします。 この規則テンプレートには、次の構成オプションがあります。  
  
-   要求規則名を指定する  
  
-   オブジェクト ピッカーを使用して、ユーザーのグループを選択する  
  
-   出力方向の要求の種類を選択する  
  
-   送信の名前 ID 形式を選択します\(は使用可能な名前 ID を、送信要求の種類 フィールドから選択した場合のみ。\)  
  
-   出力方向の要求の値を指定する  
  
このルールを作成する方法の詳細については、次を参照してください。[グループ メンバーシップを要求として送信するルールを作成](https://technet.microsoft.com/library/ee913569.aspx)です。  
  
## <a name="using-the-claim-rule-language"></a>要求規則言語の使用  
グループ SID 以外の入力方向の SID に基づいて要求を発行する場合は、"入力方向の要求の変換" 規則テンプレートを使用します。 ユーザーがメンバーとして属しているすべてのグループの名前を管理者が取得する場合は、"LDAP 属性を要求として送信する" 規則テンプレートと **tokenGroups** 属性を使用します。  
  
### <a name="example-how-to-issue-group-claims-based-on-the-users-group-membership"></a>以下に例を示します。ユーザーのグループ メンバーシップに基づいて要求を発行する方法  
次の規則は、入力方向のグループ SID に基づいて、ユーザーのグループ要求を発行します。  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-21-397933417-626991126-188441444-512", Issuer == "AD AUTHORITY"]  
=> issue(Type = "http://schemas.xmlsoap.org/claims/Group", Value = "administrators", Issuer = c.Issuer, OriginalIssuer = c.OriginalIssuer, ValueType = c.ValueType);  
```  
  
## <a name="additional-references"></a>その他の参照情報  
[要求として LDAP 属性を送信するルールを作成します。](https://technet.microsoft.com/library/dd807115.aspx)  
  

