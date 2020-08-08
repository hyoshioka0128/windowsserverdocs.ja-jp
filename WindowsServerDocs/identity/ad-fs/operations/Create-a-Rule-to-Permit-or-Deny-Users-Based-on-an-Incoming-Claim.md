---
ms.assetid: 3d770385-9834-4ebe-b66c-b684e0245971
title: 入力方向の要求に基づいてユーザーを許可または拒否する規則を作成する
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: c6d0d1b2d91b4b0983dbe8169e094403bb2c732a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87967286"
---
# <a name="create-a-rule-to-permit-or-deny-users-based-on-an-incoming-claim"></a>入力方向の要求に基づいてユーザーを許可または拒否する規則を作成する


Windows Server 2016 では、 **Access Control ポリシー**を使用して、入力方向の要求に基づいてユーザーを許可または拒否する規則を作成できます。  Windows Server 2012 R2 では、Active Directory フェデレーションサービス (AD FS) AD FS の [**入力方向の要求に基づいてユーザーを許可または拒否**する] 規則テンプレートを使用して、入力 \( \) 方向の要求の種類と値に基づいて、証明書利用者へのユーザーのアクセスを許可または拒否する承認規則を作成できます。

たとえば、これを使用すると、ドメイン管理者の値を持つグループ要求を持つユーザーのみに証明書利用者へのアクセスを許可する規則を作成できます。 すべてのユーザーに証明書利用者へのアクセスを許可する場合は、使用している Windows Server のバージョンに応じて、Everyone Access Control ポリシーを**許可**するか、**すべてのユーザーを許可**する規則テンプレートを使用します。 ユーザーは、フェデレーション サービスから証明書利用者へのアクセスが許可されても、証明書利用者によってサービスが拒否される場合があります。

AD FS 管理スナップインを使用して要求規則を作成するには、次の手順を実行 \- します。

この手順を完了するには、ローカル コンピューター上の **Administrators** または同等のメンバーシップが最低限必要です。  適切なアカウントおよびグループメンバーシップの使用方法の詳細については、「[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)」を参照してください。

## <a name="to-create-a-rule-to-permit-users-based-on-an-incoming-claim-on-windows-server-2016"></a>Windows Server 2016 の入力方向の要求に基づいてユーザーを許可する規則を作成するには

1.  サーバー マネージャーで、 **[ツール]** をクリックし、次に **[AD FS の管理]** を選択します。

2.  コンソールツリーの [ **AD FS**で、[ **Access Control ポリシー**] をクリックします。
![ルールの作成](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny3.PNG)

3. 右クリックして [ **Access Control ポリシーの追加**] を選択します。
![ルールの作成](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny4.PNG)

4. [名前] ボックスに、ポリシーの名前と説明を入力し、[**追加**] をクリックします。
![ルールの作成](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny5.PNG)

5. **ルールエディター**の [ユーザー] の下で、要求に**特定の要求を含む**チェックインを配置し、下部に**ある下線付き**の部分をクリックします。
![ルールの作成](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny6.PNG)

6. [**要求の選択**] 画面で、[**要求**] オプションボタンをクリックし、**要求の種類**、**オペレーター**、および**要求の値**を選択し、[ **Ok**] をクリックします。
![ルールの作成](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny7.PNG)

7.  **ルールエディター**で、[ **Ok]** をクリックします。  [ **Access Control ポリシーの追加**] 画面で、[ **Ok]** をクリックします。

8. **AD FS 管理**コンソールツリーで、[ **AD FS**] の [**証明書**利用者の信頼] をクリックします。
![ルールの作成](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)

9.  アクセスを許可する**証明書利用者信頼**を右クリックし、[ **Access Control ポリシーの編集**] を選択します。
![ルールの作成](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG)

10. [アクセス制御ポリシー] でポリシーを選択し、[**適用**] をクリックして、[ **Ok]** をクリックします。
![ルールの作成](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny8.PNG)

## <a name="to-create-a-rule-to-deny-users-based-on-an-incoming-claim-on-windows-server-2016"></a>Windows Server 2016 の入力方向の要求に基づいてユーザーを拒否する規則を作成するには

1.  サーバー マネージャーで、 **[ツール]** をクリックし、次に **[AD FS の管理]** を選択します。

2.  コンソールツリーの [ **AD FS**で、[ **Access Control ポリシー**] をクリックします。
![ルールの作成](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny3.PNG)

3. 右クリックして [ **Access Control ポリシーの追加**] を選択します。
![ルールの作成](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny4.PNG)

4. [名前] ボックスに、ポリシーの名前と説明を入力し、[**追加**] をクリックします。
![ルールの作成](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny9.PNG)

5. **ルールエディター**で、[すべてのユーザー] が選択されていることを確認し、[**要求内の特定の要求**でチェックイン**を行う]** を選択して、下部に**ある下線付きの部分**をクリックします。
![ルールの作成](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny10.PNG)

6. [**要求の選択**] 画面で、[**要求**] オプションボタンをクリックし、**要求の種類**、**オペレーター**、および**要求の値**を選択し、[ **Ok**] をクリックします。
![ルールの作成](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny11.PNG)

7.  **ルールエディター**で、[ **Ok]** をクリックします。  [ **Access Control ポリシーの追加**] 画面で、[ **Ok]** をクリックします。

8. **AD FS 管理**コンソールツリーで、[ **AD FS**] の [**証明書**利用者の信頼] をクリックします。
![ルールの作成](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)

9.  アクセスを許可する**証明書利用者信頼**を右クリックし、[ **Access Control ポリシーの編集**] を選択します。
![ルールの作成](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG)

10. [アクセス制御ポリシー] でポリシーを選択し、[**適用**] をクリックして、[ **Ok]** をクリックします。
![ルールの作成](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny12.PNG)


## <a name="to-create-a-rule-to-permit-or-deny-users-based-on-an-incoming-claim-on-windows-server-2012-r2"></a>Windows Server 2012 R2 の入力方向の要求に基づいてユーザーを許可または拒否する規則を作成するには

1.  サーバー マネージャーで、 **[ツール]** をクリックし、次に **[AD FS の管理]** を選択します。

2.  コンソールツリーで、[ **AD FS の \\ 信頼関係] [ \\ 証明書利用者信頼**] の下にある一覧で、この規則を作成する特定の信頼をクリックします。

3.  \-選択した信頼を右クリックし、[**要求規則の編集**] をクリックします。
![ルールの作成](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)

4.  [**要求規則の編集**] ダイアログボックスで、必要な承認規則の種類に基づいて [**発行承認規則**] タブまたは [**委任承認**規則] タブをクリックし、[ \( 規則の \) **追加**] をクリックして、**承認要求規則の追加ウィザード**を起動します。
![ルールの作成](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)

5.  [**規則テンプレートの選択**] ページの [**要求規則テンプレート**] で、一覧から [**入力方向の要求に基づいてユーザーを許可または拒否する**] を選択し、[**次へ**] をクリックします。
![ルールの作成](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny1.PNG)

6.  [**規則の構成**] ページの [**要求規則名**] に、この規則の表示名を入力します。 [入力方向の要求の**種類**] で、一覧から要求の種類を選択し、[入力方向の**要求の値**] に値を入力し \( \) ます。

    -   **この入力方向の要求を行ったユーザーのアクセスを許可**

    -   **この入力方向の要求** 
 ![ でユーザーへのアクセスを拒否するルールの作成](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny2.PNG)
7.  **[完了]** をクリックします。

8.  [**要求規則の編集**] ダイアログボックスで、[ **OK** ] をクリックして規則を保存します。

## <a name="additional-references"></a>その他の参照情報
[要求規則を構成する](Configure-Claim-Rules.md)

[チェックリスト:証明書利用者信頼の要求規則の作成](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ee913578(v=ws.11))

[承認要求規則を使用するタイミング](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)

[要求の役割](../../ad-fs/technical-reference/The-Role-of-Claims.md)

[要求規則の役割](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)
