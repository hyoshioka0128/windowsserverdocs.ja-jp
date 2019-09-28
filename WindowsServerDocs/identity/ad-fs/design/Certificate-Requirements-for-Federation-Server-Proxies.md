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

@No__t-0AD FS @ no__t Active Directory フェデレーションサービス (AD FS) のフェデレーションサーバープロキシの役割で実行されているサーバーでは、Secure Sockets Layer \(SSL @ no__t サーバー認証証明書を使用する必要があります。 フェデレーション サーバー プロキシは、SSL サーバー認証証明書を使用して、Web クライアントとの Web サーバーのトラフィック通信をセキュリティ保護します。  
  
フェデレーションサーバープロキシは、通常、インターネット上のコンピューターに公開されます。このコンピューターは、エンタープライズ公開キー基盤 \(PKI @ no__t-1 に含まれていません。 このため、パブリック \(third @ no__t-1party @ no__t-2 証明 @no__t 機関 (たとえば、VeriSign) によって発行されたサーバー認証証明書を使用します。  
  
フェデレーションサーバープロキシファームがある場合は、すべてのフェデレーションサーバープロキシコンピューターで同じサーバー認証証明書を使用する必要があります。 詳細については、次を参照してください。[フェデレーション サーバー プロキシ ファームを作成するときに](When-to-Create-a-Federation-Server-Proxy-Farm.md)します。  
  
サーバー認証証明書のサブジェクト名が、の AD FS 管理スナップインで指定されているフェデレーションサービス名の値と一致していることを確認することが重要です。 この値を検索するには、でスナップ @ no__t を開き、@ no__t をクリックして **サービス** を右クリックし、**フェデレーションサービスのプロパティの編集** をクリックして、**フェデレーションサービス名** ボックスに値を入力します。  
  
SSL 証明書の使用に関する一般的な情報については、「IIS 7.0 での Secure Sockets Layer の構成」を参照してください \([http: \/\/go.microsoft.com @ no__t-4fwlink @ no__t-6108544](https://go.microsoft.com/fwlink/?LinkID=108544)\) と iis 7.0 でのサーバー証明書の構成 \([http: 01go.microsoft.com @](https://go.microsoft.com/fwlink/?LinkID=108545)no__t-12fwlink @ no__t  
  
> [!NOTE]  
> AD FS フェデレーションサーバープロキシでは、クライアント認証証明書は必要ありません。  
  
使用する証明書に証明書失効リスト \(CRLs @ no__t-1 が含まれている場合、証明書が構成されているサーバーは、Crl を配布するサーバーに接続できる必要があります。 CRL の種類によって、使用するポートが決まります。  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
