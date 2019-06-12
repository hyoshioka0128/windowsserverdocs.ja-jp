---
ms.assetid: 7b7ae389-5032-44f7-9c0a-94398c3e4d88
title: 要求対応ではない証明書利用者信頼を作成する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e94b07d7fa654732526d0b43daadc9ad0ad4f3a8
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444931"
---
# <a name="create-a-non-claims-aware-relying-party-trust"></a>要求対応の証明書利用者のパーティの信頼を作成します。


AD FS 管理スナップインで\-以外で\-クレーム\-証明書利用者の信頼は、フェデレーション サービスと 1 つの web の間の信頼を表すために作成されたオブジェクトに注意してください\-ベースでないアプリケーションクレーム\-対応 Web アプリケーション プロキシ経由でアクセスされるとします。  
  
非\-クレーム\-証明書利用者の信頼は、証明書利用者信頼で構成される識別子、名前、および認証と承認規則、証明書利用者の信頼は、Web アプリケーション プロキシを介してアクセスするときに注意してください。 これらの web\-ベースのアプリケーションの信頼性情報、つまり、これら統合 Windows 認証を使用しない\-ベースのアプリケーションは、アクセスがときに、クレームに基づくアクセスを適用する承認規則を持つことができますWeb アプリケーション プロキシ経由で企業ネットワークの外部です。  
  
新しいを追加する非\-クレーム\-対応証明書利用者信頼、AD FS 管理スナップインを使用して\-で、次の手順を実行します。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
## <a name="to-create-a-non-claims-aware-relying-party-trust-manually"></a>手動で要求に非対応証明書利用者の信頼を作成するには 
1. サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  
  
2.  [**アクション**、] をクリックして**証明書利用者信頼の追加**します。  
![証明書利用者](media/Create-a-Relying-Party-Trust/addtrust1.PNG)   

3.  **ようこそ**ページで、選択**以外の要求に対応** をクリック**開始**します。  
![証明書利用者](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon1.PNG) 
  
4.  **表示名の指定**に名前を入力] ページで、**表示名**[**ノート**この証明書利用者のパーティの信頼の説明を入力し、クリックして **[次へ]** .  
![証明書利用者](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon2.PNG)

5. **[識別子の構成]** ページで、この証明書利用者の識別子を 1 つ以上指定し、 **[追加]** をクリックして一覧に追加したら、 **[次へ]** をクリックします。  
![証明書利用者](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon3.PNG)

6.  **へのアクセス制御ポリシーの選択**ポリシーを選択し、をクリックして**次**します。  アクセス制御ポリシーの詳細については、次を参照してください。 [AD FS でのアクセス制御ポリシー](Access-Control-Policies-in-AD-FS.md)します。 
![証明書利用者](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon4.PNG)

7. **[信頼の追加の準備完了]** ページで、設定を確認し、 **[次へ]** をクリックして、証明書利用者信頼情報を保存します。  
   ![証明書利用者](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon5.PNG) 

8. **[完了]** ページで、 **[閉じる]** をクリックします。 これにより、自動的に **[要求規則の編集]** ダイアログ ボックスが表示されます。  
![証明書利用者](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon6.PNG)  
  
## <a name="see-also"></a>関連項目  
[AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md) 
