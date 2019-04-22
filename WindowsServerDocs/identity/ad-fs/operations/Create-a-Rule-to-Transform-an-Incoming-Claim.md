---
ms.assetid: ef83960f-d2cf-441f-b2b6-d97822ec7149
title: 入力方向の要求を変換する規則を作成する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e982b7608f7602268657ceae74f641bbaaaec939
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816683"
---
# <a name="create-a-rule-to-transform-an-incoming-claim"></a>入力方向の要求を変換する規則を作成する

>適用先:Windows Server 2016、Windows Server 2012 R2

使用して、**入力方向の要求を変換**規則テンプレートの Active Directory フェデレーション サービスで\(AD FS\)、入力方向の要求を選択して、その要求の種類を変更およびその要求の値を変更します。 たとえば、この規則テンプレートを使用して、入力方向のグループ要求の要求値が同じロール要求を送信するルールを作成することができます。 Admins, の値を持つ入力方向のグループ要求がある、またはユーザー プリンシパル名のみを送信するときにグループの要求の購入者の要求の値を送信するこのルールを使用することもできます。 \(UPN\)で終わる要求@fabrikamします。  
  
次の手順を使用するには、AD FS 管理スナップインで要求規則を作成する\-でします。  
  
メンバーシップ**管理者**、またはこの手順を実行する最小要件は、ローカル コンピューターのそれと同等です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。 

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

6.  **規則の構成**] ページ [**要求規則名**、この規則の表示名を入力します。 **着信要求の種類**一覧で、要求の種類を選択します。 **出力方向の要求の種類**を一覧で、要求の種類を選択し、組織の要件に依存する次のオプションのいずれかを選択します。  
  
    -   **すべての要求値をパススルーします。**  
  
    -   **入力方向の要求値を別の送信要求の値に置き換えます**  
  
    -   **受信した電子メールを置き換える\-メールで新しい電子メール サフィックス要求\-メール サフィックス**  
![ルールを作成します。](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform4.PNG)   

7.  をクリックして、**完了**ボタンをクリックします。  
  
8.  **要求規則の編集**ダイアログ ボックスで、をクリックして **[ok]** ルールを保存します。
  
> [!NOTE]  
> AD FS を使用するダイナミック アクセス制御シナリオを設定している場合\-と、要求プロバイダー信頼では、変換規則を作成要求を発行するには、まず**着信要求の種類**、入力方向の要求の名前を入力または、以前に作成されたクレームの説明、一覧から選択してください。 2 番目に**出力方向の要求の種類**、必要な要求 URL を選択し、デバイスの信頼性情報を発行するための証明書利用者信頼の変換規則を作成します。  
>   
> ダイナミック アクセス制御シナリオの詳細については、次を参照してください。[ダイナミック アクセス制御: コンテンツ ロードマップ](../../solution-guides/dynamic-access-control--scenario-overview.md)または[と AD FS を使用して AD DS 信頼性情報](https://technet.microsoft.com/library/hh831504.aspx)します。 

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

6.  **規則の構成**] ページ [**要求規則名**、この規則の表示名を入力します。 **着信要求の種類**一覧で、要求の種類を選択します。 **出力方向の要求の種類**を一覧で、要求の種類を選択し、組織の要件に依存する次のオプションのいずれかを選択します。  
  
    -   **すべての要求値をパススルーします。**  
  
    -   **入力方向の要求値を別の送信要求の値に置き換えます**  
  
    -   **受信した電子メールを置き換える\-メールで新しい電子メール サフィックス要求\-メール サフィックス**  
![ルールを作成します。](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform4.PNG)       

7.  をクリックして、**完了**ボタンをクリックします。  
  
8.  **要求規則の編集**ダイアログ ボックスで、をクリックして **[ok]** ルールを保存します。  

> [!NOTE]  
> AD FS を使用するダイナミック アクセス制御シナリオを設定している場合\-と、要求プロバイダー信頼では、変換規則を作成要求を発行するには、まず**着信要求の種類**、入力方向の要求の名前を入力または、以前に作成されたクレームの説明、一覧から選択してください。 2 番目に**出力方向の要求の種類**、必要な要求 URL を選択し、デバイスの信頼性情報を発行するための証明書利用者信頼の変換規則を作成します。  
>   
> ダイナミック アクセス制御シナリオの詳細については、次を参照してください。[ダイナミック アクセス制御: コンテンツ ロードマップ](../../solution-guides/dynamic-access-control--scenario-overview.md)または[と AD FS を使用して AD DS 信頼性情報](https://technet.microsoft.com/library/hh831504.aspx)します。   
  
## <a name="to-create-a-rule-to-transform-an-incoming-claim-in-windows-server-2012-r2"></a>Windows Server 2012 R2 での入力方向の要求を変換する規則を作成するには 
  
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

6.  **規則の構成**] ページ [**要求規則名**、この規則の表示名を入力します。 **着信要求の種類**一覧で、要求の種類を選択します。 **出力方向の要求の種類**を一覧で、要求の種類を選択し、組織の要件に依存する次のオプションのいずれかを選択します。  
  
    -   **すべての要求値をパススルーします。**  
  
    -   **入力方向の要求値を別の送信要求の値に置き換えます**  
  
    -   **受信した電子メールを置き換える\-メールで新しい電子メール サフィックス要求\-メール サフィックス**  
![ルールを作成します。](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform2.PNG)  

> [!NOTE]  
> AD FS を使用するダイナミック アクセス制御シナリオを設定している場合\-と、要求プロバイダー信頼では、変換規則を作成要求を発行するには、まず**着信要求の種類**、入力方向の要求の名前を入力または、以前に作成されたクレームの説明、一覧から選択してください。 2 番目に**出力方向の要求の種類**、必要な要求 URL を選択し、デバイスの信頼性情報を発行するための証明書利用者信頼の変換規則を作成します。  
>   
> ダイナミック アクセス制御シナリオの詳細については、次を参照してください。[ダイナミック アクセス制御: コンテンツ ロードマップ](../../solution-guides/dynamic-access-control--scenario-overview.md)または[と AD FS を使用して AD DS 信頼性情報](https://technet.microsoft.com/library/hh831504.aspx)します。  
  
7.  **[Finish]**(完了) をクリックします。  
  
8.  **要求規則の編集**ダイアログ ボックスで、をクリックして **[ok]** ルールを保存します。  

## <a name="additional-references"></a>その他の参照情報 
[要求規則を構成します。](Configure-Claim-Rules.md)  
 
[チェックリスト:A Relying Party Trust の要求規則を作成します。](https://technet.microsoft.com/library/ee913578.aspx)  

[チェックリスト:要求規則の作成要求プロバイダー信頼します。](https://technet.microsoft.com/library/ee913564.aspx)  
  
[承認要求規則を使用する場合](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[要求の役割](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[要求規則の役割](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
