---
ms.assetid: a4f7842c-cfca-4d78-916e-023d12a9cdf0
title: 要求プロバイダー信頼を作成する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fbc8bb63435211a92cb7fc6aa05b1413aef939c6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854233"
---
# <a name="create-a-claims-provider-trust"></a>要求プロバイダー信頼を作成する

>適用先:Windows Server 2016、Windows Server 2012 R2

AD FS 管理スナップインを使用して要求プロバイダー信頼の追加、新しい\-でを手動で設定を構成、リソース パートナー組織でリソース パートナーのフェデレーション サーバーで次の手順を実行します。  
  
メンバーシップ**管理者**、またはこの手順を実行する最小要件は、ローカル コンピューターのそれと同等です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
## <a name="to-create-a-claims-provider-trust-manually"></a>要求プロバイダー信頼を手動で作成するには  
  
1.  サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  
  
2.  [**アクション**、] をクリックして**要求プロバイダー信頼の追加**します。  
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim1.PNG)   
  
3.  **[ようこそ]** ページで、 **[開始]** をクリックします。 
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim2.PNG)    
  
4.  **[データ ソースの選択]** ページで、**[要求プロバイダー信頼のデータを手動で入力する]** をクリックし、**[次へ]** をクリックします。  
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim3.PNG)     

5.  **[表示名の指定]** ページで、**[表示名]** に表示名を入力し、**[注意事項]** にこの要求プロバイダー信頼の説明を入力して、**[次へ]** をクリックします。  
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim4.PNG)     

6.  **URL の構成**ページで、指定、 **Ws-federation パッシブ URL**該当する場合 をクリック**次**します。
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim5.PNG)     

8. **[識別子の構成]** ページの **[要求プロバイダー信頼の識別子]** に、適切な識別子を入力し、**[次へ]** をクリックします。  
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim6.PNG)    

9. **[証明書の構成]** ページで **[追加]** をクリックして、証明書ファイルを参照し、それを証明書の一覧に追加した後、**[次へ]** をクリックします。  
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim7.PNG)    

10. **[信頼の追加の準備完了]** ページで **[次へ]** をクリックして、要求プロバイダー信頼情報を保存します。  
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim8.PNG)    

11. **[完了]** ページで、**[閉じる]** をクリックします。 これにより、自動的に **[要求規則の編集]** ダイアログ ボックスが表示されます。 追加する方法の詳細についての要求規則がこの要求プロバイダー信頼の次の他の参照を参照してください。  
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim9.PNG)

## <a name="to-create-a-claims-provider-trust-using-federation-metadata"></a>フェデレーション メタデータを使用して要求プロバイダー信頼を作成するには
新しいを追加する要求プロバイダー信頼、AD FS 管理スナップインを使用して、自動的にパートナーがローカル ネットワークまたはインターネットに公開したフェデレーション メタデータからパートナーに関する構成データをインポートすることで、次の手順で実行します。リソース パートナー組織のフェデレーション サーバー。

>[!NOTE]
>などの非修飾ホスト名で証明書を使用する一般的な方法が長年、 https://myserver、これらの証明書セキュリティの値がない場合や、攻撃者にフェデレーション メタデータを発行するフェデレーション サービスの権限を借用を有効にすることができます。 そのため、フェデレーション メタデータを照会するときにする必要がありますのみを使用して、完全修飾ドメイン名など https://myserver.contoso.comします。

1.  サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  
  
2.  [**アクション**、] をクリックして**要求プロバイダー信頼の追加**します。  
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim1.PNG)   
  
3.  **[ようこそ]** ページで、 **[開始]** をクリックします。 
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim2.PNG)    
  
4.  **[データ ソースの選択]** ページで、**[オンラインまたはローカル ネットワークで公開されている要求プロバイダーについてのデータをインポートする]** をクリックします。 フェデレーション メタデータのアドレス (ホスト名または URL) を入力、**フェデレーション メタデータ URL**またはホスト パートナーは、名前を指定し、をクリックし、**次**。
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim10.PNG)    

5.  表示名の指定] ページの種類、**表示名**ノートでこの要求プロバイダー信頼に説明を入力し、[クリックして**次**します。

6.  準備完了信頼の追加 ページで、をクリックして**次**を要求プロバイダー信頼の情報を保存します。

7.  [完了] ページで、次のようにクリックします。**閉じる**します。 これは、要求規則の編集 ダイアログ ボックスを自動的に表示されます。 追加する方法の詳細についての要求規則がこの要求プロバイダー信頼の下の他の参照セクションを参照してください。



    
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト:リソース パートナー組織の構成](../../ad-fs/deployment/Checklist--Configuring-the-Resource-Partner-Organization.md)  
  
[チェックリスト:要求規則の作成要求プロバイダー信頼します。](../../ad-fs/deployment/Checklist--Creating-Claim-Rules-for-a-Claims-Provider-Trust.md)  
  
## <a name="see-also"></a>関連項目  
[AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md) 
  
