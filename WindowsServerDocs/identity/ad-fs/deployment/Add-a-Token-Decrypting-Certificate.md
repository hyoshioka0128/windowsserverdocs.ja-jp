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
ms.openlocfilehash: 5714a41950b9c2f818ddc154a9af7a55fdb362d8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80814966"
---
# <a name="add-a-token-decrypting-certificate"></a>トークン暗号化解除証明書を追加する

証明書利用者のフェデレーションサーバーが、新しい証明書をプライマリ暗号化解除証明書として設定した後で、古い証明書を使用して発行されたトークンの暗号化を解除する必要がある場合、フェデレーションサーバーはトークン\-暗号化解除証明書を使用します。 Active Directory フェデレーションサービス (AD FS) \(AD FS\) は、既定の暗号化解除証明書として Secure Sockets Layer \(IIS\) にインターネットインフォメーションサービス \(SSL\) 証明書を使用します。  
  
> [!CAUTION]  
> トークン\-復号化に使用される証明書は、フェデレーションサービスの安定性にとって非常に重要です。 この目的で構成された証明書の損失または計画外の削除によってサービスが中断される可能性があるため、この目的で構成された証明書をバックアップする必要があります。  
  
次の手順を使用して、エクスポートしたファイルからの AD FS 管理スナップ\-に証明書の暗号化解除\-トークンを追加できます。  
  
この手順を完了するには、ローカル コンピューター上の **Administrators** または同等のメンバーシップが最低限必要です。  適切なアカウントとグループメンバーシップの使用に関する詳細については、\(http:\/\/go.microsoft.com\/fwlink\/? [」を参照](https://go.microsoft.com/fwlink/?LinkId=83477)してください。LinkId\=83477\)。   
  
### <a name="to-add-a-token-decrypting-certificate"></a>証明書の暗号化を解除\-トークンを追加するには  
  
1.  **スタート**画面で「**AD FS Management**」と入力し、enter キーを押します。  
  
2.  コンソールツリーで、 **[サービス]** をダブル\-クリックし、 **[証明書]** をクリックします。  
  
3.  **[操作]** ウィンドウで、[**トークンの追加\-証明書の暗号化解除**] リンクをクリックします。  
  
4.  **[証明書ファイルの参照]** ダイアログボックスで、追加する証明書ファイルに移動し、証明書ファイルを選択して **[開く]** をクリックします。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト: フェデレーションサーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)  
  
[フェデレーション サーバーの証明書の要件](https://technet.microsoft.com/library/dd807040.aspx)  
  

