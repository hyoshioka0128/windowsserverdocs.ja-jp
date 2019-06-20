---
ms.assetid: 606df285-259c-4c6b-8583-9aca1d614c43
title: 要求のパススルーとフィルターを使用するタイミングの規則
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 803d939aeaa640e2a8411da156f74f505a2f89d4
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444042"
---
# <a name="when-to-use-a-pass-through-or-filter-claim-rule"></a>要求のパススルーとフィルターを使用するタイミングの規則
この規則を使用するには Active Directory フェデレーション サービスで\(AD FS\)入力方向の要求の値に基づいて、特定の受信要求の種類を取得し、発生させる出力を決定するアクションを適用する必要がある場合。 この規則を使用する場合、次の表の規則ロジックと一致する要求を、規則で構成するオプションに基づいてパススルーまたはフィルター処理します。  
  
|規則のオプション|規則のロジック|  
|---------------|--------------|  
|すべての要求の値をパススルーする|入力方向の要求の種類が "指定した要求の種類" ** に等しく、値が "すべての値" ** に等しい場合、要求をパススルーします|  
|特定の要求値のみをパススルーする|入力方向の要求の種類が "指定した要求の種類" ** に等しく、値が "指定した要求値" ** に等しい場合、要求をパススルーします|  
|特定の電子メールに一致する要求値のみをパススルー\-電子メール サフィックスの値|入力方向の要求の種類が "指定した要求の種類" ** に等しく、値が "指定したサフィックス値" ** に等しい場合、要求をパススルーします|  
|特定の値で始まる要求値のみをパススルーする|入力方向の要求の種類が "指定した要求の種類" ** に等しく、値が "指定した要求値" ** で始まる場合、要求をパススルーします|  
  
次のセクションでは、要求規則の概要と、その規則を使用するタイミングについて詳しく説明します。  
  
## <a name="about-claim-rules"></a>要求規則について  
要求規則が入力方向の要求を実行を条件を適用するビジネス ロジックのインスタンスを表します\(x、y if\)条件パラメーターに基づいて出力方向の要求を生成します。 次の一覧に、このトピックを読む前に理解しておく必要のある、要求規則に関する重要なヒントを示します。  
  
-   AD FS 管理スナップインで\-要求規則テンプレートを使用してルールを作成することができますのみを要求  
  
-   要求規則プロセスが受信要求の要求プロバイダーから直接、 \(Active Directory または別のフェデレーション サービスなど\)または変換要求プロバイダー信頼規則、受け入れの出力から。  
  
-   要求規則は、要求発行エンジンによって、特定の規則セット内で時系列に従って処理されます。 規則に優先順位を設定すると、特定の規則セット内の先行する規則で生成された要求をさらに調整またはフィルター処理できます。  
  
-   要求規則テンプレートでは、常に入力方向の要求の種類を指定する必要があります。 ただし、1 つの規則を使用して、要求の種類が同じ複数の要求の値を処理できます。  
  
詳細については、要求規則および要求規則セットについてを参照してください。 [、要求規則の役割](The-Role-of-Claim-Rules.md)します。 ルールの処理方法の詳細については、次を参照してください。[要求エンジンの役割](The-Role-of-the-Claims-Engine.md)します。 要求規則セットを処理する方法の詳細については、次を参照してください。[要求パイプラインの役割](The-Role-of-the-Claims-Pipeline.md)します。  
  
## <a name="pass-through-all-claim-values"></a>すべての要求の値をパススルーする  
この操作を使用する場合、指定した要求の種類の入力方向の要求値すべてが、出力方向の要求としてパススルーされます。 たとえば、入力方向の要求の種類が "役割" として指定されている場合は、すべての入力方向の要求値が、新しい出力方向の要求に個別にコピーされ、出力方向の要求の種類は "役割" になります。  
  
## <a name="filtering-a-claim"></a>要求のフィルター処理  
用語、ad FS、*要求のフィルタ リング*特定の値のみが渡されるまたは出力方向の要求として経由で送信するための要求値をフィルター処理または受信制限することを意味します。 これを実現するのが、**入力方向の要求のパススルーまたはフィルター処理**規則です。 この規則のプロパティ内で、指定した条件を満たす値のみがパススルーするように、入力方向の値をフィルター処理する条件を設定できます。  
  
たとえば、この規則を使用すると、入力方向の要求の種類が "役割" と一致するとき、またはユーザー名に関する要求のみを発行する必要があるときに、購入者の要求値に一致する要求のみをパススルーできますが、ユーザーの社会保障番号を含む要求はパススルーできません。  
  
この規則でフィルター条件を使用すると、入力方向のすべての要求で、どの要求が規則で設定された条件に一致するかが確認されます。 その他の要求はすべて無視され、指定した要求値の中で、選択した要求の種類に一致するものだけがパススルーします。  
  
次の図に示すようがルール設定されている場合に使用する条件と適合する UPN だけ入力方向の要求をフィルター処理する要求の種類とで終了することも、 @fabrikam.com、この条件を満たしていない限り、その他のすべての入力方向の要求は無視されます。 これにより、E のクレームの種類では、入力方向の要求が含まれます。\-メール アドレスでその要求の値が終了する場合でも@fabrikam.comします。 ここでの値を含む要求のみNick@fabrikam.com証明書利用者に送信されます。  
  
![パスを使用するときに使用](media/adfs2_filter.gif)  
  
## <a name="configuring-this-rule-on-a-claims-provider-trust"></a>要求プロバイダー信頼でのこの規則の構成  
要求プロバイダー信頼を使用する場合、この規則は、特定の制約に一致する要求プロバイダーからの入力方向の要求のみをパススルーするように構成できます。 電子メールのみを許可するなど、\-メールが要求プロバイダーからクレーム電子メールを受け入れるようにこの規則テンプレートを使用するため、\-メールの末尾が要求プロバイダーのドメイン ネーム システムに要求の種類\(DNS。\)名。  
  
## <a name="configuring-this-rule-on-a-relying-party-trust"></a>証明書利用者の信頼でのこの規則の構成  
証明書利用者の信頼を使用すると、この規則は、証明書利用者に送信される出力方向の要求をパススルーまたはフィルター処理するように構成できます。 要求の種類すべてを、すべての証明書利用者が認識できるとは限りません。また、要求によっては、特定の証明書利用者に送信しないようにする必要がある機密情報が含まれる場合もあります。 この規則テンプレートは、特定の証明書利用者の信頼に対して、こうしたポリシーを適用するのに役立ちます。  
  
## <a name="how-to-create-this-rule"></a>この規則の作成方法  
要求規則言語を使用して、またはパススルーを使用して、この規則を作成または AD FS 管理スナップインで、入力方向の要求規則テンプレートをフィルター処理する\-でします。 この規則テンプレートには、次の構成オプションがあります。  
  
-   要求規則名を指定する  
  
-   入力方向の要求の種類を指定する  
  
-   すべての要求の値をパススルーする  
  
-   特定の要求値のみをパススルーする  
  
-   特定の電子メールに一致する要求値のみをパススルー\-電子メール サフィックスの値  
  
-   特定の値で始まる要求値のみをパススルーする  
  
このテンプレートを作成する方法の詳細については、次を参照してください。[パススルーするルールを作成または入力方向の要求をフィルター処理](https://technet.microsoft.com/library/dd807060.aspx)AD FS Deployment guide の「します。  
  
## <a name="using-the-claim-rule-language"></a>要求規則言語の使用  
要求値がカスタム パターンに一致する場合にのみ要求を送信する場合は、カスタム規則を使用する必要があります。 詳細については、カスタム規則を使用するタイミングに関するトピックを参照してください。  
  
### <a name="examples-of-how-to-construct-a-pass-through-or-filter-rule-syntax"></a>パススルーとフィルター処理規則の構文の作成例  
シンプルなフィルター処理規則では、上記で説明したプロパティのいずれかに基づいて要求をフィルター処理します。 すべての電子メールに、次の規則はパススルーなど\-要求のメールします。  
  
```  
c:[type == “http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress”]  => issue(claim  = c);  
```  
  
フィルターに論理的には AND\-連結します。 たとえば、次の規則がすべての電子メールを受け入れますが\-メールの値を持つ信頼性情報 johndoe@fabrikam.com:  
  
```  
c:[type == “http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress”, value == “johndoe@fabrikam.com “]  => issue(claim  = c);  
```  
  
前の例では、フィルターには常に等価演算子が使用されています。 要求規則言語でサポートされる演算子を次に示します。  
  
-   \=\= \- 等しい\(ケース\-機密性の高い\)  
  
-   \!\= \- 等しくない\(ケース\-機密性の高い\)  
  
-   \=~\- 正規表現の一致  
  
-   \!~ \- 非正規\-一致  
  
たとえば、次の規則がすべての電子メールを受け入れますが\-boeing.com のサフィックスを持つ、ローカルのフェデレーション サーバーによって発行されていない要求を送信します。  
  
```  
c:[type == “http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress”, value =~ “^.*@boeing\.com$” , issuer != “LOCAL AUTHORITY”]  => issue(claim  = c);  
```  
  
### <a name="best-practices-for-creating-custom-rules"></a>カスタム規則を作成するためのベスト プラクティス  
次の表で説明するように、フィルターは、各要求の 1 つ以上のプロパティに適用できます。  
  

| 要求のプロパティ |                                                                                                                                                                                                                                                                                                                                                  説明                                                                                                                                                                                                                                                                                                                                                  |
|----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      種類      |                                                                                                                                                                                        要求の種類\(通常、Uri として表される\)情報の種類は、要求で伝達に関するフェデレーション パートナー間の暗黙の同意が反映されます。 種類は http の要求など:\/\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/クレーム\/emailaddress eが含まれます\-、ユーザーのメール アドレス。                                                                                                                                                                                         |
|     Value      |                                                                                                                                                                                                                                                                   要求の値。 種類は http の要求など:\/\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/クレーム\/emailaddress 場合の値があります johndoe@fabrikam.com                                                                                                                                                                                                                                                                    |
|   ValueType    |                                                                                                                                                                                                  ValueType は、要求の値に含まれる情報を解釈する方法を表します。 通常、ValueType は http に設定されます:\/\/www.w3.org\/2001\/XMLSchema\#Base64Binary でエンコードされたデータを含めることが、文字列は、要求の値\(イメージなど、\)または日付、ブール値、およびなど。                                                                                                                                                                                                  |
|     発行者     | 発行者は、前回ユーザーに関する要求を発行したパーティです。 要求が要求プロバイダーのフェデレーション サーバーで取得された場合は、すべての要求の発行者が "LOCAL AUTHORITY" に設定されます。 フェデレーション プロバイダーのフェデレーション サーバーが要求を受信した場合、要求の発行者は、トークンに署名した要求プロバイダーの要求プロバイダー識別子に設定されます。 このため、要求プロバイダーから受信した要求の規則を処理するときは、すべての要求の発行者が同じ値に設定されます。 証明書利用者の規則を作成するとき、発行者のプロパティを使用して、別の要求プロバイダーから送信された要求を区別できます。 |
| OriginalIssuer |                                                                                                   この要求プロパティの目的は、要求を最初に発行したフェデレーション サーバーを伝達することです。 発行元はクレームが 1 つ以上のフェデレーション サーバーを介してに対して実行された場所のシナリオで便利なため、要求の issuer プロパティは、トークンに署名したフェデレーション サーバーを設定、最後に、\(など、証明書利用者、トークンを受信します。フェデレーション サーバーの利用可能性があるフェデレーション プロバイダーからユーザーを認証する特定の要求プロバイダーのフェデレーション サーバー\)                                                                                                   |
|   プロパティ   |                                                                                                                             上記で説明した 5 つのプロパティのほかに、名前付きプロパティを格納できるプロパティ バッグが各要求にあります。 これらのプロパティはトークンでシリアル化されません。また、1 台のフェデレーション サーバーのスコープ内の要求発行パイプラインのコンポーネント間で情報をやり取りする場合にのみ有効です。 たとえば、要求プロバイダー規則の処理中にプロパティを設定し、証明書利用者の規則でそのプロパティを参照します。                                                                                                                              |
