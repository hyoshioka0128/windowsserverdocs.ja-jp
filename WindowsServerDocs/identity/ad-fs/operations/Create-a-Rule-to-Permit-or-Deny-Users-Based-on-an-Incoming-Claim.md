---
ms.assetid: 3d770385-9834-4ebe-b66c-b684e0245971
title: 入力方向の要求に基づいてユーザーを許可または拒否する規則を作成する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 72fe425b040f83a217a144976265c7754830c91b
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189505"
---
# <a name="create-a-rule-to-permit-or-deny-users-based-on-an-incoming-claim"></a>入力方向の要求に基づいてユーザーを許可または拒否する規則を作成する 


Windows Server 2016 で使用することができます、**アクセス制御ポリシー**を許可または入力方向の要求に基づいてユーザーを拒否する規則を作成します。  Windows Server 2012 r2 を使用して、**を許可または拒否する入力方向の要求に基づくユーザー**規則テンプレートの Active Directory フェデレーション サービスで\(AD FS\)を許可する承認規則を作成することができますか型と、入力方向の要求の値に基づいて証明書利用者のパーティには、ユーザーのアクセスを拒否します。 

たとえば、要求の証明書利用者へのアクセスに Domain Admins の値を持つグループがあるユーザーのみを許可する規則を作成するのにこれを使用することができます。 すべてのユーザー証明書利用者へのアクセスを許可する場合、**すべてのユーザーを許可**アクセス制御ポリシー、または**すべてのユーザーを許可**Windows Server のバージョンによってルール テンプレート。 ユーザーは、フェデレーション サービスから証明書利用者へのアクセスが許可されても、証明書利用者によってサービスが拒否される場合があります。  
  
次の手順を使用するには、AD FS 管理スナップインで要求規則を作成する\-でします。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。  

## <a name="to-create-a-rule-to-permit-users-based-on-an-incoming-claim-on-windows-server-2016"></a>Windows Server 2016 での入力方向の要求に基づいてユーザーを許可するルールを作成するには
 
1.  サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  
  
2.  コンソール ツリーで [ **AD FS**、] をクリックして**アクセス制御ポリシー**します。 
![ルールを作成します。](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny3.PNG)

3. 右クリックして**アクセス制御ポリシーの追加**します。
![ルールを作成します。](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny4.PNG)

4. 名 ボックスに、ポリシー、説明およびクリックの名前を入力します。**追加**します。
![ルールを作成します。](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny5.PNG)

5. **ルール エディター**、ユーザー で、配置をオンに**要求で特定のクレームを含む**下線の付いた をクリック**特定**下部にあります。
![ルールを作成します。](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny6.PNG)

6. **要求を選択します**画面で、をクリックして、**要求**ラジオ ボタンを選択、**要求の種類**、**演算子**、および**要求の値**クリックして**Ok**します。
![ルールを作成します。](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny7.PNG)

7.  **ルール エディター**クリックして**Ok**します。  **アクセス制御ポリシーの追加**画面で、 **Ok**します。

8. **AD FS 管理**コンソール ツリーの [ **AD FS**、] をクリックして**証明書利用者信頼**します。 
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)

9.  右クリックし、 **Relying Party Trust**へのアクセスを許可しを選択したい**アクセス制御ポリシーの編集**します。  
![ルールを作成します。](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG)

10. アクセス制御ポリシー、ポリシーを選択し、順にクリックします**適用**と**Ok**します。
![ルールを作成します。](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny8.PNG)

## <a name="to-create-a-rule-to-deny-users-based-on-an-incoming-claim-on-windows-server-2016"></a>Windows Server 2016 での入力方向の要求に基づいてユーザーを拒否する規則を作成するには
 
1.  サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  
  
2.  コンソール ツリーで [ **AD FS**、] をクリックして**アクセス制御ポリシー**します。 
![ルールを作成します。](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny3.PNG)

3. 右クリックして**アクセス制御ポリシーの追加**します。
![ルールを作成します。](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny4.PNG)

4. 名 ボックスに、ポリシー、説明およびクリックの名前を入力します。**追加**します。
![ルールを作成します。](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny9.PNG)

5. **ルール エディター**、すべてのユーザーが選択されていることを確認し、[**を除く**でチェック ボックスをオン**要求で特定のクレームを含む**下線の付いた] をクリック**特定**下部にあります。
![ルールを作成します。](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny10.PNG)

6. **要求を選択します**画面で、をクリックして、**要求**ラジオ ボタンを選択、**要求の種類**、**演算子**、および**要求の値**クリックして**Ok**します。
![ルールを作成します。](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny11.PNG)

7.  **ルール エディター**クリックして**Ok**します。  **アクセス制御ポリシーの追加**画面で、 **Ok**します。

8. **AD FS 管理**コンソール ツリーの [ **AD FS**、] をクリックして**証明書利用者信頼**します。 
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)

9.  右クリックし、 **Relying Party Trust**へのアクセスを許可しを選択したい**アクセス制御ポリシーの編集**します。  
![ルールを作成します。](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG)

10. アクセス制御ポリシー、ポリシーを選択し、順にクリックします**適用**と**Ok**します。
![ルールを作成します。](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny12.PNG)

  
## <a name="to-create-a-rule-to-permit-or-deny-users-based-on-an-incoming-claim-on-windows-server-2012-r2"></a>許可または Windows Server 2012 R2 での入力方向の要求に基づいてユーザーを拒否する規則を作成するには
  
1.  サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。    
  
2.  コンソール ツリーで  **AD FS\\信頼関係\\証明書利用者信頼**、この規則を作成するリスト内の特定の信頼をクリックします。  
  
3.  右\-選択の信頼をクリックし、クリックして**要求規則の編集**します。  
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)   

4.  **要求規則の編集**ダイアログ ボックスで、をクリックして、**発行承認規則の** タブまたは**委任承認規則**タブ\(の種類に基づく必要な承認規則\)、 をクリックし、**規則の追加**を開始する、**承認の要求規則の追加ウィザード**。  
![ルールを作成します。](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)

5.  **規則テンプレートの選択** ページ **要求規則テンプレート**を選択します**を許可または拒否する入力方向の要求に基づくユーザー**  をクリックし、一覧から **次へ** します。  
![ルールを作成します。](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny1.PNG)

6.  **規則の構成**ページ**要求規則名**で、この規則の表示名を入力**着信要求の種類**一覧で、要求の種類を選択**方向の要求値**値を入力するか、参照ボタン クリックして\(入手可能になった場合\)値を選択し、組織のニーズに応じて、次のオプションのいずれかを選択。  
  
    -   **この着信要求でユーザーへのアクセスを許可します。**  
  
    -   **この着信要求でユーザー アクセスを拒否します。**  
![ルールを作成します。](media/Create-a-Rule-to-Permit-or-Deny-Users-Based-on-an-Incoming-Claim/permitdeny2.PNG)  
7.  **[Finish]** (完了) をクリックします。  
  
8.  **要求規則の編集**ダイアログ ボックスで、をクリックして **[ok]** ルールを保存します。  

## <a name="additional-references"></a>その他の参照情報 
[要求規則を構成する](Configure-Claim-Rules.md)  
 
[チェックリスト:証明書利用者信頼の要求規則の作成](https://technet.microsoft.com/library/ee913578.aspx)  
  
[承認要求規則を使用する場合](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[要求の役割](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[要求規則の役割](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
