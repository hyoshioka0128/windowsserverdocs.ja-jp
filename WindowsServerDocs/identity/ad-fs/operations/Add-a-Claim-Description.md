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
ms.openlocfilehash: 1023ca7da02d2a1f6af42f68892dc4c5c8f1a2bf
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444369"
---
# <a name="add-a-claim-description"></a>要求記述を追加する


アカウント パートナー組織では、管理者は、ユーザーのグループまたはロールのメンバーシップを表すためのユーザーの従業員識別番号などのユーザーに関するいくつかのデータを表すクレームを作成します。

リソース パートナーの組織では、管理者は、グループとリソースのユーザーとして認識できるユーザーを表す対応する要求を作成します。 リソース パートナーで、リソース パートナー組織内の入力方向の要求には、アカウント パートナー組織マップ要求送信ため、アカウント パートナーが提供する資格情報を受け入れることができます。 

次の手順を使用して、クレームを追加することができます。

この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。

## <a name="to-add-a-claim-description"></a>クレームの説明を追加するには

1. サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。 

2. 展開**サービス**で右クリック**要求記述の追加**します。
   ![クレームの説明を追加します。](media/Add-a-Claim-Description/claimdesc1.png)

3. 追加要求記述 ダイアログ ボックスの**表示名**、グループまたはこの要求のロールを識別する一意の名前を入力します。

4. 追加、**名の短い**します。

5. **要求識別子**に関連付けられたグループまたはロールを使用するクレームの URI を入力します。

6. **説明**、この要求の目的に最も近いテキストを入力します。

7. 、組織のニーズに応じてこの要求をフェデレーション メタデータに公開する、必要に応じて、次のチェック ボックスのいずれかを選択します。


~~~
- To publish this claim to make partners aware that this server can accept this claim, click **Publish this claim in federation metadata as a claim type that this Federation Service can accept**.
- To publish this claim to make partners aware that this server can issue this claim, click **Publish this claim in federation metadata as a claim type that this Federation Service can send**.
~~~

8. **[OK]** をクリックします。

![クレームの説明を追加します。](media/Add-a-Claim-Description/claimdesc2.png)


## <a name="see-also"></a>関連項目  
[AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md) 
