---
ms.assetid: 7b7ae389-5032-44f7-9c0a-94398c3e4d88
title: 要求対応ではない証明書利用者信頼を作成する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: b0ea877170a07db6abe9ac82e72d1722600ec933
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358112"
---
# <a name="create-a-non-claims-aware-relying-party-trust"></a>要求対応ではない証明書利用者信頼を作成する


AD FS Management snap @ no__t-0in は、非 @ no__t-1claims @ no__t-2aware 証明書利用者の信頼は、フェデレーションサービスと、要求 @ no__t に対応していない単一の web @ no__t ベースのアプリケーションとの間の信頼を表すために作成されるオブジェクトです。は、Web アプリケーションプロキシを介してアクセスされます。  
  
非 @ no__t-0claims @ no__t に対応する証明書利用者の信頼は、証明書利用者信頼が Web アプリケーションプロキシ経由でアクセスされるときの認証と承認のための識別子、名前、および規則で構成される証明書利用者の信頼です。 信頼性情報に依存しないこれらの web @ no__t ベースのアプリケーション (つまり、これらの統合 Windows 認証 @ no__t ベースのアプリケーション) には、アクセスが外部にある場合に、クレームに基づくアクセスを強制する承認規則を設定できます。Web アプリケーションプロキシを介した企業ネットワーク。  
  
新しい非 @ no__t-0claims @ no__t を認識する証明書利用者信頼を追加するには、の AD FS 管理スナップインを使用して、次の手順を実行します。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
## <a name="to-create-a-non-claims-aware-relying-party-trust-manually"></a>要求対応ではない証明書利用者信頼を手動で作成するには 
1. サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** を選択します。  
  
2.  **[操作]** の **[証明書利用者信頼の追加]** をクリックします。  
![relying 書利用者 @ no__t-1   

3.  **[ようこそ]** ページで、 **[要求に対応しない]** を選択し、 **[開始]** をクリックします。  
![relying 書利用者 @ no__t-1 
  
4.  **[表示名の指定]** ページで、 **[表示名]** に名前を入力し、 **[メモ]** にこの証明書利用者信頼の説明を入力して、 **[次へ]** をクリックします。  
![relying 書利用者 @ no__t-1

5. **[識別子の構成]** ページで、この証明書利用者の識別子を 1 つ以上指定し、 **[追加]** をクリックして一覧に追加したら、 **[次へ]** をクリックします。  
![relying 書利用者 @ no__t-1

6.  **[Access Control ポリシーの選択]** でポリシーを選択し、 **[次へ]** をクリックします。  Access Control ポリシーの詳細については、「 [AD FS でのポリシーの Access Control](Access-Control-Policies-in-AD-FS.md)」を参照してください。 
![relying 書利用者 @ no__t-1

7. **[信頼の追加の準備完了]** ページで、設定を確認し、 **[次へ]** をクリックして、証明書利用者信頼情報を保存します。  
   ![relying 書利用者 @ no__t-1 

8. **[完了]** ページで、 **[閉じる]** をクリックします。 これにより、自動的に **[要求規則の編集]** ダイアログ ボックスが表示されます。  
![relying 書利用者 @ no__t-1  
  
## <a name="see-also"></a>関連項目  
[AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md) 
