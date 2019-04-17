---
ms.assetid: cea6011d-3753-4b95-aaa5-38d4e97d6e42
title: Prepare Client Computers in the Account Partner
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 0c5bdcb0a80b15a1905109229ddd20ee642a8dd7
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="prepare-client-computers-in-the-account-partner"></a>Prepare Client Computers in the Account Partner

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

アカウント パートナー組織内の管理者は Active Directory フェデレーション サービス \(AD FS\) フェデレーション アプリケーションにアクセスするためのクライアント コンピューターを準備するための最も簡単な方法では、グループ ポリシーを使用します。 グループ ポリシーは、特定の証明書とフェデレーション フェデレーション アプリケーションにアクセスするために使用するすべてのクライアント コンピューターに必要な設定をプッシュするための便利な方法を提供します。  
  
クライアント コンピューターでは、証明書のプロンプトや信頼済みサイトに関連するプロンプトなしフェデレーション アプリケーションにシームレスにアクセスできる、できるように、組織で AD FS を広く展開する前にまず各クライアント コンピューターを準備することをお勧めします。 グループ ポリシーを自動的に使用を検討してください。  
  
-   アカウント フェデレーション サーバーを信頼する場合は、各クライアント コンピューターで Internet Explorer を構成します。  
  
    詳細については、次を参照してください。[、アカウント フェデレーション サーバーを信頼するクライアント コンピューターの構成](../../ad-fs/deployment/Configure-Client-Computers-to-Trust-the-Account-Federation-Server.md)します。  
  
-   適切なアカウント フェデレーション サーバー、リソース フェデレーション サーバー、および Web サーバーの Secure Sockets Layer \(SSL\) 証明書をインストール \ (またはそれと同等の証明書を信頼された使いますチェーン化された) 各クライアント コンピューターでします。  
  
    詳細については、次を参照してください。[グループ ポリシーを使用して、クライアント コンピューターに証明書を配布](../../ad-fs/deployment/Distribute-Certificates-to-Client-Computers-by-Using-Group-Policy.md)します。  
  

## <a name="see-also"></a>参照してください。
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)
