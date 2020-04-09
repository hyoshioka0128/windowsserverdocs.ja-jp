---
ms.assetid: 3d770385-9834-4ebe-b66c-b684e0245971
title: 入力方向の要求に基づいてユーザーを許可または拒否する規則を作成する
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 7d6be5b9194060bb16673e01e0fee8b36b081769
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816815"
---
# <a name="create-a-rule-to-permit-or-deny-users-based-on-an-incoming-claim"></a>入力方向の要求に基づいてユーザーを許可または拒否する規則を作成する 


Windows Server 2016 では、 **Access Control ポリシー**を使用して、入力方向の要求に基づいてユーザーを許可または拒否する規則を作成できます。  Windows Server 2012 R2 では、Active Directory フェデレーションサービス (AD FS) \(AD FS\)の [**入力方向の要求に基づいてユーザーを許可または拒否**する] 規則テンプレートを使用して、入力方向の要求の種類と値に基づいて、証明書利用者へのユーザーのアクセスを許可または拒否する承認規則を作成できます。 

たとえば、これを使用すると、ドメイン管理者の値を持つグループ要求を持つユーザーのみに証明書利用者へのアクセスを許可する規則を作成できます。 すべてのユーザーに証明書利用者へのアクセスを許可する場合は、使用している Windows Server のバージョンに応じて、Everyone Access Control ポリシーを**許可**するか、**すべてのユーザーを許可**する規則テンプレートを使用します。 ユーザーは、フェデレーション サービスから証明書利用者へのアクセスが許可されても、証明書利用者によってサービスが拒否される場合があります。  
  
で AD FS 管理スナップ\-を使用して要求規則を作成するには、次の手順を実行します。  
  
この手順を完了するには、ローカル コンピューター上の **Administrators** または同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。  

## <a name="to-create-a-rule-to-permit-users-based-on-an-incoming-claim-on-windows-server-2016"></a>Windows Server 2016 の入力方向の要求に基づいてユーザーを許可する規則を作成するには
 
1.  サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** を選択します。  
  
2.  コンソールツリーの  **AD FS**で、**Access Control ポリシー** をクリックします。 
ルール](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny3.PNG) を作成 ![には

3. 右クリックして **[Access Control ポリシーの追加]** を選択します。
ルール](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny4.PNG) を作成 ![には

4. 名前 ボックスに、ポリシーの名前と説明を入力し、**追加** をクリックします。
ルール](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny5.PNG) を作成 ![には

5. **ルールエディター**の [ユーザー] の下で、要求に**特定の要求を含む**チェックインを配置し、下部に**ある下線付き**の部分をクリックします。
ルール](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny6.PNG) を作成 ![には

6. **[要求の選択]** 画面で、 **[要求]** オプションボタンをクリックし、**要求の種類**、**オペレーター**、および**要求の値**を選択し、 **[Ok]** をクリックします。
ルール](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny7.PNG) を作成 ![には

7.  **ルールエディター**で、[ **Ok]** をクリックします。  **[Access Control ポリシーの追加]** 画面で、[ **Ok]** をクリックします。

8. **AD FS 管理**コンソールツリーで、 **[AD FS]** の **[証明書]** 利用者の信頼 をクリックします。 
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG) を作成 ![には

9.  アクセスを許可する**証明書利用者信頼**を右クリックし、 **[Access Control ポリシーの編集]** を選択します。  
ルール](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG) を作成 ![には

10. アクセス制御ポリシー でポリシーを選択し、**適用** をクリックして、 **Ok**をクリックします。
ルール](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny8.PNG) を作成 ![には

## <a name="to-create-a-rule-to-deny-users-based-on-an-incoming-claim-on-windows-server-2016"></a>Windows Server 2016 の入力方向の要求に基づいてユーザーを拒否する規則を作成するには
 
1.  サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** を選択します。  
  
2.  コンソールツリーの  **AD FS**で、**Access Control ポリシー** をクリックします。 
ルール](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny3.PNG) を作成 ![には

3. 右クリックして **[Access Control ポリシーの追加]** を選択します。
ルール](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny4.PNG) を作成 ![には

4. 名前 ボックスに、ポリシーの名前と説明を入力し、**追加** をクリックします。
ルール](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny9.PNG) を作成 ![には

5. **ルールエディター**で、[すべてのユーザー] が選択されていることを確認し、[**要求内の特定の要求**でチェックイン**を行う]** を選択して、下部に**ある下線付きの部分**をクリックします。
ルール](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny10.PNG) を作成 ![には

6. **[要求の選択]** 画面で、 **[要求]** オプションボタンをクリックし、**要求の種類**、**オペレーター**、および**要求の値**を選択し、 **[Ok]** をクリックします。
ルール](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny11.PNG) を作成 ![には

7.  **ルールエディター**で、[ **Ok]** をクリックします。  **[Access Control ポリシーの追加]** 画面で、[ **Ok]** をクリックします。

8. **AD FS 管理**コンソールツリーで、 **[AD FS]** の **[証明書]** 利用者の信頼 をクリックします。 
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG) を作成 ![には

9.  アクセスを許可する**証明書利用者信頼**を右クリックし、 **[Access Control ポリシーの編集]** を選択します。  
ルール](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG) を作成 ![には

10. アクセス制御ポリシー でポリシーを選択し、**適用** をクリックして、 **Ok**をクリックします。
ルール](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny12.PNG) を作成 ![には

  
## <a name="to-create-a-rule-to-permit-or-deny-users-based-on-an-incoming-claim-on-windows-server-2012-r2"></a>Windows Server 2012 R2 の入力方向の要求に基づいてユーザーを許可または拒否する規則を作成するには
  
1.  サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** を選択します。    
  
2.  コンソールツリーの [ **AD FS\\信頼関係\\証明書利用者信頼**] の下で、この規則を作成する特定の信頼を一覧からクリックします。  
  
3.  選択した信頼を右\-クリックし、 **[要求規則の編集]** をクリックします。  
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG) を作成 ![には   

4.  **[要求規則の編集]** ダイアログボックスで、 **[発行承認規則]** タブまたは **[委任承認]** 規則 タブをクリックし、\)必要な承認規則の種類に基づいて \(します。次に、 **[規則の追加]** をクリックして、**承認要求規則の追加ウィザード**を開始します。  
ルール](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG) を作成 ![には

5.  **[規則テンプレートの選択]** ページの **[要求規則テンプレート]** で、一覧から **[入力方向の要求に基づいてユーザーを許可または拒否する]** を選択し、 **[次へ]** をクリックします。  
ルール](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny1.PNG) を作成 ![には

6.  **[規則の構成]** ページの **[要求規則名]** に、この規則の表示名を入力し、入力方向の要求の **[種類]** ボックスの一覧で要求の種類を選択します。 入力方向の **[要求の値]** に値を入力するか、[\) \(参照] をクリックして値を選択します  
  
    -   **この入力方向の要求でユーザーにアクセスを許可する**  
  
    -   **この入力方向の要求でユーザーへのアクセスを拒否する**  
ルール](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny2.PNG) を作成 ![には  
7.  **[完了]** をクリックします。  
  
8.  **[要求規則の編集]** ダイアログボックスで、 **[OK]** をクリックして規則を保存します。  

## <a name="additional-references"></a>その他の参照情報 
[要求規則を構成する](Configure-Claim-Rules.md)  
 
[チェックリスト: 証明書利用者信頼の要求規則を作成する](https://technet.microsoft.com/library/ee913578.aspx)  
  
[承認要求規則を使用する場合](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[要求の役割](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[要求規則の役割](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
