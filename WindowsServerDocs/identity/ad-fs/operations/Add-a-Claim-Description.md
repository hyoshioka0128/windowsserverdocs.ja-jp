---
ms.assetid: 7d230527-f4fe-4572-8838-0b354ee0b06b
title: 要求記述を追加する
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: a022ec618c7255021cd424120330671e007a658a
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86962704"
---
# <a name="add-a-claim-description"></a>要求記述を追加する


アカウントパートナー組織では、管理者は、グループまたはロールのユーザーのメンバーシップを表すクレームを作成するか、ユーザーに関するデータ (ユーザーの従業員識別番号など) を表すことができます。

リソースパートナー組織では、管理者は対応する要求を作成して、リソースユーザーとして認識できるグループとユーザーを表します。 アカウントパートナー組織内の出力方向の要求は、リソースパートナー組織内の入力方向の要求にマップされるため、リソースパートナーは、アカウントパートナーが提供する資格情報を受け入れることができます。 

要求を追加するには、次の手順を実行します。

この手順を完了するには、ローカル コンピューター上の **Administrators** または同等のメンバーシップが最低限必要です。  適切なアカウントおよびグループメンバーシップの使用方法の詳細については、「[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)」を参照してください。

## <a name="to-add-a-claim-description"></a>要求の説明を追加するには

1. サーバー マネージャーで、 **[ツール]** をクリックし、次に **[AD FS の管理]** を選択します。 

2. [**サービス**] を展開し、右側の [**要求の説明の追加**] をクリックします。
   ![要求の説明の追加](media/Add-a-Claim-Description/claimdesc1.png)

3. [要求の説明の追加] ダイアログボックスの [**表示名**] に、この要求のグループまたはロールを識別する一意の名前を入力します。

4. **短い名前**を追加します。

5. [**要求識別子**] に、使用する要求のグループまたはロールに関連付けられている URI を入力します。

6. [**説明**] に、この要求の目的に最も適したテキストを入力します。

7. 組織のニーズに応じて、次のいずれかのチェックボックスをオンにして、この要求をフェデレーションメタデータに発行します。


~~~
- To publish this claim to make partners aware that this server can accept this claim, click **Publish this claim in federation metadata as a claim type that this Federation Service can accept**.
- To publish this claim to make partners aware that this server can issue this claim, click **Publish this claim in federation metadata as a claim type that this Federation Service can send**.
~~~

8. **[OK]** をクリックします。

![要求の説明の追加](media/Add-a-Claim-Description/claimdesc2.png)


## <a name="see-also"></a>参照  
[AD FS の運用](../ad-fs-operations.md) 
