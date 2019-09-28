---
ms.assetid: 638c89bd-87e6-484b-9d2e-8ae2a74227e5
title: サービス通信証明書を設定する
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: d0464853c73f88ed76545921ffc8a4bf8551c800
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408327"
---
# <a name="set-a-service-communications-certificate"></a>サービス通信証明書を設定する


Active Directory フェデレーションサービス (AD FS) \(AD FS @ no__t のフェデレーションサーバーでは、サービス通信証明書を使用して、Web クライアントまたはフェデレーションサーバーとの Secure Sockets Layer \(SSL @ no__t 通信の Web サービストラフィックをセキュリティで保護します。proxy.

> [!NOTE]  
> サービス通信証明書が SSL 証明書と同じではありません。 AD FS SSL 証明書を変更するには、Powershell を使用する必要があります。 この[記事](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/manage-ssl-certificates-ad-fs-wap)のガイダンスに従ってください。


でサービス通信証明書を変更するには、次の手順に従い、の AD FS 管理スナップイン @ no__t-0in 使用します。  

> [!NOTE]  
> AD FS Management snap @ no__t-0in は、サービス通信証明書としてフェデレーションサーバーのサーバー認証証明書を参照します。  

この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントおよびグループメンバーシップの使用に関する詳細については、「[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.microsoft.com\/fwlink\/?」を参照してください。LinkId\=83477\)。   

### <a name="to-set-a-service-communications-certificate"></a>サービス通信証明書を設定するには  

1.  **スタート**画面で「**AD FS Management**」と入力し、enter キーを押します。  

2.  コンソールツリーで、 **[サービス]** をダブルクリックし、 **[証明書]** をクリックします。  

3.  **[操作]** ウィンドウで、 **[サービス通信証明書の設定]** リンクをクリックします。  

4.  **[サービス通信証明]** 書の選択 ダイアログボックスで、サービス通信証明書として設定する証明書ファイルに移動し、証明書ファイルを選択して、 **[開く]** をクリックします。  

## <a name="additional-references"></a>その他の参照情報  
[チェックリスト:フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)  

[フェデレーション サーバーの証明書の要件](https://technet.microsoft.com/library/dd807040.aspx)  
