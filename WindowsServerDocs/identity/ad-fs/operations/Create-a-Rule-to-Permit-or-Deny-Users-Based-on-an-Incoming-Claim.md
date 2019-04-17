---
ms.assetid: 3d770385-9834-4ebe-b66c-b684e0245971
title: "許可または入力方向の要求に基づいてユーザーを拒否する規則を作成します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: afcbb8c7a08a84eda2a794c9565061d7d61d470b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-rule-to-permit-or-deny-users-based-on-an-incoming-claim"></a>許可または入力方向の要求に基づいてユーザーを拒否する規則を作成します。 

>適用対象: Windows Server 2016、Windows Server 2012 R2

Windows Server 2016 で使用することができます、**アクセス制御ポリシー**を許可する規則を作成する入力方向の要求に基づいてユーザーを拒否します。  Windows Server 2012 R2 でを使用して、**の許可または拒否に基づいてユーザー入力方向の要求**、Active Directory フェデレーション サービス \(AD FS\) 規則テンプレートを付与または種類と、入力方向の要求の値に基づいて証明書利用者へのユーザーのアクセスを拒否する承認規則を作成することができます。 

たとえば、要求の証明書利用者にアクセスするのに Domain Admins という値を持つグループのユーザーのみを許可する規則を作成するのにこのを使用することができます。 証明書利用者にアクセスを使用してすべてのユーザーを許可する場合、**すべてのユーザーを許可**アクセス制御ポリシー、または**すべてのユーザーを許可**規則テンプレートの Windows Server のバージョンによって異なります。 ユーザーは、フェデレーション サービスから証明書利用者にアクセスする許可されている可能性がありますもによって拒否されるサービス証明書利用者のパーティします。  
  
次の手順を使用するには、AD FS 管理スナップインの要求規則の作成をします。  
  
メンバーシップ**管理者**、相当するもので、ローカル コンピューターでは、この手順を完了するために必要な最低限またはします。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。  

## <a name="to-create-a-rule-to-permit-users-based-on-an-incoming-claim-on-windows-server-2016"></a>Windows Server 2016 での入力方向の要求に基づいてユーザーを許可する規則を作成するには
 
1.  サーバー マネージャーで、クリックして**ツール**、し、[ **AD FS 管理**します。  
  
2.  コンソール ツリーで、[ **AD FS**、] をクリックして**アクセス制御ポリシー**します。 
![規則を作成します。](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny3.PNG)

3. 右クリックして選択**アクセス制御ポリシーの追加**します。
![規則を作成します。](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny4.PNG)

4. [名前] ボックスの名前を入力、ポリシー、説明、およびクリック**追加**します。
![規則を作成します。](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny5.PNG)

5. **規則エディター**、ユーザー] の下で、チェックを配置**要求で特定のクレームを含む**、下線付き] をクリック**特定**下部にあります。
![規則を作成します。](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny6.PNG)

6. **信頼性情報の選択**画面で、をクリックして、**信頼性情報**ラジオ ボタンを選択、**要求の種類**、**演算子**、および**要求の値**] をクリックし、 **Ok**します。
![規則を作成します。](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny7.PNG)

7.  **規則エディター**クリックして**Ok**します。  **アクセス制御ポリシーの追加**画面で、[ **Ok**します。

8. **AD FS 管理**コンソール ツリーの [ **AD FS**、] をクリックして**証明書利用者信頼**します。 
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)

9.  右クリックし、 **Relying Party Trust**へのアクセス許可を選択する**アクセス制御ポリシーの編集**します。  
![規則を作成します。](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG)

10. アクセス制御ポリシー ポリシーを選択し、をクリックして**適用**と**Ok**します。
![規則を作成します。](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny8.PNG)

## <a name="to-create-a-rule-to-deny-users-based-on-an-incoming-claim-on-windows-server-2016"></a>Windows Server 2016 での入力方向の要求に基づいてユーザーを拒否する規則を作成するには
 
1.  サーバー マネージャーで、クリックして**ツール**、し、[ **AD FS 管理**します。  
  
2.  コンソール ツリーで、[ **AD FS**、] をクリックして**アクセス制御ポリシー**します。 
![規則を作成します。](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny3.PNG)

3. 右クリックして選択**アクセス制御ポリシーの追加**します。
![規則を作成します。](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny4.PNG)

4. [名前] ボックスの名前を入力、ポリシー、説明、およびクリック**追加**します。
![規則を作成します。](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny9.PNG)

5. **規則エディター**、すべてのユーザーが選択されていることを確認し、[**を除く**でチェック ボックスをオン**要求で特定のクレームを含む**、下線付き] をクリック**特定**下部にあります。
![規則を作成します。](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny10.PNG)

6. **信頼性情報の選択**画面で、をクリックして、**信頼性情報**ラジオ ボタンを選択、**要求の種類**、**演算子**、および**要求の値**] をクリックし、 **Ok**します。
![規則を作成します。](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny11.PNG)

7.  **規則エディター**クリックして**Ok**します。  **アクセス制御ポリシーの追加**画面で、[ **Ok**します。

8. **AD FS 管理**コンソール ツリーの [ **AD FS**、] をクリックして**証明書利用者信頼**します。 
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)

9.  右クリックし、 **Relying Party Trust**へのアクセス許可を選択する**アクセス制御ポリシーの編集**します。  
![規則を作成します。](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG)

10. アクセス制御ポリシー ポリシーを選択し、をクリックして**適用**と**Ok**します。
![規則を作成します。](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny12.PNG)

  
## <a name="to-create-a-rule-to-permit-or-deny-users-based-on-an-incoming-claim-on-windows-server-2012-r2"></a>許可または Windows Server 2012 R2 での入力方向の要求に基づいてユーザーを拒否する規則を作成するには
  
1.  サーバー マネージャーで、クリックして**ツール**、し、[ **AD FS 管理**します。    
  
2.  コンソール ツリーで、[ **AD FS\\Trust Relationships\\Relying パーティー信頼**、この規則を作成するリスト内の特定の信頼をクリックします。  
  
3.  選択した信頼を右クリックし、クリック**要求規則の編集**します。  
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)   

4.  **要求規則の編集**ダイアログ ボックスで、] をクリックして、**発行承認規則**] タブまたは**委任承認規則**] タブの [\ (に基づいて承認規則の種類を require\)、] をクリックし、**規則の追加**を開始する、**承認の要求規則の追加ウィザード**します。  
![規則を作成します。](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)

5.  **規則テンプレートの選択**ページで、**要求規則テンプレート**[**の許可または拒否する入力方向の要求に基づくユーザー**クリックして、一覧から**[次へ]**します。  
![規則を作成します。](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny1.PNG)

6.  **規則の構成**] ページの [**要求規則名**でこの規則の表示名を入力**入力方向の要求の種類**下にある一覧で、要求の種類を選択**入力方向の要求の値**値を入力するか、[参照] をクリックして \ (available\ の場合) 値を選択し、組織のニーズに応じて、次のオプションのいずれかを選択します。  
  
    -   **この入力方向の要求を持つユーザーにアクセスを許可します。**  
  
    -   **この入力方向の要求を持つユーザーにアクセス権を拒否します。**  
![規則を作成します。](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny2.PNG)  
7.  をクリックして**完了**します。  
  
8.  **要求規則の編集**ダイアログ ボックスで、] をクリックして**OK**に規則を保存します。  

## <a name="additional-references"></a>その他の参照 
[要求規則を構成します。](Configure-Claim-Rules.md)  
 
[チェックリスト: 証明書利用者のパーティ信頼の要求規則を作成します。](https://technet.microsoft.com/library/ee913578.aspx)  
  
[When to Use an Authorization Claim Rule](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[要求の役割](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[要求規則の役割](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
