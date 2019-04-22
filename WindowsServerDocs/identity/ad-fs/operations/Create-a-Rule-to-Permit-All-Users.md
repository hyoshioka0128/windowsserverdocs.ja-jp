---
ms.assetid: 8c179884-f0d9-4c7a-973d-820119cf3c38
title: すべてのユーザーを許可する規則を作成する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: de85af27e699242977054420178dd3c424b2ddb3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822593"
---
# <a name="create-a-rule-to-permit-all-users"></a>すべてのユーザーを許可する規則を作成する

>適用先:Windows Server 2016、Windows Server 2012 R2

Windows Server 2016 で使用することができます、**アクセス制御ポリシー**ルールはすべてのユーザーにアクセスできるように、証明書利用者を作成します。  Windows Server 2012 R2 でを使用して、**すべてのユーザーを許可**規則テンプレートの Active Directory フェデレーション サービスで\(AD FS\)はすべてのユーザーにアクセスできるように、証明書利用者する承認規則を作成します。パーティです。 

追加の承認規則を使用して、さらにアクセスを制限することができます。 ユーザーは、フェデレーション サービスから証明書利用者へのアクセスが許可されても、証明書利用者によってサービスが拒否される場合があります。  
  
次の手順を使用するには、AD FS 管理スナップインで要求規則を作成する\-でします。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。 

## <a name="to-create-a-rule-to-permit-all-users-in-windows-server-2016"></a>Windows Server 2016 ですべてのユーザーを許可する規則を作成するには

1.  サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  
  
2.  コンソール ツリーで [ **AD FS**、] をクリックして**証明書利用者信頼**します。 
![ルールを作成します。](media/Create-a-Rule-to-Permit-All-Users/permitall1.PNG)

3.  右クリックし、 **Relying Party Trust**へのアクセスを許可しを選択したい**アクセス制御ポリシーの編集**します。  
![ルールを作成します。](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG)

4. アクセス制御ポリシーを選択**のすべてのユーザーに許可**順にクリックします**適用**と**Ok**します。
![ルールを作成します。](media/Create-a-Rule-to-Permit-All-Users/permitall3.PNG)
  
## <a name="to-create-a-rule-to-permit-all-users-in-windows-server-2012-r2"></a>Windows Server 2012 R2 のすべてのユーザーを許可する規則を作成するには 
  
1.  サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  
  
2.  コンソール ツリーで  **AD FS\\信頼関係\\証明書利用者信頼**、この規則を作成するリスト内の特定の信頼をクリックします。  

3.  右\-選択の信頼をクリックし、クリックして**要求規則の編集**します。  
![ルールを作成します。](media/Create-a-Rule-to-Permit-All-Users/permitall4.PNG)  

4.  **要求規則の編集**ダイアログ ボックスで、をクリックして、**発行承認規則の** タブまたは**委任承認規則**タブ\(の種類に基づく必要な承認規則\)、 をクリックし、**規則の追加**を開始する、**承認の要求規則の追加ウィザード**。  
![ルールを作成します。](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)  
5.  **規則テンプレートの選択** ページ **要求規則テンプレート**を選択します**すべてのユーザーを許可** をクリックし、一覧から**次**します。  
![ルールを作成します。](media/Create-a-Rule-to-Permit-All-Users/permitall6.PNG)    
6.  **規則の構成**] ページで [**完了**します。  
  
7.  **要求規則の編集**ダイアログ ボックスで、をクリックして **[ok]** ルールを保存します。  

## <a name="additional-references"></a>その他の参照情報 
[要求規則を構成します。](Configure-Claim-Rules.md)  
 
[チェックリスト:A Relying Party Trust の要求規則を作成します。](https://technet.microsoft.com/library/ee913578.aspx)  
  
[承認要求規則を使用する場合](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[要求の役割](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[要求規則の役割](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
