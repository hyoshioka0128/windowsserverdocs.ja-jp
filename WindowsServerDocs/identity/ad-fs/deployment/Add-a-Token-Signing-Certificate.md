---
ms.assetid: bbb84ea6-7e31-4442-85ab-a9447e7c19e8
title: トークン署名証明書を追加する
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: c8b2246842dd70c06442faed995f6b883dbaf70a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71360086"
---
# <a name="add-a-token-signing-certificate"></a>トークン署名証明書を追加する


Active Directory フェデレーションサービス (AD FS) \(AD FS @ no__t のフェデレーションサーバーは、トークン @ no__t-2signing 証明書を必要とします。これにより、攻撃者が、フェデレーションへの不正アクセスを試みたときにセキュリティトークンを変更または偽造するのを防ぐことができます。参考. すべての\-トークン署名証明書には、秘密キー\)によるデジタル署名\(に使用される暗号化秘密キーと公開キーが含まれています。セキュリティトークンです。 その後、これらのキーがパートナーフェデレーションサーバーによって受信された後、暗号化されたセキュリティトークンの公開キー @ no__t によって、そのキーの @no__t 信頼性が検証されます。  
  
> [!CAUTION]  
> トークン @ no__t-0signing に使用される証明書は、フェデレーションサービスの安定性を確保するために重要です。 この目的で構成された証明書の損失または計画外の削除によってサービスが中断される可能性があるため、この目的で構成された証明書をバックアップする必要があります。  
  
トークン @ no__t-0signing 証明書は、フェデレーションサービス内の信頼されたルートにチェーンされている必要があります。 次の手順を使用して、エクスポートしたファイルから、トークン @ no__t-0signing 証明書を AD FS Management スナップ @ no__t に追加できます。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントおよびグループメンバーシップの使用に関する詳細については、「[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.microsoft.com\/fwlink\/?」を参照してください。LinkId\=83477\)。   
  
### <a name="to-add-a-token-signing-certificate"></a>トークン @ no__t-0signing 証明書を追加するには  
  
1.  **スタート**画面で「**AD FS Management**」と入力し、enter キーを押します。  
  
2.  コンソールツリーで、 **[サービス]** をダブルクリックし、 **[証明書]** をクリックします。  
  
3.  **[操作]** ウィンドウで、 **[トークンの追加 @ No__t-2Signing 証明書]** リンクをクリックします。  
  
4.  **[証明書ファイルの参照]** ダイアログボックスで、追加する証明書ファイルに移動し、証明書ファイルを選択して **[開く]** をクリックします。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト:フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)  
  
[フェデレーション サーバーの証明書の要件](https://technet.microsoft.com/library/dd807040.aspx)  
  

