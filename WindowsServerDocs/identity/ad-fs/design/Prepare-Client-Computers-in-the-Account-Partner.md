---
ms.assetid: cea6011d-3753-4b95-aaa5-38d4e97d6e42
title: アカウント パートナー内のクライアント コンピューターを準備する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 5725f4a7761d08a25ee8c67c0568977e3646397e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407941"
---
# <a name="prepare-client-computers-in-the-account-partner"></a>アカウント パートナー内のクライアント コンピューターを準備する

アカウントパートナー組織の管理者が Active Directory フェデレーションサービス (AD FS) @no__t にアクセスできるようにクライアントコンピューターを準備する最も簡単な方法はグループポリシーを使用することです。 グループ ポリシーは、フェデレーションに必要な特定の証明書と設定を、フェデレーション アプリケーションへのアクセスに使用されるすべてのクライアント コンピューターにプッシュするための便利な方法を提供します。  
  
クライアントコンピューターが証明書のプロンプトや信頼されたサイト関連のプロンプトを表示せずに、フェデレーションアプリケーションにシームレスにアクセスできるように、最初に各クライアントコンピューターを準備してから、組織内に AD FS 展開することをお勧めします。 グループ ポリシーを使用して、次の操作を自動化することを検討してください。  
  
-   各クライアントコンピューターで、アカウントフェデレーションサーバーを信頼するように Internet Explorer を構成します。  
  
    詳細については、「 [アカウント フェデレーション サーバーを信頼するクライアント コンピューターを構成します](../../ad-fs/deployment/Configure-Client-Computers-to-Trust-the-Account-Federation-Server.md)」を参照してください。  
  
-   適切なアカウントフェデレーションサーバー、リソースフェデレーションサーバー、および Web サーバー Secure Sockets Layer \(SSL @ no__t 証明書 \(、または各クライアントコンピューターの信頼されたルート @ no__t-3 にチェーンする同等の証明書をインストールします。  
  
    詳細については、「グループポリシーを使用した[クライアントコンピューターへの証明書の配布](../../ad-fs/deployment/Distribute-Certificates-to-Client-Computers-by-Using-Group-Policy.md)」を参照してください。  
  

## <a name="see-also"></a>関連項目
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
