---
ms.assetid: 27e1e299-0beb-4e86-8143-1ba031dc3502
title: トークン暗号化解除証明書を追加する
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: cf89972120f3f0effa3eb1cf0fee6d29dbc8ed4e
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192484"
---
# <a name="add-a-token-decrypting-certificate"></a>トークン暗号化解除証明書を追加する

フェデレーション サーバーは、トークンを使用して\-復号化証明書と証明書利用者のパーティのフェデレーション サーバーが、新しい証明書をプライマリ暗号化解除証明書として設定した後、古い証明書によって発行されたトークンの暗号化を解除する必要があります。 Active Directory フェデレーション サービス\(AD FS\) Secure Sockets Layer を使用して\(SSL\)インターネット インフォメーション サービスの証明書\(IIS\)として、既定の復号化証明書。  
  
> [!CAUTION]  
> トークンを使用する証明書\-復号化は、フェデレーション サービスの安定性に重要です。 損失またはこの目的用に構成されたすべての証明書の計画外の削除は、サービスを中断できる、ため、この目的用に構成されたすべての証明書をバックアップする必要があります。  
  
次の手順を使用するには、トークンを追加する\-証明書を AD FS 管理スナップインを復号化\-でエクスポートしたファイルから。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.microsoft.com\/fwlink\/でしょうか。LinkId\=83477\)します。   
  
### <a name="to-add-a-token-decrypting-certificate"></a>トークンを追加する\-証明書を復号化  
  
1.  **開始**画面で「**AD FS 管理**、し、ENTER キーを押します。  
  
2.  コンソール ツリーで、二重\-クリックして**サービス**、順にクリックします**証明書**します。  
  
3.  **アクション**ウィンドウで、をクリックして、**トークンを追加\-暗号化解除証明書**リンク。  
  
4.  **証明書ファイルの参照** ダイアログ ボックスで、追加、証明書ファイルを選択し、をクリックしたい証明書ファイルを移動**オープン**します。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト:フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)  
  
[フェデレーション サーバーの証明書の要件](https://technet.microsoft.com/library/dd807040.aspx)  
  

