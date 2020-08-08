---
ms.assetid: 8c179884-f0d9-4c7a-973d-820119cf3c38
title: すべてのユーザーを許可する規則を作成する
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 6fa3500cc0343a7c341b2e94b011ce69f6bfbc04
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87967249"
---
# <a name="create-a-rule-to-permit-all-users"></a>すべてのユーザーを許可する規則を作成する

Windows Server 2016 では、 **Access Control ポリシー**を使用して、すべてのユーザーに証明書利用者へのアクセスを許可する規則を作成できます。  Windows Server 2012 R2 では、Active Directory フェデレーションサービス (AD FS) AD FS の [**すべてのユーザーを許可**する] 規則テンプレートを使用して、すべての \( \) ユーザーに証明書利用者へのアクセスを許可する承認規則を作成できます。

追加の承認規則を使用して、さらにアクセスを制限することができます。 ユーザーは、フェデレーション サービスから証明書利用者へのアクセスが許可されても、証明書利用者によってサービスが拒否される場合があります。

AD FS 管理スナップインを使用して要求規則を作成するには、次の手順を実行 \- します。

この手順を完了するには、ローカル コンピューター上の **Administrators** または同等のメンバーシップが最低限必要です。  適切なアカウントおよびグループメンバーシップの使用方法の詳細については、「[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)」を参照してください。

## <a name="to-create-a-rule-to-permit-all-users-in-windows-server-2016"></a>Windows Server 2016 のすべてのユーザーを許可するルールを作成するには

1.  サーバー マネージャーで、 **[ツール]** をクリックし、次に **[AD FS の管理]** を選択します。

2.  コンソールツリーの [ **AD FS**で、[**証明書利用者の信頼**] をクリックします。
![ルールの作成](media/Create-a-Rule-to-Permit-All-Users/permitall1.PNG)

3.  アクセスを許可する**証明書利用者信頼**を右クリックし、[ **Access Control ポリシーの編集**] を選択します。
![ルールの作成](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG)

4. [アクセス制御ポリシー] で、[**すべてのユーザーを許可**する] を選択し、[**適用**] と [ **Ok]** をクリックします。
![ルールの作成](media/Create-a-Rule-to-Permit-All-Users/permitall3.PNG)

## <a name="to-create-a-rule-to-permit-all-users-in-windows-server-2012-r2"></a>Windows Server 2012 R2 のすべてのユーザーを許可するルールを作成するには

1.  サーバー マネージャーで、 **[ツール]** をクリックし、次に **[AD FS の管理]** を選択します。

2.  コンソールツリーで、[ **AD FS の \\ 信頼関係] [ \\ 証明書利用者信頼**] の下にある一覧で、この規則を作成する特定の信頼をクリックします。

3.  \-選択した信頼を右クリックし、[**要求規則の編集**] をクリックします。
![ルールの作成](media/Create-a-Rule-to-Permit-All-Users/permitall4.PNG)

4.  [**要求規則の編集**] ダイアログボックスで、必要な承認規則の種類に基づいて [**発行承認規則**] タブまたは [**委任承認**規則] タブをクリックし、[ \( 規則の \) **追加**] をクリックして、**承認要求規則の追加ウィザード**を起動します。
![ルールの作成](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)
5.  [**規則テンプレートの選択**] ページの [**要求規則テンプレート**] で、[一覧から**すべてのユーザーを許可**する] を選択し、[**次へ**] をクリックします。
![ルールの作成](media/Create-a-Rule-to-Permit-All-Users/permitall6.PNG)
6.  [**規則の構成**] ページで、[**完了**] をクリックします。

7.  [**要求規則の編集**] ダイアログボックスで、[ **OK** ] をクリックして規則を保存します。

## <a name="additional-references"></a>その他の参照情報
[要求規則を構成する](Configure-Claim-Rules.md)

[チェックリスト:証明書利用者信頼の要求規則の作成](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ee913578(v=ws.11))

[承認要求規則を使用するタイミング](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)

[要求の役割](../../ad-fs/technical-reference/The-Role-of-Claims.md)

[要求規則の役割](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)
