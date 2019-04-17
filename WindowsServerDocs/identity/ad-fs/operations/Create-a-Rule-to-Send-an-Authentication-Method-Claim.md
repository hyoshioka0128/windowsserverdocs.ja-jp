---
ms.assetid: 96b9f4e6-f01c-4517-8299-017d187d447e
title: "認証方法の要求を送信する規則を作成します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4065a61e042f52298da656899289e718e010f932
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-rule-to-send-an-authentication-method-claim"></a>認証方法の要求を送信する規則を作成します。

>適用対象: Windows Server 2016、Windows Server 2012 R2

いずれかを使用することができます、**グループ メンバーシップを要求として送信**規則テンプレートまたは**入力方向の要求を変換**規則テンプレートの認証方法の要求を送信します。 証明書利用者は、認証方法の要求を使用して、ユーザーを使用して認証し、Active Directory フェデレーション サービス \(AD FS\) から信頼性情報を取得するログオン メカニズムを確認します。 状況は、証明書利用者のスマート カード ログオンに基づくアクセスのレベルを決定する認証メソッドの要求を生成するのに Windows Server 2012 R2 での入力として Active Directory フェデレーション サービス \(AD FS\) の認証メカニズム保証機能を使用することができますもします。 たとえば、開発者は、フェデレーション ユーザーの証明書利用者のパーティ製のアプリケーションに異なるレベルのアクセスを割り当てることができます。 アクセスのレベルは、ユーザーが、ユーザー名とパスワードの資格情報で、スマート カードではなくログオンするかどうかに基づいています。  
  
組織の要件に応じて、次の手順のいずれかの手順に従います。  
  
-   この規則の作成を使用して、**グループ メンバーシップを要求として送信**ルール テンプレート \-最終的にどのような認証方法を決定するには、このテンプレートで指定したグループの要求を発行する場合は、この規則テンプレートを使用することができます。  
  
-   この規則の作成を使用して、**入力方向の要求を変換**規則テンプレート \-標準的な AD FS 認証メソッドの要求で認識されない製品と連動する新しい認証方法を既存の認証方法を変更する場合は、この規則テンプレートを使用することができます。  
  


## <a name="to-create-by-using-the-send-group-membership-as-claims-rule-template-on-a-relying-party-trust-in-windows-server-2016"></a>A Relying Party Trust Windows Server 2016 での要求規則テンプレートとグループ メンバーシップの送信を使用して作成するには 

1.  サーバー マネージャーで、クリックして**ツール**、し、[ **AD FS 管理**します。  
  
2.  コンソール ツリーで、[ **AD FS**、] をクリックして**証明書利用者信頼**します。 
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  選択した信頼を右クリックし、クリック**要求発行ポリシーの編集**します。
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  **要求発行ポリシーの編集**ダイアログ ボックスで、**発行変換規則**] をクリックして**規則の追加**規則ウィザードを開始します。 
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  **規則テンプレートの選択**ページで、**要求規則テンプレート**[**グループ メンバーシップを要求として送信**クリックして、一覧から**[次へ]**します。  
![規則を作成します。](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group3.PNG)      

6.  **規則の構成**] ページで、要求規則名を入力します。  
  
7.  をクリックして**参照**、グループのメンバーを含むがこの認証方法の要求を受信する必要があります、クリックして選択**OK**します。  
  
8.  **出力方向の要求の種類**[**認証方法**一覧にします。  
  
9. **出力方向の要求の値**、推奨される認証方法によっては、次の表に、既定の統一リソース識別子 \(URI\) 値のいずれかを入力でクリックし、**完了**、] をクリックし、 **[ok]**に規則を保存します。  
  
|実際の認証方法|対応する URI|  
|--------------------------------|---------------------|  
|ユーザー名とパスワードの認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password|  
|Windows 認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows|  
|トランスポート層セキュリティ \(TLS\) 相互認証 X.509 証明書を使用します。|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient|  
|TLS を使用しない X.509\ ベースの認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509|  
![規則を作成します。](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth2.PNG)
  
## <a name="to-create-by-using-the-send-group-membership-as-claims-rule-template-on-a-claims-provider-trust-in-windows-server-2016"></a>Windows Server 2016 での要求プロバイダー信頼の要求規則テンプレートとグループ メンバーシップの送信を使用して作成するには 
  
1.  サーバー マネージャーで、クリックして**ツール**、し、[ **AD FS 管理**します。  
  
2.  コンソール ツリーで、[ **AD FS**、] をクリックして**要求プロバイダー信頼**します。 
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  選択した信頼を右クリックし、クリック**要求規則の編集**します。
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  **要求規則の編集**ダイアログ ボックスで、**受け付け変換規則**] をクリックして**規則の追加**規則ウィザードを開始します。
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  **規則テンプレートの選択**ページで、**要求規則テンプレート**[**グループ メンバーシップを要求として送信**クリックして、一覧から**[次へ]**します。  
![規則を作成します。](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group3.PNG)     

6.  **規則の構成**] ページで、要求規則名を入力します。  
  
7.  をクリックして**参照**、グループのメンバーを含むがこの認証方法の要求を受信する必要があります、クリックして選択**OK**します。  
  
8.  **出力方向の要求の種類**[**認証方法**一覧にします。  
  
9. **出力方向の要求の値**、推奨される認証方法によっては、次の表に、既定の統一リソース識別子 \(URI\) 値のいずれかを入力でクリックし、**完了**、] をクリックし、 **[ok]**に規則を保存します。  
  
|実際の認証方法|対応する URI|  
|--------------------------------|---------------------|  
|ユーザー名とパスワードの認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password|  
|Windows 認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows|  
|トランスポート層セキュリティ \(TLS\) 相互認証 X.509 証明書を使用します。|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient|  
|TLS を使用しない X.509\ ベースの認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509|  
![規則を作成します。](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth2.PNG)


## <a name="to-create-this-rule-by-using-the-transform-an-incoming-claim-rule-template-on-a-relying-party-trust-in-windows-server-2016"></a>入力方向の要求規則テンプレートの a Relying Party Trust Windows Server 2016 でのトランス フォームを使用してこのルールを作成するには 

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
  
7.  **入力方向の要求の種類**[**認証方法**一覧にします。  
  
8.  **出力方向の要求の種類**[**認証方法**一覧にします。  
  
9. 選択**入力方向の要求の値を異なる出力方向の要求の値に置き換えて**、し、次の操作を行います。  
  
    1.  **入力方向の要求値**ベース実際の認証方法が最初に使用できる URI では、次の URI 値のいずれかのように入力でクリックし、**完了**、] をクリックし、 **[ok]**に規則を保存します。  
  
    2.  **出力方向の要求の値**URI の既定値のいずれかを次の表に、推奨される認証方法に関する新しい好みに依存しています入力でクリックし、**完了**、] をクリックし、 **[ok]**に規則を保存します。  
  
|実際の認証方法|対応する URI|  
|--------------------------------|---------------------|  
|ユーザー名とパスワードの認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password|  
|Windows 認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows|  
|X.509 証明書を使って TLS 相互認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient|  
|TLS を使用しない X.509\ ベースの認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509|  
![規則を作成します。](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth4.PNG)
  
> [!NOTE]  
> テーブル内の値だけでなく、その他の URI の値を使用できます。 イオンに表示される URI 値、前の表では、既定では、証明書利用者を受け入れる Uri が反映されます。  

## <a name="to-create-this-rule-by-using-the-transform-an-incoming-claim-rule-template-on-a-claims-provider-trust-in-windows-server-2016"></a>入力方向の要求規則テンプレートの Windows Server 2016 での要求プロバイダー信頼のトランス フォームを使用してこのルールを作成するには 
  
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
  
7.  **入力方向の要求の種類**[**認証方法**一覧にします。  
  
8.  **出力方向の要求の種類**[**認証方法**一覧にします。  
  
9. 選択**入力方向の要求の値を異なる出力方向の要求の値に置き換えて**、し、次の操作を行います。  
  
    1.  **入力方向の要求値**ベース実際の認証方法が最初に使用できる URI では、次の URI 値のいずれかのように入力でクリックし、**完了**、] をクリックし、 **[ok]**に規則を保存します。  
  
    2.  **出力方向の要求の値**URI の既定値のいずれかを次の表に、推奨される認証方法に関する新しい好みに依存しています入力でクリックし、**完了**、] をクリックし、 **[ok]**に規則を保存します。  
  
|実際の認証方法|対応する URI|  
|--------------------------------|---------------------|  
|ユーザー名とパスワードの認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password|  
|Windows 認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows|  
|X.509 証明書を使って TLS 相互認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient|  
|TLS を使用しない X.509\ ベースの認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509|  
![規則を作成します。](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth4.PNG)























## <a name="to-create-this-rule-by-using-the-send-group-membership-as-claims-rule-template-in-windows-server-2012-r2"></a>Windows Server 2012 R2 での要求規則テンプレートとして、[グループのメンバーシップの送信を使用してこのルールを作成するには  
  
1.  サーバー マネージャーで、クリックして**ツール**、し、[ **AD FS 管理**します。  
  
2.  コンソール ツリーで、下にある**AD FS\\Trust 関係**、] をクリックするか**要求プロバイダー信頼**または**証明書利用者信頼**、この規則を作成するリスト内の特定の信頼をクリックします。  
  
3.  選択した信頼を右クリックし、クリック**要求規則の編集**します。
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)  
  
4.  **要求規則の編集**ダイアログ ボックスで、1 つに、次のタブを選択、信頼関係を編集しているし、どの規則を設定することによって、この規則の作成にして] をクリックして**規則の追加**するルール セットに関連付けられている規則のウィザードを開始します。  
  
    -   **受け入れ変換規則**  
  
    -   **発行変換規則**  
  
    -   **発行承認規則**  
  
    -   **委任承認規則**  
![規則を作成します。](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)
    
5.  **規則テンプレートの選択**ページで、**要求規則テンプレート**[**グループ メンバーシップを要求として送信**クリックして、一覧から**[次へ]**します。  
![規則を作成します。](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group1.PNG)
  
6.  **規則の構成**] ページで、要求規則名を入力します。  
  
7.  をクリックして**参照**、グループのメンバーを含むがこの認証方法の要求を受信する必要があります、クリックして選択**OK**します。  
  
8.  **出力方向の要求の種類**[**認証方法**一覧にします。  
  
9. **出力方向の要求の値**、推奨される認証方法によっては、次の表に、既定の統一リソース識別子 \(URI\) 値のいずれかを入力でクリックし、**完了**、] をクリックし、 **[ok]**に規則を保存します。  
  
|実際の認証方法|対応する URI|  
|--------------------------------|---------------------|  
|ユーザー名とパスワードの認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password|  
|Windows 認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows|  
|トランスポート層セキュリティ \(TLS\) 相互認証 X.509 証明書を使用します。|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient|  
|TLS を使用しない X.509\ ベースの認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509|  
![規則を作成します。](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth1.PNG)
 
> [!NOTE]  
> テーブル内の値だけでなく、その他の URI の値を使用できます。 前の表に示す URI 値は、既定では、証明書利用者を受け入れる Uri を反映します。  
  
## <a name="to-create-this-rule-by-using-the-transform-an-incoming-claim-rule-template-in-windows-server-2012-r2"></a>ルールを作成するこのトランス フォームを使用して入力方向の要求規則テンプレートでは、Windows Server 2012 R2  
   
  
  
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
  
7.  **入力方向の要求の種類**[**認証方法**一覧にします。  
  
8.  **出力方向の要求の種類**[**認証方法**一覧にします。  
  
9. 選択**入力方向の要求の値を異なる出力方向の要求の値に置き換えて**、し、次の操作を行います。  
  
    1.  **入力方向の要求値**ベース実際の認証方法が最初に使用できる URI では、次の URI 値のいずれかのように入力でクリックし、**完了**、] をクリックし、 **[ok]**に規則を保存します。  
  
    2.  **出力方向の要求の値**URI の既定値のいずれかを次の表に、推奨される認証方法に関する新しい好みに依存しています入力でクリックし、**完了**、] をクリックし、 **[ok]**に規則を保存します。  
  
|実際の認証方法|対応する URI|  
|--------------------------------|---------------------|  
|ユーザー名とパスワードの認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password|  
|Windows 認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows|  
|X.509 証明書を使って TLS 相互認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient|  
|TLS を使用しない X.509\ ベースの認証|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509|  
![規則を作成します。](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth3.PNG)
  
> [!NOTE]  
> テーブル内の値だけでなく、その他の URI の値を使用できます。 イオンに表示される URI 値、前の表では、既定では、証明書利用者を受け入れる Uri が反映されます。  

## <a name="additional-references"></a>その他の参照 
[要求規則を構成します。](Configure-Claim-Rules.md)  
 
[チェックリスト: 証明書利用者のパーティ信頼の要求規則を作成します。](https://technet.microsoft.com/library/ee913578.aspx)  

[チェックリスト: Creating Claim Rules for 要求プロバイダー信頼します。](https://technet.microsoft.com/library/ee913564.aspx)  
  
[When to Use an Authorization Claim Rule](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[要求の役割](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[要求規則の役割](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
