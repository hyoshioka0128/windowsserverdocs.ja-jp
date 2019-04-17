---
ms.assetid: 6127963f-71b2-4d8f-8b53-7c525bf06521
title: "パススルーまたは入力方向の要求をフィルター処理する規則を作成します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 50f50cd4e096b107a2b58ac05328ff8ed413f2dc
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-rule-to-pass-through-or-filter-an-incoming-claim"></a>パススルーまたは入力方向の要求をフィルター処理する規則を作成します。

>適用対象: Windows Server 2016、Windows Server 2012 R2

Active Directory フェデレーション サービス \(AD FS\) のパススルーまたはフィルター処理、入力方向の要求規則テンプレートを使用すると、選択された要求種類のすべての着信要求を渡すことができます。 入力方向の要求の値をフィルター処理、選択した要求の種類とこともできます。 たとえば、この規則テンプレートを使用して、入力方向のすべてのグループ要求を送信する規則を作成することができます。 要求を送信するのみのユーザー プリンシパル名 \(UPN\) 末尾に、この規則を使用することもできます@fabrikamします。  
  
次の手順を使用するには、AD FS 管理スナップインの要求規則の作成をします。  
  
メンバーシップ**管理者**、相当するもので、ローカル コンピューターでは、この手順を完了するために必要な最低限またはします。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   

## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-on-a-relying-party-trust-in-windows-server-2016"></a>パススルーまたは a Relying Party Trust Windows Server 2016 での入力方向の要求をフィルター処理する規則を作成するには 

1.  サーバー マネージャーで、クリックして**ツール**、し、[ **AD FS 管理**します。  
  
2.  コンソール ツリーで、[ **AD FS**、] をクリックして**証明書利用者信頼**します。 
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  選択した信頼を右クリックし、クリック**要求発行ポリシーの編集**します。
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  **要求発行ポリシーの編集**ダイアログ ボックスで、**発行変換規則**] をクリックして**規則の追加**規則ウィザードを開始します。 
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  **規則テンプレートの選択**ページで、**要求規則テンプレート**[**パススルーまたはフィルター処理入力方向の要求**クリックして、一覧から**[次へ]**します。  
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)    

6.  **規則の構成**] ページの [**要求規則名**でこの規則の表示名を入力**入力方向の要求の種類**一覧で、要求の種類を選択し、組織のニーズに応じて、次のオプションのいずれかを選択します。  
  
    -   **すべての要求の値をパススルーします。**  
  
    -   **特定の要求値のみをパススルーします。**  
  
    -   **特定の電子メール サフィックスの値に一致する要求値のみをパススルーします。**  
  
    -   **特定の値で始まる要求値のみをパススルーします。**  
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule5.PNG)    

7.  をクリックして、**完了**ボタンをクリックします。  
  
8.  **要求規則の編集**ダイアログ ボックスで、] をクリックして**OK**に規則を保存します。
  
## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>パススルーまたは Windows Server 2016 での要求プロバイダー信頼の入力方向の要求をフィルター処理する規則を作成するには 
  
1.  サーバー マネージャーで、クリックして**ツール**、し、[ **AD FS 管理**します。  
  
2.  コンソール ツリーで、[ **AD FS**、] をクリックして**要求プロバイダー信頼**します。 
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  選択した信頼を右クリックし、クリック**要求規則の編集**します。
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  **要求規則の編集**ダイアログ ボックスで、**受け付け変換規則**] をクリックして**規則の追加**規則ウィザードを開始します。
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  **規則テンプレートの選択**ページで、**要求規則テンプレート**[**パススルーまたはフィルター処理入力方向の要求**クリックして、一覧から**[次へ]**します。  
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)    

6.  **規則の構成**] ページの [**要求規則名**でこの規則の表示名を入力**入力方向の要求の種類**一覧で、要求の種類を選択し、組織のニーズに応じて、次のオプションのいずれかを選択します。  
  
    -   **すべての要求の値をパススルーします。**  
  
    -   **特定の要求値のみをパススルーします。**  
  
    -   **特定の電子メール サフィックスの値に一致する要求値のみをパススルーします。**  
  
    -   **特定の値で始まる要求値のみをパススルーします。**  
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule5.PNG)    

7.  をクリックして、**完了**ボタンをクリックします。  
  
8.  **要求規則の編集**ダイアログ ボックスで、] をクリックして**OK**に規則を保存します。  

## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-in-windows-server-2012-r2"></a>パススルーまたは Windows Server 2012 R2 での入力方向の要求をフィルター処理する規則を作成するには

1.  サーバー マネージャーで、クリックして**ツール**、し、[ **AD FS 管理**します。  
  
2.  コンソール ツリーで、下にある**AD FSAD FS\\Trust 関係**、] をクリックするか**要求プロバイダー信頼**または**証明書利用者信頼**、この規則を作成するリスト内の特定の信頼をクリックします。  
  
3.  選択した信頼を右クリックし、クリック**要求規則の編集**します。
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)   
  
4.  **要求規則の編集**] ダイアログ ボックスで、次のタブを 1 つを選択に応じてを編集しているし、どの規則を設定する信頼するのには、この規則を作成し、[クリックして**規則の追加**するルール セットに関連付けられている規則のウィザードを開始します。  
  
    -   **受け入れ変換規則**  
  
    -   **発行変換規則**  
  
    -   **発行承認規則**  
  
    -   **委任承認規則**  
![規則を作成します。](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)    

5.  **規則テンプレートの選択**ページで、**要求規則テンプレート**[**パススルーまたはフィルター処理入力方向の要求**クリックして、一覧から**[次へ]**します。  
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule7.PNG)    

6.  **規則の構成**] ページの [**要求規則名**でこの規則の表示名を入力**入力方向の要求の種類**一覧で、要求の種類を選択し、組織のニーズに応じて、次のオプションのいずれかを選択します。  
  
    -   **すべての要求の値をパススルーします。**  
  
    -   **特定の要求値のみをパススルーします。**  
  
    -   **特定の電子メール サフィックスの値に一致する要求値のみをパススルーします。**  
  
    -   **特定の値で始まる要求値のみをパススルーします。**  
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule8.PNG)    

7.  をクリックして、**完了**ボタンをクリックします。  
  
8.  **要求規則の編集**ダイアログ ボックスで、] をクリックして**OK**に規則を保存します。  



  
## <a name="additional-references"></a>その他の参照  
[要求規則を構成します。](Configure-Claim-Rules.md)  
  
[パススルーを使用する場合、or Filter Claim Rule](../../ad-fs/technical-reference/When-to-Use-a-Pass-Through-or-Filter-Claim-Rule.md)  
  
[要求の役割](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[要求規則の役割](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
  
