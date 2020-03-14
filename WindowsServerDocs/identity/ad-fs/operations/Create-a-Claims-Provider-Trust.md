---
ms.assetid: a4f7842c-cfca-4d78-916e-023d12a9cdf0
title: 要求プロバイダー信頼を作成する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 4539e8abd1af1eca7bacb51971e6d355bb0aab28
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79323084"
---
# <a name="create-a-claims-provider-trust"></a>要求プロバイダー信頼を作成する

の AD FS 管理スナップ\-を使用して新しい要求プロバイダー信頼を追加し、手動で設定を構成するには、リソースパートナー組織のリソースパートナーフェデレーションサーバーで次の手順を実行します。  
  
この手順を実行するには、ローカルコンピューターの**Administrators**、またはそれと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
## <a name="to-create-a-claims-provider-trust-manually"></a>要求プロバイダー信頼を手動で作成するには  
  
1.  サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** を選択します。  
  
2.  **[アクション]** で、 **[要求プロバイダー信頼の追加]** をクリックします。  
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim1.PNG)   
  
3.  **[ようこそ]** ページで、 **[開始]** をクリックします。 
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim2.PNG)    
  
4.  **[データ ソースの選択]** ページで、 **[要求プロバイダー信頼のデータを手動で入力する]** をクリックし、 **[次へ]** をクリックします。  
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim3.PNG)     

5.  **[表示名の指定]** ページで、 **[表示名]** に表示名を入力し、 **[注意事項]** にこの要求プロバイダー信頼の説明を入力して、 **[次へ]** をクリックします。  
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim4.PNG)     

6.  **[URL の構成]** ページで、 **ws-federation パッシブ URL** (該当する場合) を指定し、 **[次へ]** をクリックします。
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim5.PNG)     

8. **[識別子の構成]** ページの **[要求プロバイダー信頼の識別子]** に、適切な識別子を入力し、 **[次へ]** をクリックします。  
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim6.PNG)    

9. **[証明書の構成]** ページで **[追加]** をクリックして、証明書ファイルを参照し、それを証明書の一覧に追加した後、 **[次へ]** をクリックします。  
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim7.PNG)    

10. **[信頼の追加の準備完了]** ページで **[次へ]** をクリックして、要求プロバイダー信頼情報を保存します。  
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim8.PNG)    

11. **[完了]** ページで、 **[閉じる]** をクリックします。 これにより、自動的に **[要求規則の編集]** ダイアログ ボックスが表示されます。 この要求プロバイダー信頼の要求規則を追加する方法の詳細については、次の追加の参照情報を参照してください。  
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim9.PNG)

## <a name="to-create-a-claims-provider-trust-using-federation-metadata"></a>フェデレーションメタデータを使用して要求プロバイダー信頼を作成するには
AD FS 管理スナップインを使用して、パートナーがローカルネットワークまたはインターネットに発行したフェデレーションメタデータからパートナーに関する構成データを自動的にインポートすることによって、新しい要求プロバイダー信頼を追加するには、次の手順を実行します。リソースパートナー組織のフェデレーションサーバー。

>[!NOTE]
>一般に、https:\//dns などの修飾されていないホスト名を持つ証明書を使用することは非常に一般的ですが、これらの証明書にはセキュリティ値がないため、攻撃者はフェデレーションメタデータを公開するフェデレーションサービスを偽装できます。 そのため、フェデレーションメタデータに対してクエリを実行する場合は、`https://myserver.contoso.com`のような完全修飾ドメイン名のみを使用する必要があります。

1.  サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** を選択します。  
  
2.  **[アクション]** で、 **[要求プロバイダー信頼の追加]** をクリックします。  
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim1.PNG)   
  
3.  **[ようこそ]** ページで、 **[開始]** をクリックします。 
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim2.PNG)    
  
4.  **[データ ソースの選択]** ページで、 **[オンラインまたはローカル ネットワークで公開されている要求プロバイダーについてのデータをインポートする]** をクリックします。 [フェデレーションメタデータアドレス (ホスト名または URL)] に、パートナーの**フェデレーションメタデータ URL**またはホスト名を入力し、 **[次へ]** をクリックします。
![要求プロバイダー信頼](media/Create-a-Claims-Provider-Trust/addclaim10.PNG)    

5.  表示名の指定 ページで、**表示名**を入力し、メモ にこの要求プロバイダー信頼の説明を入力して、**次へ** をクリックします。

6.  信頼の追加の準備完了 ページで、**次へ** をクリックして、要求プロバイダーの信頼情報を保存します。

7.  完了 ページで **閉じる** をクリックします。 これにより、[要求規則の編集] ダイアログボックスが自動的に表示されます。 この要求プロバイダー信頼の要求規則の追加を続行する方法の詳細については、以下の「その他の参照情報」を参照してください。



    
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト: リソースパートナー組織の構成](../../ad-fs/deployment/Checklist--Configuring-the-Resource-Partner-Organization.md)  
  
[チェックリスト: 要求プロバイダー信頼の要求規則を作成する](../../ad-fs/deployment/Checklist--Creating-Claim-Rules-for-a-Claims-Provider-Trust.md)  
  
## <a name="see-also"></a>参照  
[AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md) 
  
