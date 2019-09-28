---
ms.assetid: 6127963f-71b2-4d8f-8b53-7c525bf06521
title: 入力方向の要求をパススルーまたはフィルター処理するルールを作成する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 145558e620188c4311d79d2a9ba4ed7aaf7b13a8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358140"
---
# <a name="create-a-rule-to-pass-through-or-filter-an-incoming-claim"></a>入力方向の要求をパススルーまたはフィルター処理するルールを作成する

Active Directory フェデレーションサービス (AD FS) \(AD FS @ no__t-1 で、入力方向の要求をパススルーまたはフィルター処理する規則テンプレートを使用して、選択した要求の種類ですべての入力方向の要求を渡すことができます。 また、選択した要求の種類を使用して、入力方向の要求の値をフィルター処理することもできます。 たとえば、この規則テンプレートを使用して、すべての入力方向のグループ要求を送信する規則を作成できます。 また、この規則を使用すると、ユーザープリンシパル名 \(UPN @ no__t 要求を @fabrikam で終わる要求のみを送信できます。  
  
AD FS 管理スナップイン\-を使用して要求規則を作成するには、次の手順を実行します。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   

## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-on-a-relying-party-trust-in-windows-server-2016"></a>Windows Server 2016 で証明書利用者信頼に対して入力方向の要求をパススルーまたはフィルター処理する規則を作成するには 

1.  サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** を選択します。  
  
2.  コンソールツリーの  **AD FS**で、**証明書利用者の信頼** をクリックします。 
![ルールの作成](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  選択\-した信頼を右クリックし、 **[要求の発行ポリシーの編集]** をクリックします。
![ルールの作成](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  **[要求発行ポリシーの編集]** ダイアログボックスの **[発行変換規則]** で、 **[規則の追加]** をクリックして規則ウィザードを開始します。 
![ルールの作成](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  **[規則テンプレートの選択]** ページの **[要求規則テンプレート]** で、 **[入力方向の要求をパススルーまたはフィルター処理する]** を選択し、 **[次へ]** をクリックします。  
![ルールの作成](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)    

6.  **[規則の構成]** ページの **[要求規則名]** に、この規則の表示名を入力し、入力 **[方向の要求の種類]** ボックスの一覧で要求の種類を選択して、組織のニーズに応じて次のいずれかのオプションを選択します。  
  
    -   **すべての要求値をパススルーする**  
  
    -   **特定の要求値のみをパススルーする**  
  
    -   **特定の電子メールサフィックスの値に一致する要求値のみをパススルーする**  
  
    -   **特定の値で始まる要求値のみをパススルーする**  
![ルールの作成](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule5.PNG)    

7.  **[完了]** ボタンをクリックします。  
  
8.  **[要求規則の編集]** ダイアログボックスで、 **[OK]** をクリックして規則を保存します。
  
## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>Windows Server 2016 の要求プロバイダー信頼に対して入力方向の要求をパススルーまたはフィルター処理する規則を作成するには 
  
1.  サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** を選択します。  
  
2.  コンソールツリーの  **AD FS**で、**要求プロバイダー信頼** をクリックします。 
![ルールの作成](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  選択\-した信頼を右クリックし、 **[要求規則の編集]** をクリックします。
![ルールの作成](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  **[要求規則の編集]** ダイアログボックスの **[受け入れ変換規則]** で、 **[規則の追加]** をクリックして規則ウィザードを開始します。
![ルールの作成](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  **[規則テンプレートの選択]** ページの **[要求規則テンプレート]** で、 **[入力方向の要求をパススルーまたはフィルター処理する]** を選択し、 **[次へ]** をクリックします。  
![ルールの作成](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)    

6.  **[規則の構成]** ページの **[要求規則名]** に、この規則の表示名を入力し、入力 **[方向の要求の種類]** ボックスの一覧で要求の種類を選択して、組織のニーズに応じて次のいずれかのオプションを選択します。  
  
    -   **すべての要求値をパススルーする**  
  
    -   **特定の要求値のみをパススルーする**  
  
    -   **特定の電子メールサフィックスの値に一致する要求値のみをパススルーする**  
  
    -   **特定の値で始まる要求値のみをパススルーする**  
![ルールの作成](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule5.PNG)    

7.  **[完了]** ボタンをクリックします。  
  
8.  **[要求規則の編集]** ダイアログボックスで、 **[OK]** をクリックして規則を保存します。  

## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-in-windows-server-2012-r2"></a>Windows Server 2012 R2 で入力方向の要求をパススルーまたはフィルター処理するルールを作成するには

1.  サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** を選択します。  
  
2.  コンソールツリーの [ **AD\\fsad FS の信頼関係**] で、 **[要求プロバイダー信頼]** または **[証明書利用者信頼]** をクリックし、この規則を作成する一覧内の特定の信頼をクリックします。  
  
3.  選択\-した信頼を右クリックし、 **[要求規則の編集]** をクリックします。
![ルールの作成](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)   
  
4.  **[要求規則の編集]** ダイアログボックスで、編集する信頼とこの規則を作成する規則セットに応じて、次のタブのいずれかを選択し、 **[規則の追加]** をクリックして、その規則セットに関連付けられている規則ウィザードを開始します。:  
  
    -   **受け入れ変換規則**  
  
    -   **発行変換規則**  
  
    -   **発行承認規則**  
  
    -   **委任の承認規則**  
![ルールの作成](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)    

5.  **[規則テンプレートの選択]** ページの **[要求規則テンプレート]** で、 **[入力方向の要求をパススルーまたはフィルター処理する]** を選択し、 **[次へ]** をクリックします。  
![ルールの作成](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule7.PNG)    

6.  **[規則の構成]** ページの **[要求規則名]** に、この規則の表示名を入力し、入力 **[方向の要求の種類]** ボックスの一覧で要求の種類を選択して、組織のニーズに応じて次のいずれかのオプションを選択します。  
  
    -   **すべての要求値をパススルーする**  
  
    -   **特定の要求値のみをパススルーする**  
  
    -   **特定の電子メールサフィックスの値に一致する要求値のみをパススルーする**  
  
    -   **特定の値で始まる要求値のみをパススルーする**  
![ルールの作成](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule8.PNG)    

7.  **[完了]** ボタンをクリックします。  
  
8.  **[要求規則の編集]** ダイアログボックスで、 **[OK]** をクリックして規則を保存します。  



  
## <a name="additional-references"></a>その他の参照情報  
[要求規則を構成する](Configure-Claim-Rules.md)  
  
[パススルーまたはフィルター要求規則を使用する場合](../../ad-fs/technical-reference/When-to-Use-a-Pass-Through-or-Filter-Claim-Rule.md)  
  
[要求の役割](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[要求規則の役割](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
  
