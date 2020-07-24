---
ms.assetid: 7b7ae389-5032-44f7-9c0a-94398c3e4d88
title: 要求対応ではない証明書利用者信頼を作成する
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 2bc08d2797812d6001f2a792037bcfb8bab4fc0a
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86965644"
---
# <a name="create-a-non-claims-aware-relying-party-trust"></a>要求対応ではない証明書利用者信頼を作成する


AD FS 管理スナップインで \- は、要求に対応していない \- \- 証明書利用者信頼は、フェデレーションサービスと、 \- 要求に対応しておらず、 \- web アプリケーションプロキシ経由でアクセスされる1つの web ベースアプリケーションとの間の信頼を表すために作成されるオブジェクトです。  
  
要求を認識しない証明書利用者信頼は、証明書利用者信頼 \- \- が Web アプリケーションプロキシ経由でアクセスされるときの認証と承認のための識別子、名前、および規則で構成される証明書利用者の信頼です。 \-要求に依存しないこれらの web ベースのアプリケーション (つまり、統合 Windows 認証ベースの \- アプリケーション) には、アクセスが Web アプリケーションプロキシ経由で企業ネットワークの外部にある場合に、要求に基づいてアクセスを強制する承認規則を設定できます。  
  
AD FS 管理スナップインを使用して、要求に対応していない新しい証明書利用者信頼を追加するには、 \- \- \- 次の手順を実行します。  
  
この手順を完了するには、ローカル コンピューター上の **Administrators** または同等のメンバーシップが最低限必要です。  適切なアカウントおよびグループメンバーシップの使用方法の詳細については、「[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)」を参照してください。   
  
## <a name="to-create-a-non-claims-aware-relying-party-trust-manually"></a>要求対応ではない証明書利用者信頼を手動で作成するには 
1. サーバー マネージャーで、 **[ツール]** をクリックし、次に **[AD FS の管理]** を選択します。  
  
2.  [**操作**] の [**証明書利用者信頼の追加**] をクリックします。  
![証明書利用者](media/Create-a-Relying-Party-Trust/addtrust1.PNG)   

3.  [**ようこそ**] ページで、[**要求に対応しない**] を選択し、[**開始**] をクリックします。  
![証明書利用者](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon1.PNG) 
  
4.  **[表示名の指定]** ページで、**[表示名]** に名前を入力し、**[メモ]** にこの証明書利用者の説明を入力して、**[次へ]** をクリックします。  
![証明書利用者](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon2.PNG)

5. [**識別子の構成**] ページで、この証明書利用者の識別子を 1 つ以上指定し、[**追加**] をクリックして一覧に追加したら、[**次へ**] をクリックします。  
![証明書利用者](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon3.PNG)

6.  **[アクセス制御ポリシーの選択]** で、ポリシーを選択して、**[次へ]** をクリックします。  Access Control ポリシーの詳細については、「 [AD FS でのポリシーの Access Control](Access-Control-Policies-in-AD-FS.md)」を参照してください。 
![証明書利用者](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon4.PNG)

7. [**信頼の追加の準備完了**] ページで、設定を確認し、[**次へ**] をクリックして、証明書利用者信頼情報を保存します。  
   ![証明書利用者](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon5.PNG) 

8. **[完了]** ページで、**[閉じる]** をクリックします。 これにより、自動的に **[要求規則の編集]** ダイアログ ボックスが表示されます。  
![証明書利用者](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon6.PNG)  
  
## <a name="see-also"></a>参照  
[AD FS の運用](../ad-fs-operations.md) 
