---
ms.assetid: 7d230527-f4fe-4572-8838-0b354ee0b06b
title: 要求記述を追加する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 00ae720a933289e3cd4bde5fe9d20610e38ae726
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70866036"
---
# <a name="add-a-claim-description"></a>要求記述を追加する


アカウントパートナー組織では、管理者は、グループまたはロールのユーザーのメンバーシップを表すクレームを作成するか、ユーザーに関するデータ (ユーザーの従業員識別番号など) を表すことができます。

リソースパートナー組織では、管理者は対応する要求を作成して、リソースユーザーとして認識できるグループとユーザーを表します。 アカウントパートナー組織内の出力方向の要求は、リソースパートナー組織内の入力方向の要求にマップされるため、リソースパートナーは、アカウントパートナーが提供する資格情報を受け入れることができます。 

要求を追加するには、次の手順を実行します。

この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。

## <a name="to-add-a-claim-description"></a>要求の説明を追加するには

1. サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** を選択します。 

2. **[サービス]** を展開し、右側の **[要求の説明の追加]** をクリックします。
   ![要求の説明の追加](media/Add-a-Claim-Description/claimdesc1.png)

3. 要求の説明の追加 ダイアログボックスの **表示名** に、この要求のグループまたはロールを識別する一意の名前を入力します。

4. **短い名前**を追加します。

5. **[要求識別子]** に、使用する要求のグループまたはロールに関連付けられている URI を入力します。

6. **[説明]** に、この要求の目的に最も適したテキストを入力します。

7. 組織のニーズに応じて、次のいずれかのチェックボックスをオンにして、この要求をフェデレーションメタデータに発行します。


~~~
- To publish this claim to make partners aware that this server can accept this claim, click **Publish this claim in federation metadata as a claim type that this Federation Service can accept**.
- To publish this claim to make partners aware that this server can issue this claim, click **Publish this claim in federation metadata as a claim type that this Federation Service can send**.
~~~

8. **[OK]** をクリックします。

![要求の説明の追加](media/Add-a-Claim-Description/claimdesc2.png)


## <a name="see-also"></a>関連項目  
[AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md) 
