---
ms.assetid: 38eb3726-e97b-484e-9926-67e8a046b0c5
title: カスタム規則を使用して要求を送信する規則を作成する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: ade2a8304288d102608c81a0c29155478e5a4b7b
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189433"
---
# <a name="create-a-rule-to-send-claims-using-a-custom-rule"></a>カスタム規則を使用して要求を送信する規則を作成する


使用して、**カスタム規則を使用して要求を送信する**Active Directory フェデレーション サービス (AD FS) のテンプレートは、の要件は、標準的な規則テンプレートに満たしていない場合のカスタム要求規則を作成することができます、組織。 カスタム要求規則は、要求規則言語で記述し、にコピーし、 **Custom rule**規則セットを使用するテキスト ボックス。 高度なルールの構文を構築する方法の詳細については、次を参照してください。[要求規則言語の役割](../../ad-fs/technical-reference/The-Role-of-the-Claim-Rule-Language.md)します。  
  
次の手順を使用するには、AD FS 管理スナップインを使用して要求規則を作成する\-でします。  
  
メンバーシップ**管理者**、またはこの手順を実行する最小要件は、ローカル コンピューターのそれと同等です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。



## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-on-a-relying-party-trust-in-windows-server-2016"></a>パススルーまたは証明書利用者の信頼を Windows Server 2016 での入力方向の要求をフィルター処理するルールを作成するには 

1.  サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  
  
2.  コンソール ツリーで [ **AD FS**、] をクリックして**証明書利用者信頼**します。 
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  右\-選択の信頼をクリックし、クリックして**要求発行ポリシーの編集**します。
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  **要求発行ポリシーの編集**ダイアログ ボックスで、**発行変換規則** をクリックして**規則の追加**ルール ウィザードを開始します。 
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  **規則テンプレートの選択** ページ **要求規則テンプレート**を選択します**カスタム規則を使用して要求を送信する** をクリックし、一覧から **次へ** .  
![ルールを作成します。](media/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule/custom3.PNG)   
  
6.  **規則の構成**] ページ [**要求規則名**、この規則の表示名を入力します。 **Custom rule**を入力するか、このルールに使用する要求規則言語構文貼り付けます。  
![ルールを作成します。](media/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule/custom4.PNG)     

7.  **[Finish]** (完了) をクリックします。  
  
8.  **要求規則の編集**ダイアログ ボックスで、をクリックして **[ok]** ルールを保存します。   
  
## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>パススルーまたは Windows Server 2016 での要求プロバイダー信頼の入力方向の要求をフィルター処理するルールを作成するには 
  
1.  サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  
  
2.  コンソール ツリーで [ **AD FS**、] をクリックして**要求プロバイダー信頼**します。 
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  右\-選択の信頼をクリックし、クリックして**要求規則の編集**します。
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  **要求規則の編集**ダイアログ ボックスで、**受け入れ変換規則** をクリックして**規則の追加**ルール ウィザードを開始します。
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  **規則テンプレートの選択** ページ **要求規則テンプレート**を選択します**カスタム規則を使用して要求を送信する** をクリックし、一覧から **次へ** .  
![ルールを作成します。](media/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule/custom3.PNG)   
  
6.  **規則の構成**] ページ [**要求規則名**、この規則の表示名を入力します。 **Custom rule**を入力するか、このルールに使用する要求規則言語構文貼り付けます。  
![ルールを作成します。](media/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule/custom4.PNG)     

7.  **[Finish]** (完了) をクリックします。  
  
8.  **要求規則の編集**ダイアログ ボックスで、をクリックして **[ok]** ルールを保存します。   

















   
  
## <a name="to-create-a-rule-to-send-claims-by-using-a-custom-claim-in-windows-server-2012-r2"></a>Windows Server 2012 R2 でのカスタム要求を使用して要求を送信するルールを作成するには 
  
1.  サーバー マネージャーで、**ツール**、 をクリックし、 **AD FS 管理**します。  
  
2.  コンソール ツリーで [ **AD FS\\信頼関係**、] をクリックするか**要求プロバイダー信頼**または**証明書利用者信頼**特定の順にクリックしますこのルールを作成するリスト内の信頼します。  
  
3.  右\-選択の信頼をクリックし、クリックして**要求規則の編集**します。  
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG) 
  
4.  **要求規則の編集**信頼関係を編集し、どのルールで設定することに依存する次のタブが、この規則を作成し、クリックをするダイアログ ボックスで、いずれかを選択**規則の追加**ルールを開始するにはその規則セットに関連付けられているウィザード:  
  
    -   **受け入れ変換規則**  
  
    -   **発行変換規則**  
  
    -   **発行承認規則**  
  
    -   **委任承認規則**  
![ルールを作成します。](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)
  
5.  **規則テンプレートの選択** ページ **要求規則テンプレート**を選択します**カスタム規則を使用して要求を送信する** をクリックし、一覧から **次へ** .  
![ルールを作成します。](media/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule/custom1.PNG)   
  
6.  **規則の構成**] ページ [**要求規則名**、この規則の表示名を入力します。 **Custom rule**を入力するか、このルールに使用する要求規則言語構文貼り付けます。  
![ルールを作成します。](media/Create-a-Rule-to-Send-Claims-Using-a-Custom-Rule/custom2.PNG)     

7.  **[Finish]** (完了) をクリックします。  
  
8.  **要求規則の編集**ダイアログ ボックスで、をクリックして **[ok]** ルールを保存します。  

## <a name="additional-references"></a>その他の参照情報 
[要求規則を構成する](Configure-Claim-Rules.md)  
 
[チェックリスト:証明書利用者信頼の要求規則の作成](https://technet.microsoft.com/library/ee913578.aspx)  

[チェックリスト:要求プロバイダー信頼の要求規則の作成](https://technet.microsoft.com/library/ee913564.aspx)  
  
[承認要求規則を使用する場合](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[要求の役割](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[要求規則の役割](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
