---
ms.assetid: 8c179884-f0d9-4c7a-973d-820119cf3c38
title: すべてのユーザーを許可する規則を作成する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 1356218c5f9f47073f007286e8acfdf4c3608b73
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407623"
---
# <a name="create-a-rule-to-permit-all-users"></a>すべてのユーザーを許可する規則を作成する

Windows Server 2016 では、 **Access Control ポリシー**を使用して、すべてのユーザーに証明書利用者へのアクセスを許可する規則を作成できます。  Windows Server 2012 R2 では、Active Directory フェデレーションサービス (AD FS) \( AD FS @ no__t の**すべてのユーザーを許可**する規則テンプレートを使用して、すべてのユーザーに証明書利用者へのアクセスを許可する承認規則を作成できます。 

追加の承認規則を使用して、さらにアクセスを制限することができます。 ユーザーは、フェデレーション サービスから証明書利用者へのアクセスが許可されても、証明書利用者によってサービスが拒否される場合があります。  
  
次の手順に従って、の AD FS 管理スナップイン @ no__t を使用して要求規則を作成できます。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。 

## <a name="to-create-a-rule-to-permit-all-users-in-windows-server-2016"></a>Windows Server 2016 のすべてのユーザーを許可するルールを作成するには

1.  サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** を選択します。  
  
2.  コンソールツリーの  **AD FS**で、**証明書利用者の信頼** をクリックします。 
![ルールの作成](media/Create-a-Rule-to-Permit-All-Users/permitall1.PNG)

3.  アクセスを許可する**証明書利用者信頼**を右クリックし、 **[Access Control ポリシーの編集]** を選択します。  
![ルールの作成](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG)

4. アクセス制御ポリシー で、**すべてのユーザーを許可**する を選択し、**適用** と  **Ok**をクリックします。
![ルールの作成](media/Create-a-Rule-to-Permit-All-Users/permitall3.PNG)
  
## <a name="to-create-a-rule-to-permit-all-users-in-windows-server-2012-r2"></a>Windows Server 2012 R2 のすべてのユーザーを許可するルールを作成するには 
  
1.  サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** を選択します。  
  
2.  コンソールツリーで、[ **\\AD FS の信頼関係\\] [証明書利用者信頼**] の下にある一覧で、この規則を作成する特定の信頼をクリックします。  

3.  選択\-した信頼を右クリックし、 **[要求規則の編集]** をクリックします。  
![ルールの作成](media/Create-a-Rule-to-Permit-All-Users/permitall4.PNG)  

4.  **要求規則の編集** ダイアログボックスで、必要\)な承認規則の種類に基づいて  \(**発行承認規則** タブまたは **委任承認**規則 タブをクリックし、規則の追加 をクリックします。を実行して、**承認要求規則の追加ウィザード**を開始します。  
![ルールの作成](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)  
5.  **[規則テンプレートの選択]** ページの **[要求規則テンプレート]** で、一覧から **[すべてのユーザーを許可]** する を選択し、 **[次へ]** をクリックします。  
![ルールの作成](media/Create-a-Rule-to-Permit-All-Users/permitall6.PNG)    
6.  **[規則の構成]** ページで、 **[完了]** をクリックします。  
  
7.  **[要求規則の編集]** ダイアログボックスで、 **[OK]** をクリックして規則を保存します。  

## <a name="additional-references"></a>その他の参照情報 
[要求規則を構成する](Configure-Claim-Rules.md)  
 
[チェックリスト:証明書利用者信頼の要求規則の作成](https://technet.microsoft.com/library/ee913578.aspx)  
  
[承認要求規則を使用する場合](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[要求の役割](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[要求規則の役割](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
