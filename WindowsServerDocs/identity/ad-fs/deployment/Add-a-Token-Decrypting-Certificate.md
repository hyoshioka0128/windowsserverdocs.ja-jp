---
ms.assetid: 27e1e299-0beb-4e86-8143-1ba031dc3502
title: トークン暗号化解除証明書を追加する
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 388414fff97705901bf52ee844b90508d62f8c83
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408454"
---
# <a name="add-a-token-decrypting-certificate"></a>トークン暗号化解除証明書を追加する

フェデレーションサーバーでは、新しい証明書がプライマリ暗号化解除証明書として設定された後に、証明書利用者のフェデレーションサーバーが古い証明書で発行されたトークンの暗号化を解除する必要がある場合に、トークン @ no__t-0decryption 解除証明書を使用します。 Active Directory フェデレーションサービス (AD FS) \(AD FS @ no__t-1 は、既定の暗号化解除証明書としてインターネットインフォメーションサービス \(IIS @ no__t-5 の Secure Sockets Layer \(SSL @ no__t 証明書を使用します。  
  
> [!CAUTION]  
> トークン @ no__t-0decrypting 化に使用される証明書は、フェデレーションサービスの安定性を確保するために重要です。 この目的で構成された証明書の損失または計画外の削除によってサービスが中断される可能性があるため、この目的で構成された証明書をバックアップする必要があります。  
  
次の手順を使用して、エクスポートしたファイルの AD FS 管理スナップ @ no__t にトークン @ no__t-0decrypting 解除証明書を追加できます。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントおよびグループメンバーシップの使用に関する詳細については、「[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.microsoft.com\/fwlink\/?」を参照してください。LinkId\=83477\)。   
  
### <a name="to-add-a-token-decrypting-certificate"></a>トークン @ no__t-0decrypting 解除証明書を追加するには  
  
1.  **スタート**画面で「**AD FS Management**」と入力し、enter キーを押します。  
  
2.  コンソールツリーで、 **[サービス]** をダブルクリックし、 **[証明書]** をクリックします。  
  
3.  **操作** ウィンドウで、**トークンの追加 @ no__t-2Decrypting 証明書の暗号化解除** リンクをクリックします。  
  
4.  **[証明書ファイルの参照]** ダイアログボックスで、追加する証明書ファイルに移動し、証明書ファイルを選択して **[開く]** をクリックします。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト:フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)  
  
[フェデレーション サーバーの証明書の要件](https://technet.microsoft.com/library/dd807040.aspx)  
  

