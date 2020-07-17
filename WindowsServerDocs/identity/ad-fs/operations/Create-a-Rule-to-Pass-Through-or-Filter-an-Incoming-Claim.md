---
ms.assetid: 6127963f-71b2-4d8f-8b53-7c525bf06521
title: 入力方向の要求をパススルーまたはフィルター処理するルールを作成する
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: fb885d8b822faf4bd5ee82ad70c59b99678a58e9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816835"
---
# <a name="create-a-rule-to-pass-through-or-filter-an-incoming-claim"></a>入力方向の要求をパススルーまたはフィルター処理するルールを作成する

Active Directory フェデレーションサービス (AD FS) \(AD FS\)の [入力方向の要求をパススルーまたはフィルター処理する] 規則テンプレートを使用して、選択した要求の種類ですべての入力方向の要求を渡すことができます。 また、選択された要求の種類の入力方向の要求値をフィルターすることもできます。 たとえば、この規則テンプレートを使用して、入力方向のすべてのグループ要求を送信する規則を作成できます。 また、この規則を使用すると、@fabrikamで終わる要求\) UPN \(UPN のみを送信できます。  
  
で AD FS 管理スナップ\-を使用して要求規則を作成するには、次の手順を実行します。  
  
この手順を完了するには、ローカル コンピューター上の **Administrators** または同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   

## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-on-a-relying-party-trust-in-windows-server-2016"></a>Windows Server 2016 で証明書利用者信頼に対して入力方向の要求をパススルーまたはフィルター処理する規則を作成するには 

1.  サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** を選択します。  
  
2.  コンソールツリーの  **AD FS**で、**証明書利用者の信頼** をクリックします。 
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG) を作成 ![には  
  
3.  選択した信頼を右\-クリックし、 **[要求の発行ポリシーの編集]** をクリックします。
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG) を作成 ![には   
  
4.  **[要求発行ポリシーの編集]** ダイアログボックスの **[発行変換規則]** で、 **[規則の追加]** をクリックして規則ウィザードを開始します。 
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG) を作成 ![には    

5.  **[規則テンプレートの選択]** ページの **[要求規則テンプレート]** で、 **[入力方向の要求をパススルーまたはフィルター処理する]** を選択し、 **[次へ]** をクリックします。  
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG) を作成 ![には    

6.  **[規則の構成]** ページの **[要求規則名]** に、この規則の表示名を入力し、入力 **[方向の要求の種類]** ボックスの一覧で要求の種類を選択して、組織のニーズに応じて次のいずれかのオプションを選択します。  
  
    -   **すべての要求値をパススルーする**  
  
    -   **特定の要求値のみをパススルーする**  
  
    -   **特定の電子メールサフィックスの値に一致する要求値のみをパススルーする**  
  
    -   **特定の値で始まる要求値のみをパススルーする**  
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule5.PNG) を作成 ![には    

7.  **[完了]** ボタンをクリックします。  
  
8.  **[要求規則の編集]** ダイアログボックスで、 **[OK]** をクリックして規則を保存します。
  
## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>Windows Server 2016 の要求プロバイダー信頼に対して入力方向の要求をパススルーまたはフィルター処理する規則を作成するには 
  
1.  サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** を選択します。  
  
2.  コンソールツリーの  **AD FS**で、**要求プロバイダー信頼** をクリックします。 
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG) を作成 ![には  
  
3.  選択した信頼を右\-クリックし、 **[要求規則の編集]** をクリックします。
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG) を作成 ![には   
  
4.  **[要求規則の編集]** ダイアログボックスの **[受け入れ変換規則]** で、 **[規則の追加]** をクリックして規則ウィザードを開始します。
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG) を作成 ![には    

5.  **[規則テンプレートの選択]** ページの **[要求規則テンプレート]** で、 **[入力方向の要求をパススルーまたはフィルター処理する]** を選択し、 **[次へ]** をクリックします。  
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG) を作成 ![には    

6.  **[規則の構成]** ページの **[要求規則名]** に、この規則の表示名を入力し、入力 **[方向の要求の種類]** ボックスの一覧で要求の種類を選択して、組織のニーズに応じて次のいずれかのオプションを選択します。  
  
    -   **すべての要求値をパススルーする**  
  
    -   **特定の要求値のみをパススルーする**  
  
    -   **特定の電子メールサフィックスの値に一致する要求値のみをパススルーする**  
  
    -   **特定の値で始まる要求値のみをパススルーする**  
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule5.PNG) を作成 ![には    

7.  **[完了]** ボタンをクリックします。  
  
8.  **[要求規則の編集]** ダイアログボックスで、 **[OK]** をクリックして規則を保存します。  

## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-in-windows-server-2012-r2"></a>Windows Server 2012 R2 で入力方向の要求をパススルーまたはフィルター処理するルールを作成するには

1.  サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** を選択します。  
  
2.  コンソールツリーの [ **AD FSAD FS\\信頼関係**] で、 **[要求プロバイダー信頼]** または **[証明書利用者信頼]** をクリックし、この規則を作成する一覧内の特定の信頼をクリックします。  
  
3.  選択した信頼を右\-クリックし、 **[要求規則の編集]** をクリックします。
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG) を作成 ![には   
  
4.  **[要求規則の編集]** ダイアログボックスで、編集する信頼とこの規則を作成する規則セットに応じて、次のタブのいずれかを選択し、 **[規則の追加]** をクリックして、その規則セットに関連付けられている規則ウィザードを開始します。  
  
    -   **受け入れ変換規則**  
  
    -   **発行変換規則**  
  
    -   **発行承認規則**  
  
    -   **委任の承認規則**  
ルール](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG) を作成 ![には    

5.  **[規則テンプレートの選択]** ページの **[要求規則テンプレート]** で、 **[入力方向の要求をパススルーまたはフィルター処理する]** を選択し、 **[次へ]** をクリックします。  
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule7.PNG) を作成 ![には    

6.  **[規則の構成]** ページの **[要求規則名]** に、この規則の表示名を入力し、入力 **[方向の要求の種類]** ボックスの一覧で要求の種類を選択して、組織のニーズに応じて次のいずれかのオプションを選択します。  
  
    -   **すべての要求値をパススルーする**  
  
    -   **特定の要求値のみをパススルーする**  
  
    -   **特定の電子メールサフィックスの値に一致する要求値のみをパススルーする**  
  
    -   **特定の値で始まる要求値のみをパススルーする**  
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule8.PNG) を作成 ![には    

7.  **[完了]** ボタンをクリックします。  
  
8.  **[要求規則の編集]** ダイアログボックスで、 **[OK]** をクリックして規則を保存します。  



  
## <a name="additional-references"></a>その他の参照情報  
[要求規則を構成する](Configure-Claim-Rules.md)  
  
[パススルーまたはフィルター要求規則を使用する場合](../../ad-fs/technical-reference/When-to-Use-a-Pass-Through-or-Filter-Claim-Rule.md)  
  
[要求の役割](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[要求規則の役割](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
  
