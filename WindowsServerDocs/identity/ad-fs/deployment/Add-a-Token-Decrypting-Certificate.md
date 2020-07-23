---
ms.assetid: 27e1e299-0beb-4e86-8143-1ba031dc3502
title: トークン暗号化解除証明書を追加する
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: e703b9966fdd443c2799120464dcb92b2458428b
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966784"
---
# <a name="add-a-token-decrypting-certificate"></a>トークン暗号化解除証明書を追加する

フェデレーションサーバーでは、 \- 新しい証明書がプライマリ暗号化解除証明書として設定された後に、証明書利用者のフェデレーションサーバーが古い証明書で発行されたトークンの暗号化を解除する必要がある場合に、トークン暗号化解除証明書を使用します。 Active Directory フェデレーションサービス (AD FS) \( AD FS \) は、 \( 既定の \) \( \) 暗号化解除証明書としてインターネットインフォメーションサービス IIS の Secure Sockets Layer SSL 証明書を使用します。  
  
> [!CAUTION]  
> トークンの暗号化解除に使用される証明書 \- は、フェデレーションサービスの安定性を確保するために重要です。 この目的で構成された証明書の損失または計画外の削除によってサービスが中断される可能性があるため、この目的で構成された証明書をバックアップする必要があります。  
  
次の手順を使用して、 \- エクスポートしたファイルから AD FS 管理スナップインにトークン暗号化解除証明書を追加でき \- ます。  
  
この手順を完了するには、ローカル コンピューター上の **Administrators** または同等のメンバーシップが最低限必要です。  適切なアカウントおよびグループメンバーシップの使用に関する詳細については、「[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477) \( http: \/ \/ go.microsoft.com fwlink?」を参照して \/ \/ ください。LinkId \= 83477 \) 。   
  
### <a name="to-add-a-token-decrypting-certificate"></a>トークン \- 暗号化解除証明書を追加するには  
  
1.  **スタート**画面で「**AD FS Management**」と入力し、enter キーを押します。  
  
2.  コンソールツリーで、[サービス] をダブルクリックし、[ \- **証明書**] をクリックします。 **Service**  
  
3.  [**操作**] ウィンドウで、[**トークン \- 暗号化解除証明書の追加**] リンクをクリックします。  
  
4.  [**証明書ファイルの参照**] ダイアログボックスで、追加する証明書ファイルに移動し、証明書ファイルを選択して [**開く**] をクリックします。  
  
## <a name="additional-references"></a>その他のリファレンス  
[チェックリスト:フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)  
  
[フェデレーション サーバーの証明書の要件](../design/certificate-requirements-for-federation-servers.md)  
  
