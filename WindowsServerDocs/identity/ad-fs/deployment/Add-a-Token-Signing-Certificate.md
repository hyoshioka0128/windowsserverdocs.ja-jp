---
ms.assetid: bbb84ea6-7e31-4442-85ab-a9447e7c19e8
title: トークン署名証明書を追加する
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: ac9f9b95ad6226a8e3b7012e317899f1d48c60c9
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192466"
---
# <a name="add-a-token-signing-certificate"></a>トークン署名証明書を追加する


Active Directory フェデレーション サービス内のフェデレーション サーバー \(AD FS\)トークンを必要と\-を攻撃者が改ざんまたは不正にアクセスするためにセキュリティ トークンを偽造を防ぐために証明書の署名リソースのフェデレーションにします。 すべてのトークン\-秘密キーの暗号化とデジタル署名に使用される公開キー署名証明書が含まれています\(、秘密キーによって\)セキュリティ トークン。 後で、パートナーのフェデレーション サーバーでこれらのキーが受信されると、検証信頼性\(、公開キーによって\)の暗号化されたセキュリティ トークン。  
  
> [!CAUTION]  
> トークンを使用する証明書\-署名は、フェデレーション サービスの安定性に重要です。 損失またはこの目的用に構成されたすべての証明書の計画外の削除は、サービスを中断できる、ため、この目的用に構成されたすべての証明書をバックアップする必要があります。  
  
トークン\-署名証明書、フェデレーション サービスで信頼されたルートにチェーンする必要があります。 次の手順を使用するには、トークンを追加する\-署名証明書を AD FS 管理スナップインを\-でエクスポートしたファイルから。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.microsoft.com\/fwlink\/でしょうか。LinkId\=83477\)します。   
  
### <a name="to-add-a-token-signing-certificate"></a>トークンを追加する\-証明書の署名  
  
1.  **開始**画面で「**AD FS 管理**、し、ENTER キーを押します。  
  
2.  コンソール ツリーで、二重\-クリックして**サービス**、順にクリックします**証明書**します。  
  
3.  **アクション**ウィンドウで、をクリックして、**トークンを追加\-署名証明書**リンク。  
  
4.  **証明書ファイルの参照** ダイアログ ボックスで、追加、証明書ファイルを選択し、をクリックしたい証明書ファイルを移動**オープン**します。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト:フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)  
  
[フェデレーション サーバーの証明書の要件](https://technet.microsoft.com/library/dd807040.aspx)  
  

