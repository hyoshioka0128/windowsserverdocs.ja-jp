---
ms.assetid: 5b9fc9c1-5d12-4ad4-8ddc-3b8a6d45b217
title: 証明書利用者の信頼を作成する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 14e1cc732ed60b7f05a9a4a9aac9037c48b702f2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879923"
---
# <a name="create-a-relying-party-trust"></a>証明書利用者の信頼を作成する

>適用先:Windows Server 2016、Windows Server 2012 R2

次のドキュメントは、証明書利用者信頼を手動で作成すると、フェデレーション メタデータを使用して情報を提供します。
  
## <a name="to-create-a-claims-aware-relying-party-trust-manually"></a>対応の証明書利用者のパーティを手動で信頼を要求を作成するには 

AD FS 管理スナップインを使用して新しい証明書利用者信頼を追加する\-でを手動で設定を構成、フェデレーション サーバーで次の手順を実行します。  

この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。
  
1. サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  
  
2.  [**アクション**、] をクリックして**証明書利用者信頼の追加**します。  
![証明書利用者](media/Create-a-Relying-Party-Trust/addtrust1.PNG)   

3.  **ようこそ**ページで、選択**要求に対応** をクリック**開始**します。  
![証明書利用者](media/Create-a-Relying-Party-Trust/addtrust2.PNG) 
  
4.  **[データ ソースの選択]** ページで、**[証明書利用者についてのデータを手動で入力する]** をクリックし、**[次へ]** をクリックします。  
![証明書利用者](media/Create-a-Relying-Party-Trust/addtrust3.PNG) 
  
5.  **表示名の指定**に名前を入力] ページで、**表示名**[**ノート**この証明書利用者のパーティの信頼の説明を入力し、クリックして **[次へ]**.  
![証明書利用者](media/Create-a-Relying-Party-Trust/addtrust4.PNG) 

6. **証明書の構成**ページで、をクリックして、省略可能なトークン暗号化証明書がある場合**参照**証明書ファイルを検索してクリックする**次**。  
![証明書利用者](media/Create-a-Relying-Party-Trust/addtrust5.PNG) 

7.  **URL の構成** ページで、次のいずれかの操作を行います、 をクリックして**次**、手順 8. に進みます。  
  
    -   選択、 **、WS のサポートを有効にする\-フェデレーション パッシブ プロトコル**チェック ボックスをオンします。 **証明書利用者のパーティの WS\-フェデレーション パッシブ プロトコル URL**この証明書利用者のパーティの信頼の URL を入力し、クリックして**次**します。  
  
    -   **[SAML 2.0 WebSSO プロトコルのサポートを有効にする]** チェック ボックスをオンにします。 **証明書利用者 SAML 2.0 SSO サービス URL**、Security Assertion Markup Language の入力\(SAML\)サービスこの証明書利用者信頼に対して、エンドポイントの URL をクリックして**次**.  
![証明書利用者](media/Create-a-Relying-Party-Trust/addtrust6.PNG)   

8. **[識別子の構成]** ページで、この証明書利用者の識別子を 1 つ以上指定し、**[追加]** をクリックして一覧に追加したら、**[次へ]** をクリックします。  
![証明書利用者](media/Create-a-Relying-Party-Trust/addtrust8.PNG)
  
9.  **へのアクセス制御ポリシーの選択**ポリシーを選択し、をクリックして**次**します。  アクセス制御ポリシーの詳細については、次を参照してください。 [AD FS でのアクセス制御ポリシー](Access-Control-Policies-in-AD-FS.md)します。 
![証明書利用者](media/Create-a-Relying-Party-Trust/addtrust9.PNG)

10. **[信頼の追加の準備完了]** ページで、設定を確認し、**[次へ]** をクリックして、証明書利用者信頼情報を保存します。  
   ![証明書利用者](media/Create-a-Relying-Party-Trust/addtrust10.PNG) 
11. **[完了]** ページで、**[閉じる]** をクリックします。 これにより、自動的に **[要求規則の編集]** ダイアログ ボックスが表示されます。  
![証明書利用者](media/Create-a-Relying-Party-Trust/addtrust11.PNG) 

## <a name="to-create-a-claims-aware-relying-party-trust-using-federation-metadata"></a>対応の利用者がフェデレーション メタデータを使用してを信頼、要求を作成するには

新しい証明書利用者信頼を追加するには、パートナーは、ローカル ネットワークまたはインターネットに公開したフェデレーション メタデータからパートナーに関する構成データを自動的にインポートすることによって、AD FS 管理スナップインを使用して、次の手順で実行します。アカウント パートナー組織のフェデレーション サーバー。

>[!NOTE]
>などの非修飾ホスト名で証明書を使用する一般的な方法が長年、 https://myserver、これらの証明書セキュリティの値がない場合や、攻撃者にフェデレーション メタデータを発行するフェデレーション サービスの権限を借用を有効にすることができます。 そのため、フェデレーション メタデータを照会するときにする必要がありますのみを使用して、完全修飾ドメイン名など https://myserver.contoso.comします。

この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。


1. サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  
  
2.  [**アクション**、] をクリックして**証明書利用者信頼の追加**します。  
![証明書利用者](media/Create-a-Relying-Party-Trust/addtrust1.PNG)   

3.  **ようこそ**ページで、選択**要求に対応** をクリック**開始**します。  
![証明書利用者](media/Create-a-Relying-Party-Trust/addtrust2.PNG) 
  
4.  **データ ソースの選択** ページで、をクリックして **オンラインまたはローカル ネットワーク上に発行された証明書利用者に関するデータをインポート*します。 **[フェデレーション メタデータのアドレス (ホスト名または URL)]** に、パートナーのフェデレーション メタデータ URL またはホスト名を入力して、**[次へ]** をクリックします。  
![証明書利用者](media/Create-a-Relying-Party-Trust/addtrust12.PNG) 

5.  [表示名の指定] ページに名前を入力**表示名**、ノートの下でこの証明書利用者のパーティの信頼の説明を入力し、順にクリックします**次**します。

6.  発行承認規則の選択 ページで、いずれかを選択**すべてのユーザーにこの証明書利用者にアクセスする許可**または**すべてのユーザーにこの証明書利用者へのアクセスを拒否**、 をクリックし、 **次へ**.

7.  信頼の追加 ページの準備完了、設定を確認し、順にクリックします**次**証明書利用者を保存する情報を信頼します。

8.  [完了] ページで、次のようにクリックします。**閉じる**します。 このアクションでは、要求規則の編集 ダイアログ ボックスが自動的に表示されます。 この証明書利用者信頼の要求規則を追加する手順の詳細については、「その他の参照情報」を参照してください。




## <a name="see-also"></a>関連項目  
[AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md) 
