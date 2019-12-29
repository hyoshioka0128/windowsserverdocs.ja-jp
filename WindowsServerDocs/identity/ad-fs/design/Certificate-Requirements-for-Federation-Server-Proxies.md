---
ms.assetid: dc24adb7-385d-4a92-ab81-78ba73df0118
title: フェデレーション サーバー プロキシの証明書の要件
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: dab77c3e3226e89eb3ac9b74e7db9b6df8f181bf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408146"
---
# <a name="certificate-requirements-for-federation-server-proxies"></a>フェデレーション サーバー プロキシの証明書の要件

Active Directory フェデレーションサービス (AD FS) \(AD FS\) でフェデレーションサーバープロキシの役割を実行しているサーバーは、Secure Sockets Layer \(SSL\) サーバー認証証明書を使用する必要があります。 フェデレーション サーバー プロキシは、SSL サーバー認証証明書を使用して、Web クライアントとの Web サーバーのトラフィック通信をセキュリティ保護します。  
  
フェデレーションサーバープロキシは通常、インターネット上のコンピューターに公開されます。このコンピューターは、PKI\)\(エンタープライズ公開キー基盤に含まれていません。 そのため、公共 \(\-サードパーティ\) 証明機関 \(CA\)(VeriSign など) によって発行されたサーバー認証証明書を使用します。  
  
フェデレーションサーバープロキシファームがある場合は、すべてのフェデレーションサーバープロキシコンピューターで同じサーバー認証証明書を使用する必要があります。 詳細については、「 [When to Create a Federation Server Proxy Farm](When-to-Create-a-Federation-Server-Proxy-Farm.md)」を参照してください。  
  
サーバー認証証明書のサブジェクト名が、の AD FS 管理スナップイン\-で指定されているフェデレーションサービス名の値と一致することを確認することが重要です。 この値を見つけるには、でスナップ\-を開き、 **[サービス]** を右\-クリックし、 **[フェデレーションサービスのプロパティの編集]** をクリックして、 **[フェデレーションサービス名]** ボックスで値を探します。  
  
SSL 証明書の使用に関する一般的な情報については、「IIS 7.0 での Secure Sockets Layer の構成 \([http:\/\/go.microsoft.com\/fwlink\/?」を参照してください。LinkID\=108544](https://go.microsoft.com/fwlink/?LinkID=108544)\) と IIS 7.0 でのサーバー証明書の構成 \([http:\/\/go.microsoft.com\/fwlink\/?LinkID\=108545](https://go.microsoft.com/fwlink/?LinkID=108545)\)。  
  
> [!NOTE]  
> AD FS フェデレーションサーバープロキシでは、クライアント認証証明書は必要ありません。  
  
使用する証明書に Crl\)\(証明書失効リストがある場合、構成された証明書を持つサーバーは、Crl を配布するサーバーに接続できる必要があります。 CRL の種類によって、使用するポートが決まります。  
  
## <a name="see-also"></a>参照
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
