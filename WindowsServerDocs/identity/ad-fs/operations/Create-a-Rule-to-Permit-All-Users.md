---
ms.assetid: 8c179884-f0d9-4c7a-973d-820119cf3c38
title: "すべてのユーザーを許可する規則を作成します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: de85af27e699242977054420178dd3c424b2ddb3
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-rule-to-permit-all-users"></a>すべてのユーザーを許可する規則を作成します。

>適用対象: Windows Server 2016、Windows Server 2012 R2

Windows Server 2016 で使用することができます、**アクセス制御ポリシー**はすべてのユーザーにアクセスできるように、証明書利用者規則を作成します。  Windows Server 2012 R2 でを使用して、**すべてのユーザーを許可**で Active Directory フェデレーション サービス \(AD FS\) 規則テンプレートはすべてのユーザーにアクセスできるように、証明書利用者を承認規則を作成することができます。 

さらにアクセスを制限するのに追加の承認規則を使用することができます。 ユーザーは、フェデレーション サービスから証明書利用者にアクセスする許可されている可能性がありますもによって拒否されるサービス証明書利用者のパーティします。  
  
次の手順を使用すると、AD FS 管理スナップインの要求規則の作成します。  
  
メンバーシップ**管理者**、相当するもので、ローカル コンピューターでは、この手順を完了するために必要な最低限またはします。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。 

## <a name="to-create-a-rule-to-permit-all-users-in-windows-server-2016"></a>Windows Server 2016 でのすべてのユーザーを許可する規則を作成するには

1.  サーバー マネージャーで、クリックして**ツール**、し、[ **AD FS 管理**します。  
  
2.  コンソール ツリーで、[ **AD FS**、] をクリックして**証明書利用者信頼**します。 
![規則を作成します。](media/Create-a-Rule-to-Permit-All-Users/permitall1.PNG)

3.  右クリックし、 **Relying Party Trust**へのアクセス許可を選択する**アクセス制御ポリシーの編集**します。  
![規則を作成します。](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG)

4. アクセス制御ポリシー] を選択**すべてのユーザーに許可**] をクリックし、**適用**と**Ok**します。
![規則を作成します。](media/Create-a-Rule-to-Permit-All-Users/permitall3.PNG)
  
## <a name="to-create-a-rule-to-permit-all-users-in-windows-server-2012-r2"></a>Windows Server 2012 R2 のすべてのユーザーを許可する規則を作成するには 
  
1.  サーバー マネージャーで、クリックして**ツール**、し、[ **AD FS 管理**します。  
  
2.  コンソール ツリーで、[ **AD FS\\Trust Relationships\\Relying パーティー信頼**、この規則を作成するリスト内の特定の信頼をクリックします。  

3.  選択した信頼を右クリックし、クリック**要求規則の編集**します。  
![規則を作成します。](media/Create-a-Rule-to-Permit-All-Users/permitall4.PNG)  

4.  **要求規則の編集**ダイアログ ボックスで、] をクリックして、**発行承認規則**] タブまたは**委任承認規則**] タブの [\ (に基づいて承認規則の種類を require\)、] をクリックし、**規則の追加**を開始する、**承認の要求規則の追加ウィザード**します。  
![規則を作成します。](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)  
5.  **規則テンプレートの選択**ページで、**要求規則テンプレート**[**すべてのユーザーを許可**クリックして、一覧から**[次へ]**します。  
![規則を作成します。](media/Create-a-Rule-to-Permit-All-Users/permitall6.PNG)    
6.  **規則の構成**] ページで [**完了**します。  
  
7.  **要求規則の編集**ダイアログ ボックスで、] をクリックして**OK**に規則を保存します。  

## <a name="additional-references"></a>その他の参照 
[要求規則を構成します。](Configure-Claim-Rules.md)  
 
[チェックリスト: 証明書利用者のパーティ信頼の要求規則を作成します。](https://technet.microsoft.com/library/ee913578.aspx)  
  
[When to Use an Authorization Claim Rule](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[要求の役割](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[要求規則の役割](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
