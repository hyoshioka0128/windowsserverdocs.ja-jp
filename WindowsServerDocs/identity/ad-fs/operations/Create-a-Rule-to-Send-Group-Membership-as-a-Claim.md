---
ms.assetid: 475e34f9-9399-43f4-a840-9dd77258e11a
title: グループ メンバーシップを要求として送信する規則を作成する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: b8217302cc0ec5bc6972004cb2f26ffae1371614
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407584"
---
# <a name="create-a-rule-to-send-group-membership-as-a-claim"></a>グループ メンバーシップを要求として送信する規則を作成する

Active Directory フェデレーションサービス (AD FS) \(ADFS\)で "グループメンバーシップを要求として送信する" 規則テンプレートを使用して、要求として送信する Active Directory セキュリティグループを選択できるようにする規則を作成できます。 選択したグループに基づいて、この規則から1つの要求のみが出力されます。 たとえば、この規則テンプレートを使用すると、ユーザーが Domain Admins セキュリティグループのメンバーである場合に、値が Admin のグループ要求を送信する規則を作成できます。 この規則は、ローカル Active Directory ドメイン内のユーザーに対してのみ使用してください。  
  
AD FS 管理スナップイン\-を使用して要求規則を作成するには、次の手順を実行します。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   

## <a name="to-create-a-rule-to-send-group-membership-as-a-claim-on-a-relying-party-trust-in-windows-server-2016"></a>Windows Server 2016 の証明書利用者信頼に対してグループメンバーシップを要求として送信する規則を作成するには 

1.  サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** を選択します。  
  
2.  コンソールツリーの  **AD FS**で、**証明書利用者の信頼** をクリックします。 
![ルールの作成](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  選択\-した信頼を右クリックし、 **[要求の発行ポリシーの編集]** をクリックします。
![ルールの作成](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  **[要求発行ポリシーの編集]** ダイアログボックスの **[発行変換規則]** で、 **[規則の追加]** をクリックして規則ウィザードを開始します。 
![ルールの作成](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  **[規則テンプレートの選択]** ページの **[要求規則テンプレート]** で、一覧から **[グループメンバーシップを要求として送信]** を選択し、 **[次へ]** をクリックします。  
![ルールの作成](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group3.PNG)      

6.   **[規則の構成]** ページの **[要求規則名]** に、この規則の表示名を入力し、 **[ユーザーのグループ]** で **[参照]** をクリックしてグループを選択します。 **[出力方向の要求の種類]** で、目的の要求の種類を選択し、[次**へ] をクリックします。出力方向の要求の種類**値を入力します。
![ルールの作成](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group4.PNG)   

7.  **[完了]** ボタンをクリックします。  
  
8.  **[要求規則の編集]** ダイアログボックスで、 **[OK]** をクリックして規則を保存します。
  
## <a name="to-create-a-rule-to-send-group-membership-as-a-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>Windows Server 2016 の要求プロバイダー信頼に対してグループメンバーシップを要求として送信する規則を作成するには 
  
1.  サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** を選択します。  
  
2.  コンソールツリーの  **AD FS**で、**要求プロバイダー信頼** をクリックします。 
![ルールの作成](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  選択\-した信頼を右クリックし、 **[要求規則の編集]** をクリックします。
![ルールの作成](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  **[要求規則の編集]** ダイアログボックスの **[受け入れ変換規則]** で、 **[規則の追加]** をクリックして規則ウィザードを開始します。
![ルールの作成](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  **[規則テンプレートの選択]** ページの **[要求規則テンプレート]** で、一覧から **[グループメンバーシップを要求として送信]** を選択し、 **[次へ]** をクリックします。  
![ルールの作成](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group3.PNG)     

6.   **[規則の構成]** ページの **[要求規則名]** に、この規則の表示名を入力し、 **[ユーザーのグループ]** で **[参照]** をクリックしてグループを選択します。 **[出力方向の要求の種類]** で、目的の要求の種類を選択し、[次**へ] をクリックします。出力方向の要求の種類**値を入力します。 
![ルールの作成](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group4.PNG)      

7.  **[完了]** ボタンをクリックします。  
  
8.  **[要求規則の編集]** ダイアログボックスで、 **[OK]** をクリックして規則を保存します。  




  
## <a name="to-create-a-rule-to-send-group-membership-as-a-claim-in-windows-server-2012-r2"></a>Windows Server 2012 R2 でグループメンバーシップを要求として送信するルールを作成するには 
  
1.  サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** を選択します。  
  
2.  コンソールツリーの [ **\\AD FS の信頼関係**] で、 **[要求プロバイダー信頼]** または **[証明書利用者信頼]** をクリックし、この規則を作成する一覧内の特定の信頼をクリックします。  
  
3.  選択\-した信頼を右クリックし、 **[要求規則の編集]** をクリックします。
![ルールの作成](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)  
  
4.  **[要求規則の編集]** ダイアログボックスで、編集する信頼とこの規則を作成する規則セットに応じて、次のタブのいずれかを選択し、 **[規則の追加]** をクリックして、その規則セットに関連付けられている規則ウィザードを開始します。:  
  
    -   **受け入れ変換規則**  
  
    -   **発行変換規則**  
  
    -   **発行承認規則**  
  
    -   **委任の承認規則**  
![ルールの作成](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)
    
5.  **[規則テンプレートの選択]** ページの **[要求規則テンプレート]** で、 **[グループメンバーシップを要求として送信する]** を一覧から選択し、 **[次へ]** をクリックします。  
![ルールの作成](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group1.PNG)

6.  **[規則の構成]** ページの **[要求規則名]** に、この規則の表示名を入力し、 **[ユーザーのグループ]** で **[参照]** をクリックしてグループを選択します。 **[出力方向の要求の種類]** で、目的の要求の種類を選択し、[次**へ] をクリックします。出力方向の要求の種類**値を入力します。  
![ルールの作成](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group2.PNG)  

7.  **[完了]** をクリックします。  
  
8.  **[要求規則の編集]** ダイアログボックスで、 **[OK]** をクリックして規則を保存します。  



## <a name="additional-references"></a>その他の参照情報 
[要求規則を構成する](Configure-Claim-Rules.md)  
 
[チェックリスト:証明書利用者信頼の要求規則の作成](https://technet.microsoft.com/library/ee913578.aspx)  

[チェックリスト:要求プロバイダー信頼の要求規則の作成](https://technet.microsoft.com/library/ee913564.aspx)  
  
[承認要求規則を使用する場合](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[要求の役割](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[要求規則の役割](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
