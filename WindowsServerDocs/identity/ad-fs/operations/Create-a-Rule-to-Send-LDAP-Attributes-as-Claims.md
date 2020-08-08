---
ms.assetid: 66664b80-2590-46c0-bfca-82402088e42c
title: LDAP 属性を要求として送信するルールを作成する
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 938e82f5318bc374fd3f89bf5354c2fc447a9723
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87967209"
---
# <a name="create-a-rule-to-send-ldap-attributes-as-claims"></a>LDAP 属性を要求として送信するルールを作成する


Active Directory フェデレーションサービス (AD FS) AD FS で "LDAP 属性を要求として送信" 規則テンプレートを使用して、Active Directory などの \( \) ライトウェイトディレクトリアクセスプロトコル LDAP 属性ストアから属性を選択し、 \( \) 証明書利用者に要求として送信する規則を作成できます。 たとえば、この規則テンプレートを使用して、[LDAP 属性を要求として送信] 規則を作成して、認証されたユーザーの属性値を**displayName**属性と**telephoneNumber** Active Directory 属性から抽出し、それらの値を2つの異なる出力方向の要求として送信することができます。

この規則を使用して、すべてのユーザーのグループメンバーシップを送信することもできます。 個々のグループのメンバーシップのみを送信する場合は、"グループ メンバーシップを要求として送信" 規則テンプレートを使用します。 AD FS 管理スナップインを使用して要求規則を作成するには、次の手順を実行 \- します。

この手順を完了するには、ローカル コンピューター上の **Administrators** または同等のメンバーシップが最低限必要です。  適切なアカウントおよびグループメンバーシップの使用方法の詳細については、「[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)」を参照してください。

## <a name="to-create-a-rule-to-send-ldap-attributes-as-claims-for-a-relying-party-trust-in-windows-server-2016"></a>Windows Server 2016 で証明書利用者信頼の要求として LDAP 属性を送信する規則を作成するには

1.  サーバー マネージャーで、 **[ツール]** をクリックし、次に **[AD FS の管理]** を選択します。

2.  コンソールツリーの [ **AD FS**で、[**証明書利用者の信頼**] をクリックします。
![ルールの作成](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)

3.  \-選択した信頼を右クリックし、[**要求の発行ポリシーの編集**] をクリックします。
![ルールの作成](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)

4.  [**要求発行ポリシーの編集**] ダイアログボックスの [**発行変換規則**] で、[**規則の追加**] をクリックして規則ウィザードを開始します。
![ルールの作成](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)

5.  [**規則テンプレートの選択**] ページの [**要求規則テンプレート**] で、一覧から [ **LDAP 属性を要求として送信**] を選択し、[**次へ**] をクリックします。
![ルールの作成](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap1.PNG)

6.  [**規則の構成**] ページの [**要求規則名**] に、この規則の表示名を入力し、**属性ストア**を選択します。次に、LDAP 属性を選択して、出力方向の要求の種類にマップします。
![ルールの作成](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap2.PNG)

7.  **[完了]** をクリックします。

8.  [**要求規則の編集**] ダイアログボックスで、[ **OK** ] をクリックして規則を保存します。

## <a name="to-create-a-rule-to-send-ldap-attributes-as-claims-for-a-claims-provider-trust-in-windows-server-2016"></a>Windows Server 2016 の要求プロバイダー信頼の要求として LDAP 属性を送信する規則を作成するには

1.  サーバー マネージャーで、 **[ツール]** をクリックし、次に **[AD FS の管理]** を選択します。

2.  コンソールツリーの [ **AD FS**で、[**要求プロバイダー信頼**] をクリックします。
![ルールの作成](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)

3.  \-選択した信頼を右クリックし、[**要求規則の編集**] をクリックします。
![ルールの作成](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)

4.  [**要求規則の編集**] ダイアログボックスの [**受け入れ変換規則**] で、[**規則の追加**] をクリックして規則ウィザードを開始します。
![ルールの作成](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)

5.  [**規則テンプレートの選択**] ページの [**要求規則テンプレート**] で、一覧から [ **LDAP 属性を要求として送信**] を選択し、[**次へ**] をクリックします。
![ルールの作成](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap1.PNG)

6.  [**規則の構成**] ページの [**要求規則名**] に、この規則の表示名を入力し、**属性ストア**を選択します。次に、LDAP 属性を選択して、出力方向の要求の種類にマップします。
![ルールの作成](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap2.PNG)

7.  **[完了]** をクリックします。

8.  [**要求規則の編集**] ダイアログボックスで、[ **OK** ] をクリックして規則を保存します。



## <a name="to-create-a-rule-to-send-ldap-attributes-as-claims-for-windows-server-2012-r2"></a>Windows Server 2012 R2 の要求として LDAP 属性を送信するルールを作成するには

1.  サーバー マネージャーで、 **[ツール]** をクリックし、次に **[AD FS の管理]** を選択します。

2.  コンソールツリーの [ **AD FSAD FS の \\ 信頼関係**] で、[**要求プロバイダー信頼**] または [**証明書利用者信頼**] をクリックし、この規則を作成する一覧内の特定の信頼をクリックします。

3.  \-選択した信頼を右クリックし、[**要求規則の編集**] をクリックします。
![ルールの作成](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)

4.  [**要求規則の編集**] ダイアログボックスで、編集する信頼とこの規則を作成する規則セットに応じて、次のタブのいずれかを選択し、[**規則の追加**] をクリックして、その規則セットに関連付けられている規則ウィザードを開始します。

    -   **受け入れ変換規則**

    -   **発行変換規則**

    -   **発行承認規則**

    -   **委任の承認規則** 
 ![ルールの作成](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)

5.  [**規則テンプレートの選択**] ページの [**要求規則テンプレート**] で、一覧から [ **LDAP 属性を要求として送信**] を選択し、[**次へ**] をクリックします。
![ルールの作成](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap3.PNG)

6.  [**規則の構成**] ページの [**要求規則名**] の下で、この規則の表示名を入力し、[**属性ストア**] で [ **Active Directory**を選択します。また、[ **ldap 属性と出力方向の要求の種類のマッピング**] で、ドロップダウンリストから目的の**ldap 属性**と対応する**出力方向の要求**の種類を選択し \- ます。

    この規則の一部として要求を発行する Active Directory 属性ごとに、別の行で新しい LDAP 属性と出力方向の要求の種類のペアを選択する必要があります。
![ルールの作成](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap4.PNG)
7.  **[完了]** をクリックします。

8.  [**要求規則の編集**] ダイアログボックスで、[ **OK** ] をクリックして規則を保存します。

## <a name="additional-references"></a>その他の参照情報
[要求規則を構成する](Configure-Claim-Rules.md)

[チェックリスト:証明書利用者信頼の要求規則の作成](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ee913578(v=ws.11))

[チェックリスト:要求プロバイダー信頼の要求規則の作成](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ee913564(v=ws.11))

[承認要求規則を使用するタイミング](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)

[要求の役割](../../ad-fs/technical-reference/The-Role-of-Claims.md)

[要求規則の役割](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)
