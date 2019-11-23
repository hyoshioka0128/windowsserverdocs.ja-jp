---
ms.assetid: 0039fbbb-b981-4526-a550-f3456ff27635
title: 入力方向の要求を変換する規則を作成する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: d4e3a59ff9154a948143cef32103cae9f1f2d235
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407594"
---
# <a name="create-a-rule-to-send-an-ad-fs-1x-compatible-claim"></a>AD FS 1.x と互換性のある要求を送信するルールを作成する

Active Directory フェデレーションサービス (AD FS) \(AD FS\) を使用して AD FS 1.0 \(Windows Server 2003 R2\) または AD FS 1.1 \(Windows server 2008 または Windows Server 2008 R2\)を実行しているフェデレーションサーバーによって受信される要求を発行する場合は、次の操作を行う必要があります。  
  
-   UPN、電子メール、共通名の形式で名前 ID 要求の種類を送信する規則を作成します。  
  
-   送信されるその他のすべての要求には、次のいずれかの種類の要求が含まれている必要があります。  
  
    -   AD FS 1 です。*x*電子メールアドレス  
  
    -   AD FS 1 です。*x* UPN  
  
    -   共通名  
  
    -   グループ  
  
    -   https://schemas.xmlsoap.org/claims/で始まる他の要求の種類 (https://schemas.xmlsoap.org/claims/EmployeeID など)  
  
組織のニーズに応じて、次の手順のいずれかを使用して AD FS 1 を作成します。*x*互換の NameID 要求:  
  
-   このルールを作成して、"**入力方向の要求をパススルーまたはフィルター処理する" 規則テンプレート**を使用して AD FS 1.X 名前 ID 要求を発行します。  
  
-   このルールを作成して、"**入力方向の要求を変換する" 規則テンプレート**を使用して AD FS 1.X 名前 ID 要求を発行します。 この規則テンプレートは、既存の要求の種類を、AD FS 1 で動作する新しい要求の種類に変更する場合に使用できます。 *x*要求。  
  
> [!NOTE]  
> この規則を正しく動作させるには、この規則を作成する場所にある証明書利用者信頼または要求プロバイダー信頼が、 **AD FS 1.0 および1.1 プロファイル**を使用するように構成されていることを確認します。 

## <a name="to-create-a-rule-to-issue-an-adfs1x-name-id-claim-using-the-pass-through-or-filter-an-incoming-claim-rule-template-on-a-relying-party-trust-in-windows-server-2016"></a>AD FS 1 を発行するルールを作成するにはWindows Server 2016 の証明書利用者信頼に対する "入力方向の要求をパススルーまたはフィルター処理する" 規則テンプレートを使用した*x*名前 ID 要求 

1.  サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** を選択します。  
  
2.  コンソールツリーの  **AD FS**で、**証明書利用者の信頼** をクリックします。 
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG) を作成 ![には  
  
3.  選択した信頼を右\-クリックし、 **[要求の発行ポリシーの編集]** をクリックします。
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG) を作成 ![には   
  
4.  **[要求発行ポリシーの編集]** ダイアログボックスの **[発行変換規則]** で、 **[規則の追加]** をクリックして規則ウィザードを開始します。 
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG) を作成 ![には    

5.  **[規則テンプレートの選択]** ページの **[要求規則テンプレート]** で、 **[入力方向の要求をパススルーまたはフィルター処理する]** を選択し、 **[次へ]** をクリックします。  
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG) を作成 ![には    

6.  **[規則の構成]** ページで、要求規則の名前を入力します。  
  
7.  入力 **[方向の要求の種類]** で、一覧から **[名前 ID]** を選択します。  
  
8.  **[受信した名前 ID の形式]** で、次のいずれかの AD FS 1 を選択します。一覧からの*x*\-互換性のある要求形式:  
  
    -   **プリンシパル**  
  
    -   **電子メール\-**  
  
    -   **共通名**  
  
9. 組織のニーズに応じて、次のいずれかのオプションを選択します。  
  
    -   **すべての要求値をパススルーする**  
  
    -   **特定の要求値のみをパススルーする**  
  
    -   **特定の電子メールサフィックスの値に一致する要求値のみをパススルーする**  
  
    -   **特定の値で始まる要求値のみをパススルーする**  
ルール](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs3.PNG) を作成 ![には   

10. **[完了]** をクリックし、 **[OK]** をクリックして規則を保存します。  

  
## <a name="to-create-a-rule-to-issue-an-adfs1x-name-id-claim-using-the-pass-through-or-filter-an-incoming-claim-rule-template-on-a-claims-provider-trust-in-windows-server-2016"></a>AD FS 1 を発行するルールを作成するにはWindows Server 2016 の要求プロバイダー信頼に対する "入力方向の要求をパススルーまたはフィルター処理する" 規則テンプレートを使用した*x*名前 ID 要求 
  
1.  サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** を選択します。  
  
2.  コンソールツリーの  **AD FS**で、**要求プロバイダー信頼** をクリックします。 
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG) を作成 ![には  
  
3.  選択した信頼を右\-クリックし、 **[要求規則の編集]** をクリックします。
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG) を作成 ![には   
  
4.  **[要求規則の編集]** ダイアログボックスの **[受け入れ変換規則]** で、 **[規則の追加]** をクリックして規則ウィザードを開始します。
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG) を作成 ![には    

5.  **[規則テンプレートの選択]** ページの **[要求規則テンプレート]** で、 **[入力方向の要求をパススルーまたはフィルター処理する]** を選択し、 **[次へ]** をクリックします。  
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG) を作成 ![には    

6.  **[規則の構成]** ページで、要求規則の名前を入力します。  
  
7.  入力 **[方向の要求の種類]** で、一覧から **[名前 ID]** を選択します。  
  
8.  **[受信した名前 ID の形式]** で、次のいずれかの AD FS 1 を選択します。一覧からの*x*\-互換性のある要求形式:  
  
    -   **プリンシパル**  
  
    -   **電子メール\-**  
  
    -   **共通名**  
  
9. 組織のニーズに応じて、次のいずれかのオプションを選択します。  
  
    -   **すべての要求値をパススルーする**  
  
    -   **特定の要求値のみをパススルーする**  
  
    -   **特定の電子メールサフィックスの値に一致する要求値のみをパススルーする**  
  
    -   **特定の値で始まる要求値のみをパススルーする**  
ルール](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs3.PNG) を作成 ![には

10. **[完了]** をクリックし、 **[OK]** をクリックして規則を保存します。  


## <a name="to-create-a-rule-to-transform-an-incoming-claim-on-a-relying-party-trust-in-windows-server-2016"></a>Windows Server 2016 で証明書利用者信頼の入力方向の要求を変換する規則を作成するには 

1.  サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** を選択します。  
  
2.  コンソールツリーの  **AD FS**で、**証明書利用者の信頼** をクリックします。 
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG) を作成 ![には  
  
3.  選択した信頼を右\-クリックし、 **[要求の発行ポリシーの編集]** をクリックします。
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG) を作成 ![には
  
4.  **[要求発行ポリシーの編集]** ダイアログボックスの **[発行変換規則]** で、 **[規則の追加]** をクリックして規則ウィザードを開始します。 
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG) を作成 ![には

5.  **[規則テンプレートの選択]** ページの **[要求規則テンプレート]** で、 **[入力方向の要求]** を一覧から変換する を選択し、 **[次へ]** をクリックします。  
ルール](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform3.PNG) を作成 ![には

6.  **[規則の構成]** ページで、要求規則の名前を入力します。  
  
7.  [入力**方向の要求の種類**] で、一覧から変換する入力方向の要求の種類を選択します。  
  
8.  **[出力方向の要求の種類]** で、一覧から **[名前 ID]** を選択します。  
  
9. **[発信名 ID の形式]** で、次のいずれかの AD FS 1 を選択します。一覧からの*x*\-互換性のある要求形式:  
  
    -   **プリンシパル**  
  
    -   **電子メール\-**  
  
    -   **共通名**  
  
10. 組織のニーズに応じて、次のいずれかのオプションを選択します。  
  
    -   **すべての要求値をパススルーする**  
  
    -   **入力方向の要求の値を別の出力方向の要求の値に置き換える**  
  
    -   **受信した電子メールサフィックス要求を新しい電子\-メールサフィックスに置き換える\-**  
ルール](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs4.PNG) を作成 ![には

11. **[完了]** をクリックし、 **[OK]** をクリックして規則を保存します。  

  


## <a name="to-create-a-rule-to-transform-an-incoming-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>Windows Server 2016 で要求プロバイダー信頼の入力方向の要求を変換する規則を作成するには 
  
1.  サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** を選択します。  
  
2.  コンソールツリーの  **AD FS**で、**要求プロバイダー信頼** をクリックします。 
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG) を作成 ![には  
  
3.  選択した信頼を右\-クリックし、 **[要求規則の編集]** をクリックします。
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG) を作成 ![には   
  
4.  **[要求規則の編集]** ダイアログボックスの **[受け入れ変換規則]** で、 **[規則の追加]** をクリックして規則ウィザードを開始します。
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG) を作成 ![には    

5.  **[規則テンプレートの選択]** ページの **[要求規則テンプレート]** で、 **[入力方向の要求]** を一覧から変換する を選択し、 **[次へ]** をクリックします。  
ルール](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform3.PNG) を作成 ![には      

6.  **[規則の構成]** ページで、要求規則の名前を入力します。  
  
7.  [入力**方向の要求の種類**] で、一覧から変換する入力方向の要求の種類を選択します。  
  
8.  **[出力方向の要求の種類]** で、一覧から **[名前 ID]** を選択します。  
  
9. **[発信名 ID の形式]** で、次のいずれかの AD FS 1 を選択します。一覧からの*x*\-互換性のある要求形式:  
  
    -   **プリンシパル**  
  
    -   **電子メール\-**  
  
    -   **共通名**  
  
10. 組織のニーズに応じて、次のいずれかのオプションを選択します。  
  
    -   **すべての要求値をパススルーする**  
  
    -   **入力方向の要求の値を別の出力方向の要求の値に置き換える**  
  
    -   **受信した電子メールサフィックス要求を新しい電子\-メールサフィックスに置き換える\-**  
ルール](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs4.PNG) を作成 ![には    

11. **[完了]** をクリックし、 **[OK]** をクリックして規則を保存します。  













  
## <a name="to-create-a-rule-to-issue-an-adfs1x-name-id-claim-using-the-pass-through-or-filter-an-incoming-claim-rule-template-on-windows-server-2012-r2"></a>AD FS 1 を発行するルールを作成するにはWindows Server 2012 R2 での "入力方向の要求のパススルーまたはフィルター処理" 規則テンプレートを使用した*x*名前 ID 要求
  
1.  サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** をクリックします。  
  
2.  コンソールツリーの [ **AD FS\\の信頼関係**] で、 **[要求プロバイダー信頼]** または **[証明書利用者信頼]** をクリックし、この規則を作成する一覧内の特定の信頼をクリックします。  
  
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
  
6.  **[規則の構成]** ページで、要求規則の名前を入力します。  
  
7.  入力 **[方向の要求の種類]** で、一覧から **[名前 ID]** を選択します。  
  
8.  **[受信した名前 ID の形式]** で、次のいずれかの AD FS 1 を選択します。一覧からの*x*\-互換性のある要求形式:  
  
    -   **プリンシパル**  
  
    -   **電子メール\-**  
  
    -   **共通名**  
  
9. 組織のニーズに応じて、次のいずれかのオプションを選択します。  
  
    -   **すべての要求値をパススルーする**  
  
    -   **特定の要求値のみをパススルーする**  
  
    -   **特定の電子メールサフィックスの値に一致する要求値のみをパススルーする**  
  
    -   **特定の値で始まる要求値のみをパススルーする**  
ルール](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs1.PNG) を作成 ![には

10. **[完了]** をクリックし、 **[OK]** をクリックして規則を保存します。  

  
## <a name="to-create-a-rule-to-issue-an-adfs1x-name-id-claim-using-the-transform-an-incoming-claim-rule-template-in-windows-server-2012-r2"></a>AD FS 1 を発行するルールを作成するにはWindows Server 2012 R2 の "入力方向の要求の変換" 規則テンプレートを使用した*x*名前 ID 要求  
  
1.  サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** をクリックします。  
  
2.  コンソールツリーの [ **AD FS\\の信頼関係**] で、 **[要求プロバイダー信頼]** または **[証明書利用者信頼]** をクリックし、この規則を作成する一覧内の特定の信頼をクリックします。  
  
3.  選択した信頼を右\-クリックし、 **[要求規則の編集]** をクリックします。  
ルール](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG) を作成 ![には 
  
4.  **[要求規則の編集]** ダイアログボックスで、次のいずれかのタブを選択します。このタブは、編集している信頼と、この規則を作成する規則セットによって異なります。次に、 **[規則の追加]** をクリックして、その規則セットに関連付けられている規則ウィザードを開始します。  
  
    -   **受け入れ変換規則**  
  
    -   **発行変換規則**  
  
    -   **発行承認規則**  
  
    -   **委任の承認規則**  
ルール](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG) を作成 ![には
  
5.  **[規則テンプレートの選択]** ページの **[要求規則テンプレート]** で、 **[入力方向の要求]** を一覧から変換する を選択し、 **[次へ]** をクリックします。  
ルール](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform1.PNG) を作成 ![には   
  
6.  **[規則の構成]** ページで、要求規則の名前を入力します。  
  
7.  [入力**方向の要求の種類**] で、一覧から変換する入力方向の要求の種類を選択します。  
  
8.  **[出力方向の要求の種類]** で、一覧から **[名前 ID]** を選択します。  
  
9. **[発信名 ID の形式]** で、次のいずれかの AD FS 1 を選択します。一覧からの*x*\-互換性のある要求形式:  
  
    -   **プリンシパル**  
  
    -   **電子メール\-**  
  
    -   **共通名**  
  
10. 組織のニーズに応じて、次のいずれかのオプションを選択します。  
  
    -   **すべての要求値をパススルーする**  
  
    -   **入力方向の要求の値を別の出力方向の要求の値に置き換える**  
  
    -   **受信した電子メールサフィックス要求を新しい電子\-メールサフィックスに置き換える\-**  
ルール](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs2.PNG) を作成 ![には    

11. **[完了]** をクリックし、 **[OK]** をクリックして規則を保存します。  

## <a name="additional-references"></a>その他の参照情報 
[要求規則を構成する](Configure-Claim-Rules.md)  
 
[チェックリスト: 証明書利用者信頼の要求規則を作成する](https://technet.microsoft.com/library/ee913578.aspx)  

[チェックリスト: 要求プロバイダー信頼の要求規則を作成する](https://technet.microsoft.com/library/ee913564.aspx)  
  
[承認要求規則を使用する場合](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[要求の役割](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[要求規則の役割](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
