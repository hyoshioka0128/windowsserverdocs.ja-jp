---
ms.assetid: cea6011d-3753-4b95-aaa5-38d4e97d6e42
title: アカウント パートナー内のクライアント コンピューターを準備する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e3a746ec003cf312ffe0b9804f84a55c98aa8089
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190989"
---
# <a name="prepare-client-computers-in-the-account-partner"></a>アカウント パートナー内のクライアント コンピューターを準備する

管理者アカウントでの最も簡単な方法を Active Directory フェデレーション サービスにアクセスするためのクライアント コンピューターを準備する組織のパートナー \(AD FS\)フェデレーション アプリケーションは、グループ ポリシーを使用します。 グループ ポリシーは、フェデレーションに必要な特定の証明書と設定を、フェデレーション アプリケーションへのアクセスに使用されるすべてのクライアント コンピューターにプッシュするための便利な方法を提供します。  
  
クライアント コンピューターでは、証明書のプロンプトや信頼済みサイトに関連するプロンプトなしのフェデレーション アプリケーションをシームレスにアクセスできる、ように、お客様の組織で AD FS を広く展開する前にまず各クライアント コンピューターを準備することをお勧めします。 グループ ポリシーを使用して、次の操作を自動化することを検討してください。  
  
-   アカウント フェデレーション サーバーを信頼するには、各クライアント コンピューターで Internet Explorer を構成します。  
  
    詳細については、「 [Configure Client Computers to Trust the Account Federation Server](../../ad-fs/deployment/Configure-Client-Computers-to-Trust-the-Account-Federation-Server.md)」を参照してください。  
  
-   適切なアカウント フェデレーション サーバー、リソース フェデレーション サーバー、および Web サーバーをインストール Secure Sockets Layer \(SSL\)証明書\(と同等の信頼されたルートにチェーン化された証明書または\)各クライアント コンピューター。  
  
    詳細については、次を参照してください。[グループ ポリシーを使用してクライアント コンピューターに証明書を配布](../../ad-fs/deployment/Distribute-Certificates-to-Client-Computers-by-Using-Group-Policy.md)します。  
  

## <a name="see-also"></a>関連項目
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
