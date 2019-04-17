---
ms.assetid: dc24adb7-385d-4a92-ab81-78ba73df0118
title: "フェデレーション サーバー プロキシの証明書の要件"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e7fb8e71afed1c0eb6b55857835d95f2dd0ec9d5
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="certificate-requirements-for-federation-server-proxies"></a>フェデレーション サーバー プロキシの証明書の要件

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Active Directory フェデレーション サービス \(AD FS\) でフェデレーション サーバー プロキシの役割で実行しているサーバーは、Secure Sockets Layer \(SSL\) サーバー認証証明書を使用する必要があります。 フェデレーション サーバー プロキシは、Web クライアントと Web サーバーのトラフィック通信をセキュリティで保護するのに SSL サーバー認証証明書を使用します。  
  
通常、フェデレーション サーバー プロキシは、エンタープライズ公開キー インフラストラクチャに含まれていないインターネット上のコンピューターに公開 \(PKI\) します。 そのため、パブリック \(third\-party\) 証明機関によって発行されたサーバー認証証明書を使用して \(CA\)、VeriSign などです。  
  
フェデレーション サーバー プロキシ ファームがある場合は、すべてのフェデレーション サーバー プロキシ コンピューターは、同じサーバー認証証明書を使用する必要があります。 詳細については、次を参照してください。[フェデレーション サーバー プロキシ ファームを作成するときに](When-to-Create-a-Federation-Server-Proxy-Farm.md)します。  
  
ことが重要で、サーバー認証証明書のサブジェクト名の AD FS 管理スナップインで指定されているフェデレーション サービス名の値と一致していることを確認します。 この値を見つけるを開き、スナップイン、右クリック**サービス**、] をクリックして**フェデレーション サービスのプロパティの編集**、し、値を検索**フェデレーション サービス名**テキスト ボックスです。  
  
詳細については、SSL 証明書を使用して、IIS 7.0 で Secure Sockets Layer の構成を参照してください \ ([http:///\/go.microsoft.com\/fwlink\/ですか?。LinkID\ = 108544](https://go.microsoft.com/fwlink/?LinkID=108544)\) と IIS 7.0 でサーバー証明書の構成 \ ([http:///\/go.microsoft.com\/fwlink\/ ですか?LinkID\ = 108545](https://go.microsoft.com/fwlink/?LinkID=108545)\)。  
  
> [!NOTE]  
> クライアント認証証明書は、AD FS フェデレーション サーバー プロキシの必要はありません。  
  
使用する任意の証明書の証明書失効リスト \(CRLs\) 場合は、構成された証明書で、サーバーは、Crl を配布するサーバーに接続できる必要があります。 CRL の種類は、どのようなポートが使用を決定します。  
  
## <a name="see-also"></a>参照してください。
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)
