---
ms.assetid: 6127963f-71b2-4d8f-8b53-7c525bf06521
title: パススルーまたは入力方向の要求をフィルター処理するルールを作成します。
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 50f50cd4e096b107a2b58ac05328ff8ed413f2dc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860273"
---
# <a name="create-a-rule-to-pass-through-or-filter-an-incoming-claim"></a>パススルーまたは入力方向の要求をフィルター処理するルールを作成します。

>適用先:Windows Server 2016、Windows Server 2012 R2

パススルーを使用して、Active Directory フェデレーション サービスで、入力方向の要求規則テンプレートをフィルター処理または\(AD FS\)、選択したクレームの種類ですべての着信要求を渡すことができます。 入力方向の要求の値は、選択したクレームの種類でフィルターすることもできます。 たとえば、この規則テンプレートを使用して、グループのすべての着信要求を送信するルールを作成することができます。 ユーザー プリンシパル名のみを送信するこのルールを使用することもできます。 \(UPN\)で終わる要求@fabrikamします。  
  
次の手順を使用するには、AD FS 管理スナップインで要求規則を作成する\-でします。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   

## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-on-a-relying-party-trust-in-windows-server-2016"></a>パススルーまたは証明書利用者の信頼を Windows Server 2016 での入力方向の要求をフィルター処理するルールを作成するには 

1.  サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  
  
2.  コンソール ツリーで [ **AD FS**、] をクリックして**証明書利用者信頼**します。 
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  右\-選択の信頼をクリックし、クリックして**要求発行ポリシーの編集**します。
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  **要求発行ポリシーの編集**ダイアログ ボックスで、**発行変換規則** をクリックして**規則の追加**ルール ウィザードを開始します。 
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  **規則テンプレートの選択** ページ **要求規則テンプレート**を選択します**パススルーまたはフィルター処理の入力方向の要求** をクリックし、一覧から**次へ**.  
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)    

6.  **規則の構成**ページ**要求規則名**で、この規則の表示名を入力**着信要求の種類**一覧で、要求の種類を選択しのいずれかを選択します次のオプションを組織のニーズによって異なります。  
  
    -   **すべての要求値をパススルーします。**  
  
    -   **特定の要求値のみをパススルーします。**  
  
    -   **特定の電子メール サフィックスの値に一致する要求値のみをパススルーします。**  
  
    -   **特定の値で始まる要求値のみをパススルーします。**  
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule5.PNG)    

7.  をクリックして、**完了**ボタンをクリックします。  
  
8.  **要求規則の編集**ダイアログ ボックスで、をクリックして **[ok]** ルールを保存します。
  
## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>パススルーまたは Windows Server 2016 での要求プロバイダー信頼の入力方向の要求をフィルター処理するルールを作成するには 
  
1.  サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  
  
2.  コンソール ツリーで [ **AD FS**、] をクリックして**要求プロバイダー信頼**します。 
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  右\-選択の信頼をクリックし、クリックして**要求規則の編集**します。
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  **要求規則の編集**ダイアログ ボックスで、**受け入れ変換規則** をクリックして**規則の追加**ルール ウィザードを開始します。
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  **規則テンプレートの選択** ページ **要求規則テンプレート**を選択します**パススルーまたはフィルター処理の入力方向の要求** をクリックし、一覧から**次へ**.  
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)    

6.  **規則の構成**ページ**要求規則名**で、この規則の表示名を入力**着信要求の種類**一覧で、要求の種類を選択しのいずれかを選択します次のオプションを組織のニーズによって異なります。  
  
    -   **すべての要求値をパススルーします。**  
  
    -   **特定の要求値のみをパススルーします。**  
  
    -   **特定の電子メール サフィックスの値に一致する要求値のみをパススルーします。**  
  
    -   **特定の値で始まる要求値のみをパススルーします。**  
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule5.PNG)    

7.  をクリックして、**完了**ボタンをクリックします。  
  
8.  **要求規則の編集**ダイアログ ボックスで、をクリックして **[ok]** ルールを保存します。  

## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-in-windows-server-2012-r2"></a>パススルーまたは Windows Server 2012 R2 での入力方向の要求をフィルター処理するルールを作成するには

1.  サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  
  
2.  コンソール ツリーで [ **AD FSAD FS\\信頼関係**、いずれかをクリックします**要求プロバイダー信頼**または**証明書利用者信頼**、] をクリックし、このルールを作成する一覧で特定の信頼します。  
  
3.  右\-選択の信頼をクリックし、クリックして**要求規則の編集**します。
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)   
  
4.  **要求規則の編集**ダイアログ ボックスで、1 つに、次のタブを選択、信頼関係を編集して、ルール セットによって、この規則を作成して順にクリックします**規則の追加**ルール ウィザードを起動するにはその規則セットに関連付けられています。  
  
    -   **受け入れ変換規則**  
  
    -   **発行変換規則**  
  
    -   **発行承認規則**  
  
    -   **委任承認規則**  
![ルールを作成します。](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)    

5.  **規則テンプレートの選択** ページ **要求規則テンプレート**を選択します**パススルーまたはフィルター処理の入力方向の要求** をクリックし、一覧から**次へ**.  
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule7.PNG)    

6.  **規則の構成**ページ**要求規則名**で、この規則の表示名を入力**着信要求の種類**一覧で、要求の種類を選択しのいずれかを選択します次のオプションを組織のニーズによって異なります。  
  
    -   **すべての要求値をパススルーします。**  
  
    -   **特定の要求値のみをパススルーします。**  
  
    -   **特定の電子メール サフィックスの値に一致する要求値のみをパススルーします。**  
  
    -   **特定の値で始まる要求値のみをパススルーします。**  
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule8.PNG)    

7.  をクリックして、**完了**ボタンをクリックします。  
  
8.  **要求規則の編集**ダイアログ ボックスで、をクリックして **[ok]** ルールを保存します。  



  
## <a name="additional-references"></a>その他の参照情報  
[要求規則を構成します。](Configure-Claim-Rules.md)  
  
[パススルーを使用する場合、or Filter Claim Rule](../../ad-fs/technical-reference/When-to-Use-a-Pass-Through-or-Filter-Claim-Rule.md)  
  
[要求の役割](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[要求規則の役割](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
  
