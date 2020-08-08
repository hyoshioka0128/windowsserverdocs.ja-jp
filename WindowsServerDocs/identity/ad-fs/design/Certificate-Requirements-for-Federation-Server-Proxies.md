---
ms.assetid: dc24adb7-385d-4a92-ab81-78ba73df0118
title: フェデレーション サーバー プロキシの証明書の要件
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 51eb0e72f52fafdb2f1b8bbb3f9a2850602c3f75
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954338"
---
# <a name="certificate-requirements-for-federation-server-proxies"></a>フェデレーション サーバー プロキシの証明書の要件

Active Directory フェデレーションサービス (AD FS) AD FS でフェデレーションサーバープロキシの役割を実行しているサーバー \( \) は Secure Sockets Layer \( SSL サーバー認証証明書を使用する必要が \) あります。 フェデレーション サーバー プロキシは、SSL サーバー認証証明書を使用して、Web クライアントとの Web サーバーのトラフィック通信をセキュリティ保護します。

通常、フェデレーションサーバープロキシは、エンタープライズ公開キー基盤 PKI に含まれていないインターネット上のコンピューターに公開され \( \) ます。 そのため、 \( \- VeriSign などの公共のサードパーティ \) の証明機関 CA によって発行されたサーバー認証証明書を使用し \( \) ます。

フェデレーションサーバープロキシファームがある場合は、すべてのフェデレーションサーバープロキシコンピューターで同じサーバー認証証明書を使用する必要があります。 詳細については、「 [When to Create a Federation Server Proxy Farm](When-to-Create-a-Federation-Server-Proxy-Farm.md)」を参照してください。

サーバー認証証明書のサブジェクト名が、AD FS 管理スナップインで指定されているフェデレーションサービス名の値と一致していることを確認することが重要です \- 。 この値を検索するには、スナップインを開き、 \- \- [**サービス**] を右クリックし、[**フェデレーションサービスのプロパティの編集**] をクリックして、**フェデレーションサービス名**] テキストボックスで値を探します。

SSL 証明書の使用に関する一般的な情報については、「IIS 7.0 での Secure Sockets Layer の構成 \( [http: \/ \/ go.microsoft.com \/ fwlink \/ ?」を参照してください。\=](https://go.microsoft.com/fwlink/?LinkID=108544) \) IIS 7.0 での LinkID 108544 とサーバー証明書の構成 \( [http: \/ \/ go.microsoft.com \/ fwlink \/ ?LinkID \= 108545](https://go.microsoft.com/fwlink/?LinkID=108545) \) 。

> [!NOTE]
> AD FS フェデレーションサーバープロキシでは、クライアント認証証明書は必要ありません。

使用する証明書に証明書失効リストの crl がある場合 \( \) 、構成された証明書を持つサーバーは、crl を配布するサーバーに接続できる必要があります。 CRL の種類によって、使用するポートが決まります。

## <a name="see-also"></a>参照
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
