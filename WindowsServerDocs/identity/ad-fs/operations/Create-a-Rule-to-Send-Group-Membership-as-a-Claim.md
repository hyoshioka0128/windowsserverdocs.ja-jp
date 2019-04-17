---
ms.assetid: 475e34f9-9399-43f4-a840-9dd77258e11a
title: "要求として送信グループのメンバーシップの規則を作成します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: d4fb03de9de2dcca36b18ce089db11ed599de820
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-rule-to-send-group-membership-as-a-claim"></a>要求として送信グループのメンバーシップの規則を作成します。

>適用対象: Windows Server 2016、Windows Server 2012 R2

Active Directory フェデレーション サービス \(AD FS\) で要求規則テンプレートとして使用し、[グループのメンバーシップの送信が可能にすることを要求として送信する Active Directory セキュリティ グループを選択するためのルールを作成できます。 このルールは、選択したグループに基づいてから 1 つの要求のみが表示されます。 たとえば、この規則テンプレートを使用して、ユーザーが Domain Admins セキュリティ グループのメンバーである場合、管理者の値を持つグループの要求を送信する規則を作成することができます。 このルールは、ローカルの Active Directory ドメインのユーザーに対してのみ使用する必要があります。  
  
次の手順を使用するには、AD FS 管理スナップインの要求規則の作成をします。  
  
メンバーシップ**管理者**、相当するもので、ローカル コンピューターでは、この手順を完了するために必要な最低限またはします。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   

## <a name="to-create-a-rule-to-send-group-membership-as-a-claim-on-a-relying-party-trust-in-windows-server-2016"></a>グループのメンバーシップを a Relying Party Trust Windows Server 2016 での要求として送信する規則を作成するには 

1.  サーバー マネージャーで、クリックして**ツール**、し、[ **AD FS 管理**します。  
  
2.  コンソール ツリーで、[ **AD FS**、] をクリックして**証明書利用者信頼**します。 
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  選択した信頼を右クリックし、クリック**要求発行ポリシーの編集**します。
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  **要求発行ポリシーの編集**ダイアログ ボックスで、**発行変換規則**] をクリックして**規則の追加**規則ウィザードを開始します。 
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  **規則テンプレートの選択**ページで、**要求規則テンプレート**[**グループ メンバーシップを要求として送信**クリックして、一覧から**[次へ]**します。  
![規則を作成します。](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group3.PNG)      

6.   **規則の構成**] ページの [**要求規則名**でこの規則の表示名を入力**ユーザーのグループ**] をクリックして**参照**下にあるグループを選択して**出力方向の要求の種類**必要な要求の種類を選択し、**出力方向の要求の種類**値を入力します。
![規則を作成します。](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group4.PNG)   

7.  をクリックして、**完了**ボタンをクリックします。  
  
8.  **要求規則の編集**ダイアログ ボックスで、] をクリックして**OK**に規則を保存します。
  
## <a name="to-create-a-rule-to-to-send-group-membership-as-a-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>グループのメンバーシップを Windows Server 2016 での要求プロバイダー信頼の要求として送信する規則を作成するには 
  
1.  サーバー マネージャーで、クリックして**ツール**、し、[ **AD FS 管理**します。  
  
2.  コンソール ツリーで、[ **AD FS**、] をクリックして**要求プロバイダー信頼**します。 
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  選択した信頼を右クリックし、クリック**要求規則の編集**します。
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  **要求規則の編集**ダイアログ ボックスで、**受け付け変換規則**] をクリックして**規則の追加**規則ウィザードを開始します。
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  **規則テンプレートの選択**ページで、**要求規則テンプレート**[**グループ メンバーシップを要求として送信**クリックして、一覧から**[次へ]**します。  
![規則を作成します。](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group3.PNG)     

6.   **規則の構成**] ページの [**要求規則名**でこの規則の表示名を入力**ユーザーのグループ**] をクリックして**参照**下にあるグループを選択して**出力方向の要求の種類**必要な要求の種類を選択し、**出力方向の要求の種類**値を入力します。 
![規則を作成します。](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group4.PNG)      

7.  をクリックして、**完了**ボタンをクリックします。  
  
8.  **要求規則の編集**ダイアログ ボックスで、] をクリックして**OK**に規則を保存します。  




  
## <a name="to-create-a-rule-to-send-group-membership-as-a-claim-in-windows-server-2012-r2"></a>グループのメンバーシップを Windows Server 2012 R2 での要求として送信する規則を作成するには 
  
1.  サーバー マネージャーで、クリックして**ツール**、し、[ **AD FS 管理**します。  
  
2.  コンソール ツリーで、下にある**AD FS\\Trust 関係**、] をクリックするか**要求プロバイダー信頼**または**証明書利用者信頼**、この規則を作成するリスト内の特定の信頼をクリックします。  
  
3.  選択した信頼を右クリックし、クリック**要求規則の編集**します。
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)  
  
4.  **要求規則の編集**ダイアログ ボックスで、1 つに、次のタブを選択、信頼関係を編集しているし、どの規則を設定することによって、この規則の作成にして] をクリックして**規則の追加**するルール セットに関連付けられている規則のウィザードを開始します。  
  
    -   **受け入れ変換規則**  
  
    -   **発行変換規則**  
  
    -   **発行承認規則**  
  
    -   **委任承認規則**  
![規則を作成します。](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)
    
5.  **規則テンプレートの選択**ページで、**要求規則テンプレート**[**グループ メンバーシップを要求として送信**クリックして、一覧から**[次へ]**します。  
![規則を作成します。](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group1.PNG)

6.  **規則の構成**] ページの [**要求規則名**でこの規則の表示名を入力**ユーザーのグループ**] をクリックして**参照**下にあるグループを選択して**出力方向の要求の種類**必要な要求の種類を選択し、**出力方向の要求の種類**値を入力します。  
![規則を作成します。](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group2.PNG)  

7.  をクリックして**完了**します。  
  
8.  **要求規則の編集**ダイアログ ボックスで、] をクリックして**OK**に規則を保存します。  



## <a name="additional-references"></a>その他の参照 
[要求規則を構成します。](Configure-Claim-Rules.md)  
 
[チェックリスト: 証明書利用者のパーティ信頼の要求規則を作成します。](https://technet.microsoft.com/library/ee913578.aspx)  

[チェックリスト: Creating Claim Rules for 要求プロバイダー信頼します。](https://technet.microsoft.com/library/ee913564.aspx)  
  
[When to Use an Authorization Claim Rule](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[要求の役割](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[要求規則の役割](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
