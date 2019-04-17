---
ms.assetid: ef83960f-d2cf-441f-b2b6-d97822ec7149
title: "入力方向の要求を変換する規則を作成します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e982b7608f7602268657ceae74f641bbaaaec939
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-rule-to-transform-an-incoming-claim"></a>入力方向の要求を変換する規則を作成します。

>適用対象: Windows Server 2016、Windows Server 2012 R2

使用して、**入力方向の要求を変換**規則テンプレートで、Active Directory フェデレーション サービス \(AD FS\) を選択入力方向の要求、その要求の種類を変更してその要求値を変更します。 たとえば、この規則テンプレートを使用して、ロール クレームを同じ要求の値の入力方向のグループ要求を送信する規則を作成することができます。 このルールを使用して Admins, の値を持つ入力方向のグループ要求があるまたはのみユーザーのプリンシパル名 \(UPN\) で終わるの要求を送信するときにグループの要求の購入者の要求の値を送信する@fabrikamします。  
  
次の手順を使用するには、AD FS 管理スナップインの要求規則の作成をします。  
  
メンバーシップ**管理者**、相当するもので、ローカル コンピューターでは、この手順を実行する最小要件またはします。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。 

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

6.  **規則の構成**ページで、**要求規則名**、この規則の表示名を入力します。 **入力方向の要求の種類**、一覧で、要求の種類を選択します。 **出力方向の要求の種類**、一覧で、要求の種類を選択し、組織の要件によって異なりますが、次のオプションのいずれかを選択します。  
  
    -   **すべての要求の値をパススルーします。**  
  
    -   **入力方向の要求の値を異なる出力方向の要求の値に置き換えます**  
  
    -   **入力方向の e\ 電子メール サフィックス要求を新しい e\ メール サフィックスに置き換えます**  
![規則を作成します。](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform4.PNG)   

7.  をクリックして、**完了**ボタンをクリックします。  
  
8.  **要求規則の編集**ダイアログ ボックスで、] をクリックして**OK**に規則を保存します。
  
> [!NOTE]  
> AD FS\ によって発行されたクレームを使用するダイナミック アクセス制御シナリオを設定するは、まずルールを作成トランス フォームと、要求プロバイダー信頼で**入力方向の要求の種類**、入力方向の要求の名前を入力または、要求記述を以前に作成された場合は、一覧から選択します。 1 秒、**出力方向の要求の種類**、必要な要求 URL を選択し、証明書利用者信頼に対してデバイスの信頼性情報を発行する変換規則を作成します。  
>   
> ダイナミック アクセス制御シナリオの詳細については、次を参照してください。[ダイナミック アクセス制御: コンテンツ ロードマップ](../../solution-guides/dynamic-access-control--scenario-overview.md)または[を AD FS と共に使用する AD DS 信頼性情報](https://technet.microsoft.com/library/hh831504.aspx)します。 

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

6.  **規則の構成**ページで、**要求規則名**、この規則の表示名を入力します。 **入力方向の要求の種類**、一覧で、要求の種類を選択します。 **出力方向の要求の種類**、一覧で、要求の種類を選択し、組織の要件によって異なりますが、次のオプションのいずれかを選択します。  
  
    -   **すべての要求の値をパススルーします。**  
  
    -   **入力方向の要求の値を異なる出力方向の要求の値に置き換えます**  
  
    -   **入力方向の e\ 電子メール サフィックス要求を新しい e\ メール サフィックスに置き換えます**  
![規則を作成します。](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform4.PNG)       

7.  をクリックして、**完了**ボタンをクリックします。  
  
8.  **要求規則の編集**ダイアログ ボックスで、] をクリックして**OK**に規則を保存します。  

> [!NOTE]  
> AD FS\ によって発行されたクレームを使用するダイナミック アクセス制御シナリオを設定するは、まずルールを作成トランス フォームと、要求プロバイダー信頼で**入力方向の要求の種類**、入力方向の要求の名前を入力または、要求記述を以前に作成された場合は、一覧から選択します。 1 秒、**出力方向の要求の種類**、必要な要求 URL を選択し、証明書利用者信頼に対してデバイスの信頼性情報を発行する変換規則を作成します。  
>   
> ダイナミック アクセス制御シナリオの詳細については、次を参照してください。[ダイナミック アクセス制御: コンテンツ ロードマップ](../../solution-guides/dynamic-access-control--scenario-overview.md)または[を AD FS と共に使用する AD DS 信頼性情報](https://technet.microsoft.com/library/hh831504.aspx)します。   
  
## <a name="to-create-a-rule-to-transform-an-incoming-claim-in-windows-server-2012-r2"></a>Windows Server 2012 R2 での入力方向の要求を変換する規則を作成するには 
  
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

6.  **規則の構成**ページで、**要求規則名**、この規則の表示名を入力します。 **入力方向の要求の種類**、一覧で、要求の種類を選択します。 **出力方向の要求の種類**、一覧で、要求の種類を選択し、組織の要件によって異なりますが、次のオプションのいずれかを選択します。  
  
    -   **すべての要求の値をパススルーします。**  
  
    -   **入力方向の要求の値を異なる出力方向の要求の値に置き換えます**  
  
    -   **入力方向の e\ 電子メール サフィックス要求を新しい e\ メール サフィックスに置き換えます**  
![規則を作成します。](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform2.PNG)  

> [!NOTE]  
> AD FS\ によって発行されたクレームを使用するダイナミック アクセス制御シナリオを設定するは、まずルールを作成トランス フォームと、要求プロバイダー信頼で**入力方向の要求の種類**、入力方向の要求の名前を入力または、要求記述を以前に作成された場合は、一覧から選択します。 1 秒、**出力方向の要求の種類**、必要な要求 URL を選択し、証明書利用者信頼に対してデバイスの信頼性情報を発行する変換規則を作成します。  
>   
> ダイナミック アクセス制御シナリオの詳細については、次を参照してください。[ダイナミック アクセス制御: コンテンツ ロードマップ](../../solution-guides/dynamic-access-control--scenario-overview.md)または[を AD FS と共に使用する AD DS 信頼性情報](https://technet.microsoft.com/library/hh831504.aspx)します。  
  
7.  をクリックして**完了**します。  
  
8.  **要求規則の編集**ダイアログ ボックスで、] をクリックして**OK**に規則を保存します。  

## <a name="additional-references"></a>その他の参照 
[要求規則を構成します。](Configure-Claim-Rules.md)  
 
[チェックリスト: 証明書利用者のパーティ信頼の要求規則を作成します。](https://technet.microsoft.com/library/ee913578.aspx)  

[チェックリスト: Creating Claim Rules for 要求プロバイダー信頼します。](https://technet.microsoft.com/library/ee913564.aspx)  
  
[When to Use an Authorization Claim Rule](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[要求の役割](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[要求規則の役割](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
