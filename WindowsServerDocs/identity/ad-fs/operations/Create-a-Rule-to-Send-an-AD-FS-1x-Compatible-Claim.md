---
ms.assetid: 0039fbbb-b981-4526-a550-f3456ff27635
title: "入力方向の要求を変換する規則を作成します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3745a0ab9d313223c611e58864dd6b4d747f0624
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="create-a-rule-to-send-an-ad-fs-1x-compatible-claim"></a>AD FS 1.x の互換性のある要求を送信する規則を作成します。

>適用対象: Windows Server 2016、Windows Server 2012 R2


Active Directory フェデレーション サービスを使用している場合に発行する \(AD FS\) 信頼性情報は、AD FS 1.0 を実行しているフェデレーション サーバーで受信される \ (Windows Server 2003 R2\) または AD FS 1.1 \ (Windows Server 2008 または Windows Server 2008 R2\)、次を行う必要があります。  
  
-   名前 ID 要求の種類の形式での UPN、電子メール、または共通名を送信する規則を作成します。  
  
-   送信される他のすべての要求は、次の要求の種類のいずれかが必要です。  
  
    -   AD FS 1 です。*x*電子メール アドレス  
  
    -   AD FS 1 です。*x* UPN  
  
    -   共通名  
  
    -   グループ  
  
    -   その他の要求の種類 https://schemas.xmlsoap.org/claims/EmployeeID などの https://schemas.xmlsoap.org/claims/ で始まる  
  
によっては、組織のニーズを AD FS 1 を作成するのに、次の手順のいずれかを使用します。*x* NameID 互換の要求。  
  
-   問題、AD FS 1.x 名前 ID 要求を使用するには、この規則の作成、**パススルーまたはフィルター処理、入力方向の要求規則テンプレート**  
  
-   問題、AD FS 1.x 名前 ID 要求を使用するには、この規則の作成、 **、入力方向の要求規則テンプレートを変換**します。 AD FS 1 で動作する新しい要求の種類に既存の要求の種類を変更する状況では、この規則テンプレートを使用できます。 *x*要求します。  
  
> [!NOTE]  
> 期待どおりに動作するには、この規則に証明書利用者の信頼またはこのルールを作成する要求プロバイダー信頼が構成されているを使用することを確認してください、 **AD FS 1.0 および 1.1 プロファイル**します。 




## <a name="to-create-a-rule-to-issue-an-ad-fs-1x-name-id-claim-using-the-pass-through-or-filter-an-incoming-claim-rule-template-on-a-relying-party-trust-in-windows-server-2016"></a>AD FS 1 を発行する規則を作成します。*x*名前 ID 要求のパススルーまたは a Relying Party Trust Windows Server 2016 での入力方向の要求規則テンプレートをフィルター処理 

1.  サーバー マネージャーで、クリックして**ツール**、し、[ **AD FS 管理**します。  
  
2.  コンソール ツリーで、[ **AD FS**、] をクリックして**証明書利用者信頼**します。 
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  選択した信頼を右クリックし、クリック**要求発行ポリシーの編集**します。
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  **要求発行ポリシーの編集**ダイアログ ボックスで、**発行変換規則**] をクリックして**規則の追加**規則ウィザードを開始します。 
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  **規則テンプレートの選択**ページで、**要求規則テンプレート**[**パススルーまたはフィルター処理入力方向の要求**クリックして、一覧から**[次へ]**します。  
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)    

6.  **規則の構成**] ページで、要求規則名を入力します。  
  
7.  **入力方向の要求の種類**[**名前 ID**一覧にします。  
  
8.  **名前 ID の形式の入力方向**、次の AD FS 1 のいずれかを選択します。*x*\-compatible 要求の形式の一覧から。  
  
    -   **UPN**  
  
    -   **E\ メール**  
  
    -   **共通名**  
  
9. 組織のニーズに応じて、次のオプションのいずれかを選択します。  
  
    -   **すべての要求の値をパススルーします。**  
  
    -   **特定の要求値のみをパススルーします。**  
  
    -   **特定の電子メール サフィックスの値に一致する要求値のみをパススルーします。**  
  
    -   **特定の値で始まる要求値のみをパススルーします。**  
![規則を作成します。](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs3.PNG)   

10. をクリックして**完了**、] をクリックし、 **OK**に規則を保存します。  

  
## <a name="to-create-a-rule-to-issue-an-ad-fs-1x-name-id-claim-using-the-pass-through-or-filter-an-incoming-claim-rule-template-on-a-claims-provider-trust-in-windows-server-2016"></a>AD FS 1 を発行する規則を作成します。*x*名前 ID 要求のパススルーまたは Windows Server 2016 での要求プロバイダー信頼で、入力方向の要求規則テンプレートをフィルター処理 
  
1.  サーバー マネージャーで、クリックして**ツール**、し、[ **AD FS 管理**します。  
  
2.  コンソール ツリーで、[ **AD FS**、] をクリックして**要求プロバイダー信頼**します。 
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  選択した信頼を右クリックし、クリック**要求規則の編集**します。
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  **要求規則の編集**ダイアログ ボックスで、**受け付け変換規則**] をクリックして**規則の追加**規則ウィザードを開始します。
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  **規則テンプレートの選択**ページで、**要求規則テンプレート**[**パススルーまたはフィルター処理入力方向の要求**クリックして、一覧から**[次へ]**します。  
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)    

6.  **規則の構成**] ページで、要求規則名を入力します。  
  
7.  **入力方向の要求の種類**[**名前 ID**一覧にします。  
  
8.  **名前 ID の形式の入力方向**、次の AD FS 1 のいずれかを選択します。*x*\-compatible 要求の形式の一覧から。  
  
    -   **UPN**  
  
    -   **E\ メール**  
  
    -   **共通名**  
  
9. 組織のニーズに応じて、次のオプションのいずれかを選択します。  
  
    -   **すべての要求の値をパススルーします。**  
  
    -   **特定の要求値のみをパススルーします。**  
  
    -   **特定の電子メール サフィックスの値に一致する要求値のみをパススルーします。**  
  
    -   **特定の値で始まる要求値のみをパススルーします。**  
![規則を作成します。](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs3.PNG)   

10. をクリックして**完了**、] をクリックし、 **OK**に規則を保存します。  

  

## <a name="to-create-a-rule-to-transform-an-incoming-claim-on-a-relying-party-trust-in-windows-server-2016"></a>A Relying Party Trust Windows Server 2016 での入力方向の要求を変換する規則を作成するには 

1.  サーバー マネージャーで、クリックして**ツール**、し、[ **AD FS 管理**します。  
  
2.  コンソール ツリーで、[ **AD FS**、] をクリックして**証明書利用者信頼**します。 
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  選択した信頼を右クリックし、クリック**要求発行ポリシーの編集**します。
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  **要求発行ポリシーの編集**ダイアログ ボックスで、**発行変換規則**] をクリックして**規則の追加**規則ウィザードを開始します。 
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  **規則テンプレートの選択**ページで、**要求規則テンプレート**[**入力方向の要求を変換**クリックして、一覧から**[次へ]**します。  
![規則を作成します。](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform3.PNG)      

6.  **規則の構成**] ページで、要求規則名を入力します。  
  
7.  **入力方向の要求の種類**、一覧に変換する入力方向の要求の種類を選択します。  
  
8.  **出力方向の要求の種類**[**名前 ID**一覧にします。  
  
9. **発信名前 ID 形式**、次の AD FS 1 のいずれかを選択します。*x*\-compatible 要求の形式の一覧から。  
  
    -   **UPN**  
  
    -   **E\ メール**  
  
    -   **共通名**  
  
10. 組織のニーズに応じて、次のオプションのいずれかを選択します。  
  
    -   **すべての要求の値をパススルーします。**  
  
    -   **入力方向の要求の値を異なる出力方向の要求の値に置き換えます**  
  
    -   **入力方向の e\ 電子メール サフィックス要求を新しい e\ メール サフィックスに置き換えます**  
![規則を作成します。](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs4.PNG)    

11. をクリックして**完了**、] をクリックし、 **OK**に規則を保存します。  

  


## <a name="to-create-a-rule-to-transform-an-incoming-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>Windows Server 2016 での要求プロバイダー信頼の入力方向の要求を変換する規則を作成するには 
  
1.  サーバー マネージャーで、クリックして**ツール**、し、[ **AD FS 管理**します。  
  
2.  コンソール ツリーで、[ **AD FS**、] をクリックして**要求プロバイダー信頼**します。 
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  選択した信頼を右クリックし、クリック**要求規則の編集**します。
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  **要求規則の編集**ダイアログ ボックスで、**受け付け変換規則**] をクリックして**規則の追加**規則ウィザードを開始します。
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  **規則テンプレートの選択**ページで、**要求規則テンプレート**[**入力方向の要求を変換**クリックして、一覧から**[次へ]**します。  
![規則を作成します。](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform3.PNG)      

6.  **規則の構成**] ページで、要求規則名を入力します。  
  
7.  **入力方向の要求の種類**、一覧に変換する入力方向の要求の種類を選択します。  
  
8.  **出力方向の要求の種類**[**名前 ID**一覧にします。  
  
9. **発信名前 ID 形式**、次の AD FS 1 のいずれかを選択します。*x*\-compatible 要求の形式の一覧から。  
  
    -   **UPN**  
  
    -   **E\ メール**  
  
    -   **共通名**  
  
10. 組織のニーズに応じて、次のオプションのいずれかを選択します。  
  
    -   **すべての要求の値をパススルーします。**  
  
    -   **入力方向の要求の値を異なる出力方向の要求の値に置き換えます**  
  
    -   **入力方向の e\ 電子メール サフィックス要求を新しい e\ メール サフィックスに置き換えます**  
![規則を作成します。](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs4.PNG)    

11. をクリックして**完了**、] をクリックし、 **OK**に規則を保存します。  













  
## <a name="to-create-a-rule-to-issue-an-ad-fs-1x-name-id-claim-using-the-pass-through-or-filter-an-incoming-claim-rule-template-on-windows-server-2012-r2"></a>AD FS 1 を発行する規則を作成します。*x*名前 ID 要求のパススルーまたは Windows Server 2012 R2 で、入力方向の要求規則テンプレートをフィルター処理
  
1.  サーバー マネージャーで、クリックして**ツール**、] をクリックし、 **AD FS 管理**します。  
  
2.  コンソール ツリーで、下にある**AD FS\\Trust 関係**、] をクリックするか**要求プロバイダー信頼**または**証明書利用者信頼**、この規則を作成するリスト内の特定の信頼をクリックします。  
  
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
  
6.  **規則の構成**] ページで、要求規則名を入力します。  
  
7.  **入力方向の要求の種類**[**名前 ID**一覧にします。  
  
8.  **名前 ID の形式の入力方向**、次の AD FS 1 のいずれかを選択します。*x*\-compatible 要求の形式の一覧から。  
  
    -   **UPN**  
  
    -   **E\ メール**  
  
    -   **共通名**  
  
9. 組織のニーズに応じて、次のオプションのいずれかを選択します。  
  
    -   **すべての要求の値をパススルーします。**  
  
    -   **特定の要求値のみをパススルーします。**  
  
    -   **特定の電子メール サフィックスの値に一致する要求値のみをパススルーします。**  
  
    -   **特定の値で始まる要求値のみをパススルーします。**  
![規則を作成します。](media/\Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs1.PNG)   

10. をクリックして**完了**、] をクリックし、 **OK**に規則を保存します。  

  
## <a name="to-create-a-rule-to-issue-an-ad-fs-1x-name-id-claim-using-the-transform-an-incoming-claim-rule-template-in-windows-server-2012-r2"></a>AD FS 1 を発行する規則を作成します。*x* Windows Server 2012 R2 での変換、入力方向の要求規則テンプレートを使用して名前 ID 要求  
  
1.  サーバー マネージャーで、クリックして**ツール**、] をクリックし、 **AD FS 管理**します。  
  
2.  コンソール ツリーで、下にある**AD FS\\Trust 関係**、] をクリックするか**要求プロバイダー信頼**または**証明書利用者信頼**、この規則を作成するリスト内の特定の信頼をクリックします。  
  
3.  選択した信頼を右クリックし、クリック**要求規則の編集**します。  
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG) 
  
4.  **要求規則の編集**次のタブは、信頼関係を編集して、どの規則で設定することによって異なりますがこの規則を作成し、をクリックします] ダイアログ ボックスで、いずれかを選択**規則の追加**するルール セットに関連付けられている規則のウィザードを開始します。  
  
    -   **受け入れ変換規則**  
  
    -   **発行変換規則**  
  
    -   **発行承認規則**  
  
    -   **委任承認規則**  
![規則を作成します。](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)
  
5.  **規則テンプレートの選択**ページで、**要求規則テンプレート**[**入力方向の要求を変換**クリックして、一覧から**[次へ]**します。  
![規則を作成します。](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform1.PNG)   
  
6.  **規則の構成**] ページで、要求規則名を入力します。  
  
7.  **入力方向の要求の種類**、一覧に変換する入力方向の要求の種類を選択します。  
  
8.  **出力方向の要求の種類**[**名前 ID**一覧にします。  
  
9. **発信名前 ID 形式**、次の AD FS 1 のいずれかを選択します。*x*\-compatible 要求の形式の一覧から。  
  
    -   **UPN**  
  
    -   **E\ メール**  
  
    -   **共通名**  
  
10. 組織のニーズに応じて、次のオプションのいずれかを選択します。  
  
    -   **すべての要求の値をパススルーします。**  
  
    -   **入力方向の要求の値を異なる出力方向の要求の値に置き換えます**  
  
    -   **入力方向の e\ 電子メール サフィックス要求を新しい e\ メール サフィックスに置き換えます**  
![規則を作成します。](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs2.PNG)    

11. をクリックして**完了**、] をクリックし、 **OK**に規則を保存します。  

## <a name="additional-references"></a>その他の参照 
[要求規則を構成します。](Configure-Claim-Rules.md)  
 
[チェックリスト: 証明書利用者のパーティ信頼の要求規則を作成します。](https://technet.microsoft.com/library/ee913578.aspx)  

[チェックリスト: Creating Claim Rules for 要求プロバイダー信頼します。](https://technet.microsoft.com/library/ee913564.aspx)  
  
[When to Use an Authorization Claim Rule](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[要求の役割](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[要求規則の役割](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
