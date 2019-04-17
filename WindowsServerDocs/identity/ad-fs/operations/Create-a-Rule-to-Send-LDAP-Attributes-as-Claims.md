---
ms.assetid: 66664b80-2590-46c0-bfca-82402088e42c
title: "LDAP 属性を要求として送信する規則を作成します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e9762e4bc50a1c2b862999af5269a0da376ec9a1
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-rule-to-send-ldap-attributes-as-claims"></a>LDAP 属性を要求として送信する規則を作成します。

>適用対象: Windows Server 2016、Windows Server 2012 R2

Active Directory フェデレーション サービス \(AD FS\) で要求規則テンプレートとして LDAP 属性の送信を使用して、Active Directory は、証明書利用者に要求として送信するなど、Lightweight Directory Access Protocol \(LDAP\) 属性ストアから属性を選択しの規則を作成できます。 たとえば、この規則テンプレートを使用して要求規則から認証済みユーザーの属性値を抽出するは、a Send LDAP Attributes を作成することができます、 **displayName**と**telephoneNumber** Active Directory 属性し、これらの値を 2 つの異なる出力方向の要求として送信します。  
  
すべてのユーザーのグループ メンバーシップを送信するのにこの規則を使用することもできます。 個々 のグループのメンバーシップのみを送信する場合は、要求規則テンプレートとグループ メンバーシップの送信を使用します。 次の手順を使用するには、AD FS 管理スナップインの要求規則の作成をします。  
  
メンバーシップ**管理者**、相当するもので、ローカル コンピューターでは、この手順を完了するために必要な最低限またはします。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。  

## <a name="to-create-a-rule-to-send-ldap-attributes-as-claims-for-a-relying-party-trust-in-windows-server-2016"></a>A Relying Party Trust Windows Server 2016 での要求として LDAP 属性を送信する規則を作成するには 

1.  サーバー マネージャーで、クリックして**ツール**、し、[ **AD FS 管理**します。  
  
2.  コンソール ツリーで、[ **AD FS**、] をクリックして**証明書利用者信頼**します。 
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  選択した信頼を右クリックし、クリック**要求発行ポリシーの編集**します。
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  **要求発行ポリシーの編集**ダイアログ ボックスで、**発行変換規則**] をクリックして**規則の追加**規則ウィザードを開始します。 
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  **規則テンプレートの選択**ページで、**要求規則テンプレート**[ **LDAP 属性を要求として送信**クリックして、一覧から**[次へ]**します。  
![規則を作成します。](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap1.PNG)    

6.  **規則の構成**] ページの [**要求規則名**この規則の表示名を入力、**属性ストア**、LDAP 属性を選択して、出力方向の要求の種類にマップします。 
![規則を作成します。](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap2.PNG)    

7.  をクリックして、**完了**ボタンをクリックします。  
  
8.  **要求規則の編集**ダイアログ ボックスで、] をクリックして**OK**に規則を保存します。
  
## <a name="to-create-a-rule-to-send-ldap-attributes-as-claims-for-a-claims-provider-trust-in-windows-server-2016"></a>Windows Server 2016 での要求プロバイダー信頼の要求として LDAP 属性を送信する規則を作成するには 
  
1.  サーバー マネージャーで、クリックして**ツール**、し、[ **AD FS 管理**します。  
  
2.  コンソール ツリーで、[ **AD FS**、] をクリックして**要求プロバイダー信頼**します。 
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  選択した信頼を右クリックし、クリック**要求規則の編集**します。
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  **要求規則の編集**ダイアログ ボックスで、**受け付け変換規則**] をクリックして**規則の追加**規則ウィザードを開始します。
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  **規則テンプレートの選択**ページで、**要求規則テンプレート**[ **LDAP 属性を要求として送信**クリックして、一覧から**[次へ]**します。  
![規則を作成します。](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap1.PNG)       

6.  **規則の構成**] ページの [**要求規則名**この規則の表示名を入力、**属性ストア**、LDAP 属性を選択して、出力方向の要求の種類にマップします。 
![規則を作成します。](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap2.PNG)      

7.  をクリックして、**完了**ボタンをクリックします。  
  
8.  **要求規則の編集**ダイアログ ボックスで、] をクリックして**OK**に規則を保存します。  

 
  
## <a name="to-create-a-rule-to-send-ldap-attributes-as-claims-for-windows-server-2012-r2"></a>Windows Server 2012 R2 の要求として LDAP 属性を送信する規則を作成するには  
  
1.  サーバー マネージャーで、クリックして**ツール**、し、[ **AD FS 管理**します。  
  
2.  コンソール ツリーで、下にある**AD FSAD FS\\Trust 関係**、] をクリックするか**要求プロバイダー信頼**または**証明書利用者信頼**、この規則を作成するリスト内の特定の信頼をクリックします。  
  
3.  選択した信頼を右クリックし、クリック**要求規則の編集**します。
![規則を作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)  
  
4.  **要求規則の編集**ダイアログ ボックスで、1 つに、次のタブを選択、信頼関係を編集しているし、どの規則を設定することによって、この規則の作成にして] をクリックして**規則の追加**するルール セットに関連付けられている規則のウィザードを開始します。  
  
    -   **受け入れ変換規則**  
  
    -   **発行変換規則**  
  
    -   **発行承認規則**  
  
    -   **委任承認規則**  
![規則を作成します。](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG) 
  
5.  **規則テンプレートの選択**ページで、**要求規則テンプレート**[ **LDAP 属性を要求として送信**クリックして、一覧から**[次へ]**します。  
![規則を作成します。](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap3.PNG)  
  
6.  **規則の構成**] ページの [**要求規則名**下にある、この規則の表示名を入力**属性ストア**選択**Active Directory**、し、[**マッピングの LDAP 属性と出力方向の要求の種類**目的**LDAP 属性**と対応する**出力方向の要求の種類**ドロップダウン リストから種類。  
  
    新しい LDAP 属性と出力方向の要求の種類ペアにこの規則の一部としての要求を発行する Active Directory 属性ごとに別の行を選択する必要があります。  
![規則を作成します。](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap4.PNG)    
7.  をクリックして、**完了**ボタンをクリックします。  
  
8.  **要求規則の編集**ダイアログ ボックスで、] をクリックして**OK**に規則を保存します。  

## <a name="additional-references"></a>その他の参照 
[要求規則を構成します。](Configure-Claim-Rules.md)  
 
[チェックリスト: 証明書利用者のパーティ信頼の要求規則を作成します。](https://technet.microsoft.com/library/ee913578.aspx)  

[チェックリスト: Creating Claim Rules for 要求プロバイダー信頼します。](https://technet.microsoft.com/library/ee913564.aspx)  
  
[When to Use an Authorization Claim Rule](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[要求の役割](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[要求規則の役割](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
