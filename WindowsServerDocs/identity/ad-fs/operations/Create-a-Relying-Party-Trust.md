---
ms.assetid: 5b9fc9c1-5d12-4ad4-8ddc-3b8a6d45b217
title: 証明書利用者の信頼を作成する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: a0d32edd7ebc23fa724439710c6511642d9c49a3
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79323054"
---
# <a name="create-a-relying-party-trust"></a>証明書利用者の信頼を作成する


次のドキュメントでは、証明書利用者信頼を手動で作成し、フェデレーションメタデータを使用する方法について説明します。
  
## <a name="to-create-a-claims-aware-relying-party-trust-manually"></a>要求に対応する証明書利用者信頼を手動で作成するには 

の AD FS 管理スナップ\-を使用して新しい証明書利用者信頼を追加し、設定を手動で構成するには、フェデレーションサーバーで次の手順を実行します。  

この手順を完了するには、ローカル コンピューター上の **Administrators** または同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。
  
1. サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** を選択します。  
  
2.  **[操作]** の **[証明書利用者信頼の追加]** をクリックします。  
証明書利用者](media/Create-a-Relying-Party-Trust/addtrust1.PNG) の ![   

3.  **[ようこそ]** ページで、 **[要求に対応]** を選択し、 **[開始]** をクリックします。  
証明書利用者](media/Create-a-Relying-Party-Trust/addtrust2.PNG) の ![ 
  
4.  **[データ ソースの選択]** ページで、 **[証明書利用者についてのデータを手動で入力する]** をクリックし、 **[次へ]** をクリックします。  
証明書利用者](media/Create-a-Relying-Party-Trust/addtrust3.PNG) の ![ 
  
5.  **[表示名の指定]** ページで、 **[表示名]** に名前を入力し、 **[メモ]** にこの証明書利用者信頼の説明を入力して、 **[次へ]** をクリックします。  
証明書利用者](media/Create-a-Relying-Party-Trust/addtrust4.PNG) の ![ 

6. オプションのトークン暗号化証明書がある場合は、 **[証明書の構成]** ページで **[参照]** をクリックして証明書ファイルを指定し、 **[次へ]** をクリックします。  
証明書利用者](media/Create-a-Relying-Party-Trust/addtrust5.PNG) の ![ 

7.  **[URL の構成]** ページで、次のいずれかまたは両方を実行し、 **[次へ]** をクリックして、手順 8. に進みます。  
  
    -   [ **WS\-フェデレーションパッシブプロトコルのサポートを有効にする**] チェックボックスをオンにします。 [**証明書利用者 WS\-フェデレーションパッシブプロトコル url**] に、この証明書利用者信頼の url を入力し、 **[次へ]** をクリックします。  
  
    -   **[SAML 2.0 WebSSO プロトコルのサポートを有効にする]** チェック ボックスをオンにします。 **[証明書利用者 SAML 2.0 SSO サービス url]** に、この証明書利用者信頼の SECURITY ASSERTION MARKUP LANGUAGE \(SAML\) サービスエンドポイント url を入力し、 **[次へ]** をクリックします。  
証明書利用者](media/Create-a-Relying-Party-Trust/addtrust6.PNG) の ![   

8. **[識別子の構成]** ページで、この証明書利用者の識別子を 1 つ以上指定し、 **[追加]** をクリックして一覧に追加したら、 **[次へ]** をクリックします。  
証明書利用者](media/Create-a-Relying-Party-Trust/addtrust8.PNG) の ![
  
9.  **[Access Control ポリシーの選択]** でポリシーを選択し、 **[次へ]** をクリックします。  Access Control ポリシーの詳細については、「 [AD FS でのポリシーの Access Control](Access-Control-Policies-in-AD-FS.md)」を参照してください。 
証明書利用者](media/Create-a-Relying-Party-Trust/addtrust9.PNG) の ![

10. **[信頼の追加の準備完了]** ページで、設定を確認し、 **[次へ]** をクリックして、証明書利用者信頼情報を保存します。  
   証明書利用者](media/Create-a-Relying-Party-Trust/addtrust10.PNG) の ![ 
11. **[完了]** ページで、 **[閉じる]** をクリックします。 これにより、自動的に **[要求規則の編集]** ダイアログ ボックスが表示されます。  
証明書利用者](media/Create-a-Relying-Party-Trust/addtrust11.PNG) の ![ 

## <a name="to-create-a-claims-aware-relying-party-trust-using-federation-metadata"></a>フェデレーションメタデータを使用して要求に対応する証明書利用者信頼を作成するには

AD FS 管理スナップインを使用して新しい証明書利用者信頼を追加するには、パートナーがローカルネットワークまたはインターネットに発行したフェデレーションメタデータからパートナーに関する構成データを自動的にインポートして、次の手順を実行します。アカウントパートナー組織のフェデレーションサーバー。

>[!NOTE]
>https://myserverなど、修飾されていないホスト名を持つ証明書を使用することは、一般的には長いことですが、これらの証明書にはセキュリティ値がなく、攻撃者はフェデレーションメタデータを公開するフェデレーションサービスを偽装できます。 そのため、フェデレーションメタデータに対してクエリを実行する場合は、 https://myserver.contoso.comのような完全修飾ドメイン名のみを使用する必要があります。

この手順を完了するには、ローカル コンピューター上の **Administrators** または同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。


1. サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** を選択します。  
  
2. **[操作]** の **[証明書利用者信頼の追加]** をクリックします。  
   証明書利用者](media/Create-a-Relying-Party-Trust/addtrust1.PNG) の ![   

3. **[ようこそ]** ページで、 **[要求に対応]** を選択し、 **[開始]** をクリックします。  
   証明書利用者](media/Create-a-Relying-Party-Trust/addtrust2.PNG) の ![ 
  
4. **[データソースの選択]** ページで、[<strong>オンラインまたはローカルネットワークで公開されている証明書利用者に関するデータをインポートする] * をクリックします。* * [フェデレーションメタデータアドレス (ホスト名または URL)] に</strong>、パートナーのフェデレーションメタデータ URL またはホスト名を入力し、 **[次へ]** をクリックします。  
   証明書利用者](media/Create-a-Relying-Party-Trust/addtrust12.PNG) の ![ 

5. 表示名の指定 ページで、**表示名** に名前を入力し、メモ にこの証明書利用者信頼の説明を入力して、**次へ** をクリックします。

6. 発行承認規則の選択 ページで、**この証明書利用者へのすべてのユーザーのアクセスを許可する** または **この証明書利用者へのすべてのユーザーのアクセスを拒否**する を選択し、**次へ** をクリックします。

7. 信頼の追加の準備完了 ページで設定を確認し、**次へ** をクリックして証明書利用者の信頼情報を保存します。

8. 完了 ページで **閉じる** をクリックします。 これにより、自動的に [要求規則の編集] ダイアログ ボックスが表示されます。 この証明書利用者信頼の要求規則を追加する手順の詳細については、「その他の参照情報」を参照してください。




## <a name="see-also"></a>参照  
[AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md) 
