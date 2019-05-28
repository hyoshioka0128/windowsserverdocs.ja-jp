---
ms.assetid: dc24adb7-385d-4a92-ab81-78ba73df0118
title: フェデレーション サーバー プロキシの証明書の要件
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: ca0b25480eedfc6471837ab8ae83b0d1d522e61e
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191659"
---
# <a name="certificate-requirements-for-federation-server-proxies"></a>フェデレーション サーバー プロキシの証明書の要件

Active Directory フェデレーション サービスでは、フェデレーション サーバー プロキシ ロールで実行されているサーバー \(AD FS\) Secure Sockets Layer を使用するために必要な\(SSL\)サーバー認証証明書。 フェデレーション サーバー プロキシは、SSL サーバー認証証明書を使用して、Web クライアントとの Web サーバーのトラフィック通信をセキュリティ保護します。  
  
フェデレーション サーバー プロキシは通常、エンタープライズ公開キー インフラストラクチャに含まれないインターネット上のコンピューターに公開\(PKI\)します。 そのため、パブリックによって発行されたサーバー認証証明書を使用して、 \(3 番目\-パーティ\)証明機関\(CA\)、たとえば、VeriSign します。  
  
フェデレーション サーバー プロキシ ファームを使用すると、すべてのフェデレーション サーバー プロキシ コンピューターが同じサーバー認証証明書を使用する必要があります。 詳細については、「 [When to Create a Federation Server Proxy Farm](When-to-Create-a-Federation-Server-Proxy-Farm.md)」を参照してください。  
  
AD FS 管理スナップインで、フェデレーション サービス名の値がサーバー認証証明書の一致にサブジェクト名が指定されていることを確認することが重要\-でします。 この値を検索するには、スナップインを開きます\-、右\-クリックして**サービス**、 をクリックして**フェデレーション サービス プロパティの編集**、しの値を検索**フェデレーションサービス名**テキスト ボックス。  
  
SSL 証明書の使用の詳細については、IIS 7.0 で Secure Sockets Layer の構成を参照してください。 \( [http:\/\/go.microsoft.com\/fwlink\/でしょうか。LinkID\=108544](https://go.microsoft.com/fwlink/?LinkID=108544) \) Configuring Server Certificates in IIS 7.0 と\( [http:\/\/go.microsoft.com\/fwlink\/?LinkID\=108545](https://go.microsoft.com/fwlink/?LinkID=108545)\)します。  
  
> [!NOTE]  
> クライアント認証証明書は、AD FS フェデレーション サーバー プロキシの必要はありません。  
  
証明書のいずれかをする場合の使用は、証明書失効リスト\(Crl\)、構成された証明書を使用して、サーバーは、Crl を配布するサーバーに接続できる必要があります。 CRL の種類によって、使用するポートが決まります。  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
