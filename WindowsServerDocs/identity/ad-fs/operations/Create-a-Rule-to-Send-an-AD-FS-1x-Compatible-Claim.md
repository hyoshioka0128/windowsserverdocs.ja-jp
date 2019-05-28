---
ms.assetid: 0039fbbb-b981-4526-a550-f3456ff27635
title: 入力方向の要求を変換する規則を作成する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: c87b76224d1ac5dbe3befc837fad8879d0b9a1ef
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189402"
---
# <a name="create-a-rule-to-send-an-ad-fs-1x-compatible-claim"></a>AD FS 1.x の互換性のある要求を送信するルールを作成します。

Active Directory フェデレーション サービスを使用している状況で\(AD FS\) AD FS 1.0 を実行しているフェデレーション サーバーによって受信する要求を問題に\(Windows Server 2003 R2\)または AD FS 1.1 \(Windows Server 2008 または Windows Server 2008 R2\)次を行う必要があります。  
  
-   UPN、電子メール、または共通名の形式名 ID クレームの種類を送信するルールを作成します。  
  
-   送信されるその他のすべての要求は、次の要求の種類のいずれかが必要です。  
  
    -   AD FS 1。*x*電子メール アドレス  
  
    -   AD FS 1。*x* UPN  
  
    -   共通名  
  
    -   グループ  
  
    -   始まるその他の要求種類 https://schemas.xmlsoap.org/claims/など https://schemas.xmlsoap.org/claims/EmployeeID  
  
、組織のニーズに応じて、AD FS 1 を作成するのに手順は次のいずれかを使用します。*x*互換の NameID 要求。  
  
-   問題、AD FS 1.x 名前 ID 要求を使用するには、この規則を作成、**パススルーまたはフィルター処理する入力方向の要求規則テンプレート**  
  
-   問題、AD FS 1.x 名前 ID 要求を使用するには、この規則を作成、 **、入力方向の要求規則テンプレートを変換**します。 AD FS 1 で動作する新しいクレームの種類に既存の要求の種類を変更する場合にこの規則テンプレートを使用することができます。 *x*要求。  
  
> [!NOTE]  
> 期待どおりに動作するには、この規則のことを証明書利用者の信頼またはこのルールを作成する要求プロバイダー信頼が使用する構成されていることを確認して、 **AD FS 1.0 および 1.1 プロファイル**します。 




## <a name="to-create-a-rule-to-issue-an-adfs1x-name-id-claim-using-the-pass-through-or-filter-an-incoming-claim-rule-template-on-a-relying-party-trust-in-windows-server-2016"></a>AD FS 1 を発行するルールを作成します。*x*名前 ID 要求のパススルーを使用してまたは証明書利用者の信頼を Windows Server 2016 で、入力方向の要求規則テンプレートをフィルター処理 

1.  サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  
  
2.  コンソール ツリーで [ **AD FS**、] をクリックして**証明書利用者信頼**します。 
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  右\-選択の信頼をクリックし、クリックして**要求発行ポリシーの編集**します。
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  **要求発行ポリシーの編集**ダイアログ ボックスで、**発行変換規則** をクリックして**規則の追加**ルール ウィザードを開始します。 
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  **規則テンプレートの選択** ページ **要求規則テンプレート**を選択します**パススルーまたはフィルター処理の入力方向の要求** をクリックし、一覧から **次へ** .  
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)    

6.  **規則の構成**ページで、要求規則の名前を入力します。  
  
7.  **着信要求の種類**を選択します**名前 ID**一覧にします。  
  
8.  **着信名前 ID 形式**、次の AD FS 1 のいずれかを選択します *。x*\-互換性のあるリストから形式を要求します。  
  
    -   **UPN**  
  
    -   **E\-メール**  
  
    -   **共通名**  
  
9. 組織のニーズに応じて、次のオプションのいずれかを選択します。  
  
    -   **すべての要求値をパススルーします。**  
  
    -   **特定の要求値のみをパススルーします。**  
  
    -   **特定の電子メール サフィックスの値に一致する要求値のみをパススルーします。**  
  
    -   **特定の値で始まる要求値のみをパススルーします。**  
![ルールを作成します。](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs3.PNG)   

10. をクリックして**完了**、順にクリックします**OK**ルールを保存します。  

  
## <a name="to-create-a-rule-to-issue-an-adfs1x-name-id-claim-using-the-pass-through-or-filter-an-incoming-claim-rule-template-on-a-claims-provider-trust-in-windows-server-2016"></a>AD FS 1 を発行するルールを作成します。*x*名前 ID 要求のパススルーを使用してまたは Windows Server 2016 での要求プロバイダー信頼で、入力方向の要求規則テンプレートをフィルター処理 
  
1.  サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  
  
2.  コンソール ツリーで [ **AD FS**、] をクリックして**要求プロバイダー信頼**します。 
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  右\-選択の信頼をクリックし、クリックして**要求規則の編集**します。
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  **要求規則の編集**ダイアログ ボックスで、**受け入れ変換規則** をクリックして**規則の追加**ルール ウィザードを開始します。
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  **規則テンプレートの選択** ページ **要求規則テンプレート**を選択します**パススルーまたはフィルター処理の入力方向の要求** をクリックし、一覧から **次へ** .  
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)    

6.  **規則の構成**ページで、要求規則の名前を入力します。  
  
7.  **着信要求の種類**を選択します**名前 ID**一覧にします。  
  
8.  **着信名前 ID 形式**、次の AD FS 1 のいずれかを選択します *。x*\-互換性のあるリストから形式を要求します。  
  
    -   **UPN**  
  
    -   **E\-メール**  
  
    -   **共通名**  
  
9. 組織のニーズに応じて、次のオプションのいずれかを選択します。  
  
    -   **すべての要求値をパススルーします。**  
  
    -   **特定の要求値のみをパススルーします。**  
  
    -   **特定の電子メール サフィックスの値に一致する要求値のみをパススルーします。**  
  
    -   **特定の値で始まる要求値のみをパススルーします。**  
![ルールを作成します。](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs3.PNG)   

10. をクリックして**完了**、順にクリックします**OK**ルールを保存します。  

  

## <a name="to-create-a-rule-to-transform-an-incoming-claim-on-a-relying-party-trust-in-windows-server-2016"></a>証明書利用者の信頼を Windows Server 2016 での入力方向の要求を変換する規則を作成するには 

1.  サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  
  
2.  コンソール ツリーで [ **AD FS**、] をクリックして**証明書利用者信頼**します。 
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  右\-選択の信頼をクリックし、クリックして**要求発行ポリシーの編集**します。
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  **要求発行ポリシーの編集**ダイアログ ボックスで、**発行変換規則** をクリックして**規則の追加**ルール ウィザードを開始します。 
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  **規則テンプレートの選択** ページ **要求規則テンプレート**を選択します**入力方向の要求を変換** をクリックし、一覧から**次**.  
![ルールを作成します。](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform3.PNG)      

6.  **規則の構成**ページで、要求規則の名前を入力します。  
  
7.  **着信要求の種類**リストに変換する入力方向の要求の種類を選択します。  
  
8.  **出力方向の要求の種類**を選択します**名前 ID**一覧にします。  
  
9. **発信名前 ID 形式**、次の AD FS 1 のいずれかを選択します *。x*\-互換性のあるリストから形式を要求します。  
  
    -   **UPN**  
  
    -   **E\-メール**  
  
    -   **共通名**  
  
10. 組織のニーズに応じて、次のオプションのいずれかを選択します。  
  
    -   **すべての要求値をパススルーします。**  
  
    -   **入力方向の要求値を別の送信要求の値に置き換えます**  
  
    -   **受信した電子メールを置き換える\-メールで新しい電子メール サフィックス要求\-メール サフィックス**  
![ルールを作成します。](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs4.PNG)    

11. をクリックして**完了**、順にクリックします**OK**ルールを保存します。  

  


## <a name="to-create-a-rule-to-transform-an-incoming-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>Windows Server 2016 での要求プロバイダー信頼の入力方向の要求を変換する規則を作成するには 
  
1.  サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  
  
2.  コンソール ツリーで [ **AD FS**、] をクリックして**要求プロバイダー信頼**します。 
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  右\-選択の信頼をクリックし、クリックして**要求規則の編集**します。
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  **要求規則の編集**ダイアログ ボックスで、**受け入れ変換規則** をクリックして**規則の追加**ルール ウィザードを開始します。
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  **規則テンプレートの選択** ページ **要求規則テンプレート**を選択します**入力方向の要求を変換** をクリックし、一覧から**次**.  
![ルールを作成します。](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform3.PNG)      

6.  **規則の構成**ページで、要求規則の名前を入力します。  
  
7.  **着信要求の種類**リストに変換する入力方向の要求の種類を選択します。  
  
8.  **出力方向の要求の種類**を選択します**名前 ID**一覧にします。  
  
9. **発信名前 ID 形式**、次の AD FS 1 のいずれかを選択します *。x*\-互換性のあるリストから形式を要求します。  
  
    -   **UPN**  
  
    -   **E\-メール**  
  
    -   **共通名**  
  
10. 組織のニーズに応じて、次のオプションのいずれかを選択します。  
  
    -   **すべての要求値をパススルーします。**  
  
    -   **入力方向の要求値を別の送信要求の値に置き換えます**  
  
    -   **受信した電子メールを置き換える\-メールで新しい電子メール サフィックス要求\-メール サフィックス**  
![ルールを作成します。](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs4.PNG)    

11. をクリックして**完了**、順にクリックします**OK**ルールを保存します。  













  
## <a name="to-create-a-rule-to-issue-an-adfs1x-name-id-claim-using-the-pass-through-or-filter-an-incoming-claim-rule-template-on-windows-server-2012-r2"></a>AD FS 1 を発行するルールを作成します。*x*名前 ID 要求のパススルーを使用してまたは Windows Server 2012 R2 で、入力方向の要求規則テンプレートをフィルター処理
  
1.  サーバー マネージャーで、**ツール**、 をクリックし、 **AD FS 管理**します。  
  
2.  コンソール ツリーで [ **AD FS\\信頼関係**、] をクリックするか**要求プロバイダー信頼**または**証明書利用者信頼**特定の順にクリックしますこのルールを作成するリスト内の信頼します。  
  
3.  右\-選択の信頼をクリックし、クリックして**要求規則の編集**します。  
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG) 
  
4.  **要求規則の編集**ダイアログ ボックスで、1 つに、次のタブを選択、信頼関係を編集して、ルール セットによって、この規則を作成して順にクリックします**規則の追加**ルール ウィザードを起動するにはその規則セットに関連付けられています。  
  
    -   **受け入れ変換規則**  
  
    -   **発行変換規則**  
  
    -   **発行承認規則**  
  
    -   **委任承認規則**  
![ルールを作成します。](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)    

5.  **規則テンプレートの選択** ページ **要求規則テンプレート**を選択します**パススルーまたはフィルター処理の入力方向の要求** をクリックし、一覧から **次へ** .  
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule7.PNG)  
  
6.  **規則の構成**ページで、要求規則の名前を入力します。  
  
7.  **着信要求の種類**を選択します**名前 ID**一覧にします。  
  
8.  **着信名前 ID 形式**、次の AD FS 1 のいずれかを選択します *。x*\-互換性のあるリストから形式を要求します。  
  
    -   **UPN**  
  
    -   **E\-メール**  
  
    -   **共通名**  
  
9. 組織のニーズに応じて、次のオプションのいずれかを選択します。  
  
    -   **すべての要求値をパススルーします。**  
  
    -   **特定の要求値のみをパススルーします。**  
  
    -   **特定の電子メール サフィックスの値に一致する要求値のみをパススルーします。**  
  
    -   **特定の値で始まる要求値のみをパススルーします。**  
![ルールを作成します。](media/\Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs1.PNG)   

10. をクリックして**完了**、順にクリックします**OK**ルールを保存します。  

  
## <a name="to-create-a-rule-to-issue-an-adfs1x-name-id-claim-using-the-transform-an-incoming-claim-rule-template-in-windows-server-2012-r2"></a>AD FS 1 を発行するルールを作成します。*x*名前 ID 要求が Windows Server 2012 R2 で、変換、入力方向の要求規則テンプレートを使用します。  
  
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
  
5.  **規則テンプレートの選択** ページ **要求規則テンプレート**を選択します**入力方向の要求を変換** をクリックし、一覧から**次**.  
![ルールを作成します。](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform1.PNG)   
  
6.  **規則の構成**ページで、要求規則の名前を入力します。  
  
7.  **着信要求の種類**リストに変換する入力方向の要求の種類を選択します。  
  
8.  **出力方向の要求の種類**を選択します**名前 ID**一覧にします。  
  
9. **発信名前 ID 形式**、次の AD FS 1 のいずれかを選択します *。x*\-互換性のあるリストから形式を要求します。  
  
    -   **UPN**  
  
    -   **E\-メール**  
  
    -   **共通名**  
  
10. 組織のニーズに応じて、次のオプションのいずれかを選択します。  
  
    -   **すべての要求値をパススルーします。**  
  
    -   **入力方向の要求値を別の送信要求の値に置き換えます**  
  
    -   **受信した電子メールを置き換える\-メールで新しい電子メール サフィックス要求\-メール サフィックス**  
![ルールを作成します。](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs2.PNG)    

11. をクリックして**完了**、順にクリックします**OK**ルールを保存します。  

## <a name="additional-references"></a>その他の参照情報 
[要求規則を構成する](Configure-Claim-Rules.md)  
 
[チェックリスト:証明書利用者信頼の要求規則の作成](https://technet.microsoft.com/library/ee913578.aspx)  

[チェックリスト:要求プロバイダー信頼の要求規則の作成](https://technet.microsoft.com/library/ee913564.aspx)  
  
[承認要求規則を使用する場合](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[要求の役割](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[要求規則の役割](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
