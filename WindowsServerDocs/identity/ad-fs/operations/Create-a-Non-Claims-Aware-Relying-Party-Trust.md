---
ms.assetid: 7b7ae389-5032-44f7-9c0a-94398c3e4d88
title: "要求に非対応証明書利用者信頼を作成します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f46675ff4c471af743fd8782c1e3036e7c546256
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-non-claims-aware-relying-party-trust"></a>要求対応ではない証明書利用者のパーティ信頼を作成します。

>適用対象: Windows Server 2016、Windows Server 2012 R2

AD FS 管理スナップイン、以外に claims\ 対応では証明書利用者の信頼で、フェデレーション サービスと 1 つ web ベースのアプリケーションと claims\ 対応がない、Web アプリケーション プロキシを介してアクセスされる間の信頼を表すために作成されるオブジェクトです。  
  
証明書以外に claims\ 対応では証明書利用者信頼は、証明書利用者信頼 Web アプリケーション プロキシ経由、証明書利用者信頼にアクセスするときの id、名前、および認証と承認規則で構成されます。 信頼性情報に依存しないこれらの web ベース アプリケーション言い換えると、これらの統合 Windows Authentication\ ベースのアプリケーションでは、ことができます、アクセスが Web アプリケーション プロキシ経由で企業ネットワークの外部に信頼性情報に基づくアクセスを適用する承認規則。  
  
AD FS 管理スナップインを使用して、新しい以外に claims\ 対応では証明書利用者信頼を追加するには、次の手順を実行します。  
  
メンバーシップ**管理者**、相当するもので、ローカル コンピューターでは、この手順を完了するために必要な最低限またはします。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
##<a name="to-create-a-non-claims-aware-relying-party-trust-manually"></a>A 要求に非対応 Relying Party Trust を手動で作成するには 
1. サーバー マネージャーで、クリックして**ツール**、し、[ **AD FS 管理**します。  
  
2.  [**アクション**、] をクリックして**証明書利用者信頼の追加**します。  
![証明書利用者](media/Create-a-Relying-Party-Trust/addtrust1.PNG)   

3.  **ようこそ**ページで、選択**要求に非対応**] をクリック**開始**します。  
![証明書利用者](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon1.PNG) 
  
4.  **表示名の指定**に名前を入力] ページで、**表示名**[**ノート**この証明書利用者信頼の説明を入力し、をクリックして**[次へ]**します。  
![証明書利用者](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon2.PNG)

5. **識別子の構成**] ページでこの証明書利用者の 1 つまたは複数の識別子を指定して、[**追加**クリックして、一覧に追加する**[次へ]**します。  
![証明書利用者](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon3.PNG)

6.  **アクセス制御ポリシーの選択**ポリシーを選択し、をクリックして**次**します。  アクセス制御ポリシーの詳細については、次を参照してください。 [AD FS のアクセス制御ポリシー](Access-Control-Policies-in-AD-FS.md)します。 
![証明書利用者](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon4.PNG)

7. **信頼の追加の準備完了**] ページで、設定を確認してをクリックして**[次へ]** 、証明書利用者を保存する情報を信頼します。  
   ![証明書利用者](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon5.PNG) 

8. **完了**] ページで [**閉じる**します。 このアクションは自動的に表示されます、**要求規則の編集**] ダイアログ ボックス。  
![証明書利用者](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon6.PNG)  
  
## <a name="see-also"></a>参照してください。  
[AD FS の操作](../../ad-fs/AD-FS-2016-Operations.md) 
