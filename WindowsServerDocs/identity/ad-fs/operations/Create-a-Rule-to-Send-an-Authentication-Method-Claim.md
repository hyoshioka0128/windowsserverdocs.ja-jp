---
ms.assetid: 96b9f4e6-f01c-4517-8299-017d187d447e
title: 認証方法の要求を送信する規則を作成する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4065a61e042f52298da656899289e718e010f932
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819093"
---
# <a name="create-a-rule-to-send-an-authentication-method-claim"></a>認証方法の要求を送信する規則を作成する

>適用先:Windows Server 2016、Windows Server 2012 R2

いずれかを使用することができます、**グループ メンバーシップを要求として送信**規則テンプレートまたは**入力方向の要求を変換**メソッドの認証要求を送信する規則テンプレート。 証明書利用者は、メソッドの認証要求を使用して、ユーザーが認証および取得に使用するログオン メカニズムは Active Directory フェデレーション サービスから要求を決定する\(AD FS\)します。 Active Directory フェデレーション サービスの認証メカニズム保証の機能を使用することもできます\(AD FS\)を状況メソッド要求の認証を生成する入力として Windows Server 2012 R2 で、証明書利用者。スマート カードのログオン時に基づいているアクセスのレベルを確認したいとします。 たとえば、開発者は、証明書利用者アプリケーションのフェデレーション ユーザーに異なるアクセス レベルを割り当てることができます。 アクセスのレベルは、そのユーザー名とパスワード資格情報で、スマート カードではなく、ユーザーのログオンかどうかに基づいています。  
  
組織の要件に応じて、次の手順のいずれかの手順に従います。  
  
-   使用してこのルールを作成、**グループ メンバーシップを要求として送信**規則テンプレート\-最終的にこのテンプレートで指定したグループは、どのような認証方法を決定する場合は、この規則テンプレートを使用することができます発行する要求します。  
  
-   使用してこのルールを作成、**入力方向の要求を変換**規則テンプレート\-製品で動作する新しい認証方法に既存の認証方法を変更する場合は、この規則テンプレートを使用することができますAD FS 認証メソッドの標準の要求を認識しません。  
  


## <a name="to-create-by-using-the-send-group-membership-as-claims-rule-template-on-a-relying-party-trust-in-windows-server-2016"></a>証明書利用者の信頼を Windows Server 2016 での要求規則テンプレートとして送信するグループのメンバーシップを使用して作成するには 

1.  サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  
  
2.  コンソール ツリーで [ **AD FS**、] をクリックして**証明書利用者信頼**します。 
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  右\-選択の信頼をクリックし、クリックして**要求発行ポリシーの編集**します。
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  **要求発行ポリシーの編集**ダイアログ ボックスで、**発行変換規則** をクリックして**規則の追加**ルール ウィザードを開始します。 
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  **規則テンプレートの選択** ページ **要求規則テンプレート**を選択します**グループ メンバーシップを要求として送信** をクリックし、一覧から**次へ**.  
![ルールを作成します。](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group3.PNG)      

6.  **規則の構成**ページで、要求規則の名前を入力します。  
  
7.  をクリックして**参照**、選択、グループのメンバーを持つ必要がありますこの認証メソッド要求を受け取るし、順にクリックします**OK**します。  
  
8.  **出力方向の要求の種類**を選択します**認証メソッド**一覧にします。  
  
9. **出力方向の要求値**、既定の uniform resource identifier のいずれかを入力\(URI\)推奨される認証方法に応じて、次の表の値をクリックして**の完了**、 をクリックし、 **OK**ルールを保存します。  
  
|実際の認証方法|対応する URI|  
|--------------------------------|---------------------|  
|ユーザー名とパスワードの認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password|  
|Windows 認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows|  
|トランスポート層セキュリティ\(TLS\) X.509 証明書を使用して相互認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient|  
|X.509\-ベースの認証では、TLS を使用しません。|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509|  
![ルールを作成します。](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth2.PNG)
  
## <a name="to-create-by-using-the-send-group-membership-as-claims-rule-template-on-a-claims-provider-trust-in-windows-server-2016"></a>Windows Server 2016 での要求プロバイダー信頼の要求規則テンプレートとして送信するグループのメンバーシップを使用して作成するには 
  
1.  サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  
  
2.  コンソール ツリーで [ **AD FS**、] をクリックして**要求プロバイダー信頼**します。 
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  右\-選択の信頼をクリックし、クリックして**要求規則の編集**します。
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  **要求規則の編集**ダイアログ ボックスで、**受け入れ変換規則** をクリックして**規則の追加**ルール ウィザードを開始します。
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  **規則テンプレートの選択** ページ **要求規則テンプレート**を選択します**グループ メンバーシップを要求として送信** をクリックし、一覧から**次へ**.  
![ルールを作成します。](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group3.PNG)     

6.  **規則の構成**ページで、要求規則の名前を入力します。  
  
7.  をクリックして**参照**、選択、グループのメンバーを持つ必要がありますこの認証メソッド要求を受け取るし、順にクリックします**OK**します。  
  
8.  **出力方向の要求の種類**を選択します**認証メソッド**一覧にします。  
  
9. **出力方向の要求値**、既定の uniform resource identifier のいずれかを入力\(URI\)推奨される認証方法に応じて、次の表の値をクリックして**の完了**、 をクリックし、 **OK**ルールを保存します。  
  
|実際の認証方法|対応する URI|  
|--------------------------------|---------------------|  
|ユーザー名とパスワードの認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password|  
|Windows 認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows|  
|トランスポート層セキュリティ\(TLS\) X.509 証明書を使用して相互認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient|  
|X.509\-ベースの認証では、TLS を使用しません。|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509|  
![ルールを作成します。](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth2.PNG)


## <a name="to-create-this-rule-by-using-the-transform-an-incoming-claim-rule-template-on-a-relying-party-trust-in-windows-server-2016"></a>入力方向の要求規則テンプレートの証明書利用者の信頼を Windows Server 2016 での変換を使用してこのルールを作成するには 

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
  
7.  **着信要求の種類**を選択します**認証メソッド**一覧にします。  
  
8.  **出力方向の要求の種類**を選択します**認証メソッド**一覧にします。  
  
9. 選択**方向の要求値を別の送信要求の値に置き換えます**、し、次の操作を行います。  
  
    1.  **着信要求の値**実際の認証メソッドの最初に使用された URI に基づく次の URI 値のいずれかの入力をクリックし、**完了**、 をクリックし、 **ok**ルールを保存します。  
  
    2.  **出力方向の要求値**、次の表は、新しいの推奨される認証方法の選択内容に応じて決まります入力 URI の既定値のいずれか、をクリックして**完了**、 をクリックし、 **ok**ルールを保存します。  
  
|実際の認証方法|対応する URI|  
|--------------------------------|---------------------|  
|ユーザー名とパスワードの認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password|  
|Windows 認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows|  
|X.509 証明書を使用する TLS 相互認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient|  
|X.509\-ベースの認証では、TLS を使用しません。|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509|  
![ルールを作成します。](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth4.PNG)
  
> [!NOTE]  
> テーブル内の値だけでなく、その他の URI 値を使用できます。 Ion 示されている URI 値、前の表では、既定では、証明書利用者が受け取る Uri が反映されます。  

## <a name="to-create-this-rule-by-using-the-transform-an-incoming-claim-rule-template-on-a-claims-provider-trust-in-windows-server-2016"></a>入力方向の要求規則テンプレートの Windows Server 2016 での要求プロバイダー信頼の変換を使用してこのルールを作成するには 
  
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
  
7.  **着信要求の種類**を選択します**認証メソッド**一覧にします。  
  
8.  **出力方向の要求の種類**を選択します**認証メソッド**一覧にします。  
  
9. 選択**方向の要求値を別の送信要求の値に置き換えます**、し、次の操作を行います。  
  
    1.  **着信要求の値**実際の認証メソッドの最初に使用された URI に基づく次の URI 値のいずれかの入力をクリックし、**完了**、 をクリックし、 **ok**ルールを保存します。  
  
    2.  **出力方向の要求値**、次の表は、新しいの推奨される認証方法の選択内容に応じて決まります入力 URI の既定値のいずれか、をクリックして**完了**、 をクリックし、 **ok**ルールを保存します。  
  
|実際の認証方法|対応する URI|  
|--------------------------------|---------------------|  
|ユーザー名とパスワードの認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password|  
|Windows 認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows|  
|X.509 証明書を使用する TLS 相互認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient|  
|X.509\-ベースの認証では、TLS を使用しません。|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509|  
![ルールを作成します。](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth4.PNG)























## <a name="to-create-this-rule-by-using-the-send-group-membership-as-claims-rule-template-in-windows-server-2012-r2"></a>Windows Server 2012 R2 での要求規則テンプレートとして送信グループ メンバーシップを使用してこのルールを作成するには  
  
1.  サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  
  
2.  コンソール ツリーで [ **AD FS\\信頼関係**、] をクリックするか**要求プロバイダー信頼**または**証明書利用者信頼**特定の順にクリックしますこのルールを作成するリスト内の信頼します。  
  
3.  右\-選択の信頼をクリックし、クリックして**要求規則の編集**します。
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)  
  
4.  **要求規則の編集**ダイアログ ボックスで、1 つに、次のタブを選択、信頼関係を編集して、どのルールを設定することによって、この規則を作成して順にクリックします**規則の追加**ルールを開始するにはその規則セットに関連付けられているウィザード:  
  
    -   **受け入れ変換規則**  
  
    -   **発行変換規則**  
  
    -   **発行承認規則**  
  
    -   **委任承認規則**  
![ルールを作成します。](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)
    
5.  **規則テンプレートの選択** ページ **要求規則テンプレート**を選択します**グループ メンバーシップを要求として送信** をクリックし、一覧から**次へ**.  
![ルールを作成します。](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group1.PNG)
  
6.  **規則の構成**ページで、要求規則の名前を入力します。  
  
7.  をクリックして**参照**、選択、グループのメンバーを持つ必要がありますこの認証メソッド要求を受け取るし、順にクリックします**OK**します。  
  
8.  **出力方向の要求の種類**を選択します**認証メソッド**一覧にします。  
  
9. **出力方向の要求値**、既定の uniform resource identifier のいずれかを入力\(URI\)推奨される認証方法に応じて、次の表の値をクリックして**の完了**、 をクリックし、 **OK**ルールを保存します。  
  
|実際の認証方法|対応する URI|  
|--------------------------------|---------------------|  
|ユーザー名とパスワードの認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password|  
|Windows 認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows|  
|トランスポート層セキュリティ\(TLS\) X.509 証明書を使用して相互認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient|  
|X.509\-ベースの認証では、TLS を使用しません。|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509|  
![ルールを作成します。](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth1.PNG)
 
> [!NOTE]  
> テーブル内の値だけでなく、その他の URI 値を使用できます。 前の表に示す URI の値には、既定では、証明書利用者が受け取る Uri が反映されます。  
  
## <a name="to-create-this-rule-by-using-the-transform-an-incoming-claim-rule-template-in-windows-server-2012-r2"></a>このルールを作成、変換を使用して、入力方向の要求規則テンプレートで Windows Server 2012 R2  
   
  
  
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
  
7.  **着信要求の種類**を選択します**認証メソッド**一覧にします。  
  
8.  **出力方向の要求の種類**を選択します**認証メソッド**一覧にします。  
  
9. 選択**方向の要求値を別の送信要求の値に置き換えます**、し、次の操作を行います。  
  
    1.  **着信要求の値**実際の認証メソッドの最初に使用された URI に基づく次の URI 値のいずれかの入力をクリックし、**完了**、 をクリックし、 **ok**ルールを保存します。  
  
    2.  **出力方向の要求値**、次の表は、新しいの推奨される認証方法の選択内容に応じて決まります入力 URI の既定値のいずれか、をクリックして**完了**、 をクリックし、 **ok**ルールを保存します。  
  
|実際の認証方法|対応する URI|  
|--------------------------------|---------------------|  
|ユーザー名とパスワードの認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password|  
|Windows 認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows|  
|X.509 証明書を使用する TLS 相互認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient|  
|X.509\-ベースの認証では、TLS を使用しません。|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509|  
![ルールを作成します。](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth3.PNG)
  
> [!NOTE]  
> テーブル内の値だけでなく、その他の URI 値を使用できます。 Ion 示されている URI 値、前の表では、既定では、証明書利用者が受け取る Uri が反映されます。  

## <a name="additional-references"></a>その他の参照情報 
[要求規則を構成します。](Configure-Claim-Rules.md)  
 
[チェックリスト:A Relying Party Trust の要求規則を作成します。](https://technet.microsoft.com/library/ee913578.aspx)  

[チェックリスト:要求規則の作成要求プロバイダー信頼します。](https://technet.microsoft.com/library/ee913564.aspx)  
  
[承認要求規則を使用する場合](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[要求の役割](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[要求規則の役割](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
