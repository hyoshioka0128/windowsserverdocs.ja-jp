---
ms.assetid: 475e34f9-9399-43f4-a840-9dd77258e11a
title: グループ メンバーシップを要求として送信する規則を作成する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: c9c4cdb881d77fe902776551b4e99061e67660ea
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189383"
---
# <a name="create-a-rule-to-send-group-membership-as-a-claim"></a>グループ メンバーシップを要求として送信する規則を作成する

Active Directory フェデレーション サービスで要求規則テンプレートとして送信グループ メンバーシップを使用して\(AD FS\)、要求として送信する Active Directory セキュリティ グループを選択することを可能にするためのルールを作成することができます。 このルールは、選択したグループに基づくから 1 つの要求のみが表示されます。 たとえば、この規則テンプレートを使用すると、ユーザーが Domain Admins セキュリティ グループのメンバーである場合に管理者の値を持つグループの要求を送信するルールを作成します。 このルールは、ローカルの Active Directory ドメインのユーザーに対してのみ使用する必要があります。  
  
次の手順を使用するには、AD FS 管理スナップインで要求規則を作成する\-でします。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   

## <a name="to-create-a-rule-to-send-group-membership-as-a-claim-on-a-relying-party-trust-in-windows-server-2016"></a>グループのメンバーシップを証明書利用者の信頼を Windows Server 2016 での要求として送信するルールを作成するには 

1.  サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  
  
2.  コンソール ツリーで [ **AD FS**、] をクリックして**証明書利用者信頼**します。 
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  右\-選択の信頼をクリックし、クリックして**要求発行ポリシーの編集**します。
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  **要求発行ポリシーの編集**ダイアログ ボックスで、**発行変換規則** をクリックして**規則の追加**ルール ウィザードを開始します。 
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  **規則テンプレートの選択** ページ **要求規則テンプレート**を選択します**グループ メンバーシップを要求として送信** をクリックし、一覧から **次へ** .  
![ルールを作成します。](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group3.PNG)      

6.   **規則の構成**ページで**要求規則名**で、この規則の表示名を入力**ユーザーのグループ**クリックして**参照**を選択し、グループの下で**出力方向の要求の種類**目的のクレームの種類を選択し、**出力方向の要求の種類**値を入力します。
![ルールを作成します。](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group4.PNG)   

7.  をクリックして、**完了**ボタンをクリックします。  
  
8.  **要求規則の編集**ダイアログ ボックスで、をクリックして **[ok]** ルールを保存します。
  
## <a name="to-create-a-rule-to-send-group-membership-as-a-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>Windows Server 2016 での要求プロバイダー信頼のクレームとしてグループのメンバーシップを送信するルールを作成するには 
  
1.  サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  
  
2.  コンソール ツリーで [ **AD FS**、] をクリックして**要求プロバイダー信頼**します。 
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  右\-選択の信頼をクリックし、クリックして**要求規則の編集**します。
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  **要求規則の編集**ダイアログ ボックスで、**受け入れ変換規則** をクリックして**規則の追加**ルール ウィザードを開始します。
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  **規則テンプレートの選択** ページ **要求規則テンプレート**を選択します**グループ メンバーシップを要求として送信** をクリックし、一覧から **次へ** .  
![ルールを作成します。](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group3.PNG)     

6.   **規則の構成**ページで**要求規則名**で、この規則の表示名を入力**ユーザーのグループ**クリックして**参照**を選択し、グループの下で**出力方向の要求の種類**目的のクレームの種類を選択し、**出力方向の要求の種類**値を入力します。 
![ルールを作成します。](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group4.PNG)      

7.  をクリックして、**完了**ボタンをクリックします。  
  
8.  **要求規則の編集**ダイアログ ボックスで、をクリックして **[ok]** ルールを保存します。  




  
## <a name="to-create-a-rule-to-send-group-membership-as-a-claim-in-windows-server-2012-r2"></a>グループのメンバーシップを Windows Server 2012 R2 で要求として送信するルールを作成するには 
  
1.  サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  
  
2.  コンソール ツリーで [ **AD FS\\信頼関係**、] をクリックするか**要求プロバイダー信頼**または**証明書利用者信頼**特定の順にクリックしますこのルールを作成するリスト内の信頼します。  
  
3.  右\-選択の信頼をクリックし、クリックして**要求規則の編集**します。
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)  
  
4.  **要求規則の編集**ダイアログ ボックスで、1 つに、次のタブを選択、信頼関係を編集して、どのルールを設定することによって、この規則を作成して順にクリックします**規則の追加**ルールを開始するにはその規則セットに関連付けられているウィザード:  
  
    -   **受け入れ変換規則**  
  
    -   **発行変換規則**  
  
    -   **発行承認規則**  
  
    -   **委任承認規則**  
![ルールを作成します。](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)
    
5.  **規則テンプレートの選択** ページ **要求規則テンプレート**を選択します**グループ メンバーシップを要求として送信** をクリックし、一覧から **次へ** .  
![ルールを作成します。](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group1.PNG)

6.  **規則の構成**ページで**要求規則名**で、この規則の表示名を入力**ユーザーのグループ**クリックして**参照**を選択し、グループの下で**出力方向の要求の種類**目的のクレームの種類を選択し、**出力方向の要求の種類**値を入力します。  
![ルールを作成します。](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group2.PNG)  

7.  **[Finish]** (完了) をクリックします。  
  
8.  **要求規則の編集**ダイアログ ボックスで、をクリックして **[ok]** ルールを保存します。  



## <a name="additional-references"></a>その他の参照情報 
[要求規則を構成する](Configure-Claim-Rules.md)  
 
[チェックリスト:証明書利用者信頼の要求規則の作成](https://technet.microsoft.com/library/ee913578.aspx)  

[チェックリスト:要求プロバイダー信頼の要求規則の作成](https://technet.microsoft.com/library/ee913564.aspx)  
  
[承認要求規則を使用する場合](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[要求の役割](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[要求規則の役割](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
