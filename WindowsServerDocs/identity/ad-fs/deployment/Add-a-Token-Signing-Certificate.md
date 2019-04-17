---
ms.assetid: bbb84ea6-7e31-4442-85ab-a9447e7c19e8
title: "トークン署名証明書を追加します。"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 8a94e0724d6fd2a04e2fbfc22b3054b49d87f440
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="add-a-token-signing-certificate"></a>トークン署名証明書を追加します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Active Directory フェデレーション サービス \(AD FS\) 内のフェデレーション サーバーでは、攻撃者が改ざんまたはフェデレーション リソースに不正にアクセスしようとすると、セキュリティ トークンを偽造するを防ぐために token\ 署名証明書が必要です。 すべての token\ 署名証明書には秘密キーの暗号化とデジタル署名に使用される公開キーが含まれています \ (プライベート key \) を使用してセキュリティ トークン。 その後、これらのキーがパートナーのフェデレーション サーバーによって受信されると、検証信頼性 \ (public key \) を使用して、暗号化されたセキュリティ トークンのします。  
  
> [!CAUTION]  
> Token\ 署名に使用される証明書は、フェデレーション サービスの安定性にとって重要です。 損失またはこの目的で構成されているすべての証明書の計画外の削除は、サービスを妨害したり、ために、この目的で構成されているすべての証明書をバックアップする必要があります。  
  
Token\ 署名証明書は、フェデレーション サービスにおいて信頼されたルートにチェーンする必要があります。 エクスポートしたファイルから AD FS 管理スナップインに token\ 署名証明書を追加するのに、次の手順を使用することができます。  
  
メンバーシップ**管理者**、相当するもので、ローカル コンピューターでは、この手順を完了するために必要な最低限またはします。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)\ (http:///\/go.microsoft.com\/fwlink\/ですか?LinkId\ = 83477\)。   
  
### <a name="to-add-a-token-signing-certificate"></a>Token\ 署名証明書の追加  
  
1.  **開始**画面で「**AD FS 管理**、し、Enter キーを押します。  
  
2.  コンソール ツリーで、ダブルクリック**サービス**、] をクリックし、**証明書**します。  
  
3.  **アクション**] ウィンドウで、をクリックして、**追加 Token\ 署名証明書**リンクします。  
  
4.  **証明書ファイルの参照**] ダイアログ ボックスで、追加、証明書ファイルを選択し、クリックする証明書ファイルを移動**開く**します。  
  
## <a name="additional-references"></a>その他の参照  
[チェックリスト: フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)  
  
[フェデレーション サーバーの証明書の要件](https://technet.microsoft.com/library/dd807040.aspx)  
  

