---
ms.assetid: 66664b80-2590-46c0-bfca-82402088e42c
title: 要求として LDAP 属性を送信するルールを作成します。
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 00ea4f9f868b9c82c2a0859be971db26394251a3
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189350"
---
# <a name="create-a-rule-to-send-ldap-attributes-as-claims"></a>要求として LDAP 属性を送信するルールを作成します。


Active Directory フェデレーション サービスで要求規則テンプレートとして送信 LDAP 属性を使用して\(AD FS\)、ライトウェイト ディレクトリ アクセス プロトコルからの属性を選択するルールを作成する\(LDAP\)証明書利用者に要求として送信する、Active Directory などの属性ストアです。 たとえば、この規則テンプレートを使用して要求規則から認証されたユーザーの属性値が抽出するように a Send LDAP Attributes を作成することができます、 **displayName**と**telephoneNumber** Activeディレクトリは、属性し、2 つの異なる出力方向の要求としてそれらの値を送信します。  
  
また、この規則を使用して、すべてのユーザーのグループ メンバーシップを送信することもできます。 個々のグループのメンバーシップのみを送信する場合は、"グループ メンバーシップを要求として送信" 規則テンプレートを使用します。 次の手順を使用するには、AD FS 管理スナップインで要求規則を作成する\-でします。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。  

## <a name="to-create-a-rule-to-send-ldap-attributes-as-claims-for-a-relying-party-trust-in-windows-server-2016"></a>証明書利用者の信頼を Windows Server 2016 での要求として LDAP 属性を送信するルールを作成するには 

1.  サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  
  
2.  コンソール ツリーで [ **AD FS**、] をクリックして**証明書利用者信頼**します。 
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  右\-選択の信頼をクリックし、クリックして**要求発行ポリシーの編集**します。
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  **要求発行ポリシーの編集**ダイアログ ボックスで、**発行変換規則** をクリックして**規則の追加**ルール ウィザードを開始します。 
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  **規則テンプレートの選択** ページ **要求規則テンプレート**を選択します**要求として LDAP 属性を送信** をクリックし、一覧から **次へ** .  
![ルールを作成します。](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap1.PNG)    

6.  **規則の構成**ページ**要求規則名**この規則の表示名を入力、**属性ストア**、LDAP 属性を選択して、マップ、発信要求の種類。 
![ルールを作成します。](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap2.PNG)    

7.  をクリックして、**完了**ボタンをクリックします。  
  
8.  **要求規則の編集**ダイアログ ボックスで、をクリックして **[ok]** ルールを保存します。
  
## <a name="to-create-a-rule-to-send-ldap-attributes-as-claims-for-a-claims-provider-trust-in-windows-server-2016"></a>Windows Server 2016 での要求プロバイダー信頼の要求として LDAP 属性を送信するルールを作成するには 
  
1.  サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  
  
2.  コンソール ツリーで [ **AD FS**、] をクリックして**要求プロバイダー信頼**します。 
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  右\-選択の信頼をクリックし、クリックして**要求規則の編集**します。
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  **要求規則の編集**ダイアログ ボックスで、**受け入れ変換規則** をクリックして**規則の追加**ルール ウィザードを開始します。
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  **規則テンプレートの選択** ページ **要求規則テンプレート**を選択します**要求として LDAP 属性を送信** をクリックし、一覧から **次へ** .  
![ルールを作成します。](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap1.PNG)       

6.  **規則の構成**ページ**要求規則名**この規則の表示名を入力、**属性ストア**、LDAP 属性を選択して、マップ、発信要求の種類。 
![ルールを作成します。](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap2.PNG)      

7.  をクリックして、**完了**ボタンをクリックします。  
  
8.  **要求規則の編集**ダイアログ ボックスで、をクリックして **[ok]** ルールを保存します。  

 
  
## <a name="to-create-a-rule-to-send-ldap-attributes-as-claims-for-windows-server-2012-r2"></a>Windows Server 2012 R2 の要求として LDAP 属性を送信するルールを作成するには  
  
1.  サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  
  
2.  コンソール ツリーで [ **AD FSAD FS\\信頼関係**、いずれかをクリックします**要求プロバイダー信頼**または**証明書利用者信頼**、] をクリックし、このルールを作成する一覧で特定の信頼します。  
  
3.  右\-選択の信頼をクリックし、クリックして**要求規則の編集**します。
![ルールを作成します。](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)  
  
4.  **要求規則の編集**ダイアログ ボックスで、1 つに、次のタブを選択、信頼関係を編集して、どのルールを設定することによって、この規則を作成して順にクリックします**規則の追加**ルールを開始するにはその規則セットに関連付けられているウィザード:  
  
    -   **受け入れ変換規則**  
  
    -   **発行変換規則**  
  
    -   **発行承認規則**  
  
    -   **委任承認規則**  
![ルールを作成します。](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG) 
  
5.  **規則テンプレートの選択** ページ **要求規則テンプレート**を選択します**要求として LDAP 属性を送信** をクリックし、一覧から **次へ** .  
![ルールを作成します。](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap3.PNG)  
  
6.  **規則の構成**ページ**要求規則名**で、この規則の表示名を入力**属性ストア**選択**Active Directory**、し、**マッピングの LDAP 属性と出力方向の要求の種類**目的**LDAP 属性**と対応する**出力方向の要求の種類**ドロップダウンから型\-リストします。  
  
    このルールの一部としての要求を発行する Active Directory 属性ごとに別の行を発信のクレーム型のペアを新しい LDAP 属性を選択する必要があります。  
![ルールを作成します。](media/Create-a-Rule-to-Send-LDAP-Attributes-as-Claims/ldap4.PNG)    
7.  をクリックして、**完了**ボタンをクリックします。  
  
8.  **要求規則の編集**ダイアログ ボックスで、をクリックして **[ok]** ルールを保存します。  

## <a name="additional-references"></a>その他の参照情報 
[要求規則を構成する](Configure-Claim-Rules.md)  
 
[チェックリスト:証明書利用者信頼の要求規則の作成](https://technet.microsoft.com/library/ee913578.aspx)  

[チェックリスト:要求プロバイダー信頼の要求規則の作成](https://technet.microsoft.com/library/ee913564.aspx)  
  
[承認要求規則を使用する場合](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[要求の役割](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[要求規則の役割](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
