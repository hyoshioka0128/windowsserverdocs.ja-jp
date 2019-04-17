---
ms.assetid: 27e1e299-0beb-4e86-8143-1ba031dc3502
title: "トークン暗号化解除証明書を追加します。"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 0eba51521e7ef88542bccf93d92d2e783d800b5e
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="add-a-token-decrypting-certificate"></a>トークン暗号化解除証明書を追加します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

フェデレーション サーバーは、証明書利用者のパーティ フェデレーション サーバーが、新しい証明書がプライマリ暗号化解除証明書として設定された後、古い証明書によって発行されたトークンの暗号化を解除する必要があるときに、token\ 暗号化解除証明書を使用します。 Active Directory フェデレーション サービス \(AD FS\) は、既定の暗号化解除証明書としてインターネット インフォメーション サービス \(IIS\) Secure Sockets Layer \(SSL\) 証明書を使用します。  
  
> [!CAUTION]  
> Token\ 復号化に使用される証明書は、フェデレーション サービスの安定性にとって重要です。 損失またはこの目的で構成されているすべての証明書の計画外の削除は、サービスを妨害したり、ために、この目的で構成されているすべての証明書をバックアップする必要があります。  
  
エクスポートしたファイルから AD FS 管理スナップインに token\ 暗号化解除証明書を追加するのに、次の手順を使用することができます。  
  
メンバーシップ**管理者**、相当するもので、ローカル コンピューターでは、この手順を完了するために必要な最低限またはします。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)\ (http:///\/go.microsoft.com\/fwlink\/ですか?LinkId\ = 83477\)。   
  
### <a name="to-add-a-token-decrypting-certificate"></a>Token\ 暗号化解除証明書の追加  
  
1.  **開始**画面で「**AD FS 管理**、し、Enter キーを押します。  
  
2.  コンソール ツリーで、ダブルクリック**サービス**、] をクリックし、**証明書**します。  
  
3.  **アクション**] ウィンドウで、をクリックして、**追加 Token\ 暗号化解除証明書**リンクします。  
  
4.  **証明書ファイルの参照**] ダイアログ ボックスで、追加、証明書ファイルを選択し、クリックする証明書ファイルを移動**開く**します。  
  
## <a name="additional-references"></a>その他の参照  
[チェックリスト: フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)  
  
[フェデレーション サーバーの証明書の要件](https://technet.microsoft.com/library/dd807040.aspx)  
  

