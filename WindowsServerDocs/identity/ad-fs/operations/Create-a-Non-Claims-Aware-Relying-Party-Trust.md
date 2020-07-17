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
ms.openlocfilehash: c6886145e910b76edbe99549266d651cdd7c3edf
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816925"
---
# <a name="create-a-non-claims-aware-relying-party-trust"></a>要求対応ではない証明書利用者信頼を作成する


の AD FS 管理スナップ\-では、非\-要求\-対応証明書利用者信頼は、フェデレーションサービスと、Web アプリケーションプロキシ経由でアクセスされる要求\-認識されない単一の web\-ベースのアプリケーションとの間の信頼を表すために作成されるオブジェクトです。  
  
非\-要求\-対応証明書利用者信頼は、証明書利用者信頼が Web アプリケーションプロキシ経由でアクセスされるときの認証と承認のための識別子、名前、および規則で構成される証明書利用者の信頼です。 要求に依存しないこれらの web\-ベースのアプリケーション (つまり、統合 Windows 認証\-ベースのアプリケーション) は、アクセスが Web アプリケーションプロキシ経由で企業ネットワークの外部にある場合に、要求に基づいてアクセスを強制する承認規則を持つことができます。  
  
の AD FS 管理スナップ\-を使用して、新しい非\-要求\-対応証明書利用者信頼を追加するには、次の手順を実行します。  
  
この手順を完了するには、ローカル コンピューター上の **Administrators** または同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
## <a name="to-create-a-non-claims-aware-relying-party-trust-manually"></a>要求対応ではない証明書利用者信頼を手動で作成するには 
1. サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** を選択します。  
  
2.  **[操作]** の **[証明書利用者信頼の追加]** をクリックします。  
証明書利用者](media/Create-a-Relying-Party-Trust/addtrust1.PNG) の ![   

3.  **[ようこそ]** ページで、 **[要求に対応しない]** を選択し、 **[開始]** をクリックします。  
証明書利用者](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon1.PNG) の ![ 
  
4.  **[表示名の指定]** ページで、 **[表示名]** に名前を入力し、 **[メモ]** にこの証明書利用者信頼の説明を入力して、 **[次へ]** をクリックします。  
証明書利用者](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon2.PNG) の ![

5. **[識別子の構成]** ページで、この証明書利用者の識別子を 1 つ以上指定し、 **[追加]** をクリックして一覧に追加したら、 **[次へ]** をクリックします。  
証明書利用者](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon3.PNG) の ![

6.  **[Access Control ポリシーの選択]** でポリシーを選択し、 **[次へ]** をクリックします。  Access Control ポリシーの詳細については、「 [AD FS でのポリシーの Access Control](Access-Control-Policies-in-AD-FS.md)」を参照してください。 
証明書利用者](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon4.PNG) の ![

7. **[信頼の追加の準備完了]** ページで、設定を確認し、 **[次へ]** をクリックして、証明書利用者信頼情報を保存します。  
   証明書利用者](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon5.PNG) の ![ 

8. **[完了]** ページで、 **[閉じる]** をクリックします。 これにより、自動的に **[要求規則の編集]** ダイアログ ボックスが表示されます。  
証明書利用者](media/Create-a-Non-Claims-Aware-Relying-Party-Trust/addnon6.PNG) の ![  
  
## <a name="see-also"></a>参照  
[AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md) 
