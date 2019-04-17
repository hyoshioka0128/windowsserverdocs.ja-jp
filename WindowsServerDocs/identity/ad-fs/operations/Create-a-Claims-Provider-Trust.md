---
ms.assetid: a4f7842c-cfca-4d78-916e-023d12a9cdf0
title: "要求プロバイダー信頼を作成します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b4dc20713fdd137b019a072037e35e9219e02fa9
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-claims-provider-trust"></a>要求プロバイダー信頼を作成します。

>適用対象: Windows Server 2016、Windows Server 2012 R2

AD FS 管理スナップインを使用して新しい要求プロバイダー信頼を追加して、手動で設定を構成、リソース パートナー組織のリソース パートナーのフェデレーション サーバーで次の手順を実行します。  
  
メンバーシップ**管理者**、相当するもので、ローカル コンピューターでは、この手順を実行する最小要件またはします。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
## <a name="to-create-a-claims-provider-trust-manually"></a>要求プロバイダー信頼を手動で作成するには  
  
1.  サーバー マネージャーで、クリックして**ツール**、し、[ **AD FS 管理**します。  
  
2.  [**アクション**、] をクリックして**要求プロバイダー信頼の追加**します。  
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim1.PNG)   
  
3.  **ようこそ**] ページで [**開始**します。 
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim2.PNG)    
  
4.  **データ ソースの選択**] ページで [**要求プロバイダー信頼のデータの手動で入力**、] をクリックし、 **[次へ]**します。  
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim3.PNG)     

5.  **表示名の指定**] ページで、入力、**表示名**[**ノート**この要求プロバイダー信頼の説明を入力し、[クリックして**[次へ]**します。  
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim4.PNG)     

6.  **URL の構成**] ページで、指定、 **Ws-federation パッシブ URL**該当する場合] をクリック**次**します。
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim5.PNG)     

8. **識別子の構成**ページで、**要求プロバイダー信頼の識別子**適切な識別子を入力し、[クリックして**次**します。  
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim6.PNG)    

9. **証明書の構成**ページで、[**追加**証明書ファイルを検索し、証明書の一覧に追加] をクリックし、**次**します。  
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim7.PNG)    

10. **信頼の追加の準備完了**] ページで [ **[次へ]** 、要求プロバイダー信頼の情報を保存します。  
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim8.PNG)    

11. **完了**] ページで [**閉じる**します。 このアクションは自動的に表示されます、**要求規則の編集**] ダイアログ ボックス。 追加する方法の詳細についてこの要求プロバイダー信頼に要求規則は、次の他の参照を参照してください。  
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim9.PNG)

## <a name="to-create-a-claims-provider-trust-using-federation-metadata"></a>フェデレーション メタデータを使用して要求プロバイダー信頼を作成するには
パートナーがローカル ネットワークまたはインターネットに公開したフェデレーション メタデータからパートナーに関する構成データを自動的にインポートして、AD FS 管理スナップインを使用して新しい要求プロバイダー信頼を追加するには、リソース パートナー組織内のフェデレーション サーバーで次の手順を実行します。

>[!NOTE]
>Https://myserver などの非修飾ホスト名を持つ証明書を使用する一般的なプラクティス長いされた、これらの証明書はセキュリティの値が設定されていないと、フェデレーション メタデータを公開するフェデレーション サービスの偽装が攻撃者が有効にすることができます。 したがって、フェデレーション メタデータを照会する場合のみに https://myserver.contoso.com などの完全修飾ドメイン名を使用する必要があります。

1.  サーバー マネージャーで、クリックして**ツール**、し、[ **AD FS 管理**します。  
  
2.  [**アクション**、] をクリックして**証明書利用者信頼の追加**します。  
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim1.PNG)   
  
3.  **ようこそ**] ページで [**開始**します。 
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim2.PNG)    
  
4.  **データ ソースの選択**] ページで [**オンラインまたはローカル ネットワークで公開されている要求プロバイダーについてインポート データ**します。 フェデレーション メタデータのアドレス (ホスト名または URL) を入力、**フェデレーション メタデータ URL**またはホスト、パートナーの名前を指定し、をクリックして**次**します。
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim10.PNG)    

5.  表示名の指定 [種類] ページで、**表示名**ノート下にある必要この要求プロバイダー信頼の説明を入力し、[クリックして**次**します。

6.  準備完了信頼の追加] ページで、をクリックして**次**、要求プロバイダー信頼の情報を保存します。

7.  [完了] ページで、をクリックして**閉じる**します。 これは、要求規則の編集] ダイアログ ボックスを自動的に表示されます。 追加する方法の詳細についてはこの要求プロバイダー信頼に要求規則、後述の「その他参照を参照してください。



    
## <a name="additional-references"></a>その他の参照  
[チェックリスト: リソース パートナー組織の構成](../../ad-fs/deployment/Checklist--Configuring-the-Resource-Partner-Organization.md)  
  
[チェックリスト: Creating Claim Rules for 要求プロバイダー信頼します。](../../ad-fs/deployment/Checklist--Creating-Claim-Rules-for-a-Claims-Provider-Trust.md)  
  
## <a name="see-also"></a>参照してください。  
[AD FS の操作](../../ad-fs/AD-FS-2016-Operations.md) 
  
