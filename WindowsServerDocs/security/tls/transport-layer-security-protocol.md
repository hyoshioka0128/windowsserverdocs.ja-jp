---
title: トランスポート層セキュリティ プロトコル
description: Windows Server のセキュリティ
ms.topic: article
ms.assetid: de510bb0-a9f6-4bbe-8f8a-8dd7473bbae8
author: justinha
ms.author: justinha
manager: brianlic
ms.date: 05/16/2018
ms.openlocfilehash: 5641d79c40edaa17fd6c8fddc8cd80cbd30a0951
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87989488"
---
# <a name="transport-layer-security-protocol"></a>トランスポート層セキュリティ プロトコル

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10

IT 担当者向けのこのトピックでは、トランスポート層セキュリティ (TLS) プロトコルのしくみについて説明し、TLS 1.0、TLS 1.1、および TLS 1.2 の IETF Rfc へのリンクを示します。

TLS (および SSL) プロトコルは、アプリケーションプロトコルレイヤーと TCP/IP レイヤーの間に配置されます。この層では、アプリケーションデータをセキュリティで保護し、トランスポート層に送信できます。 プロトコルはアプリケーション層とトランスポート層の間で機能するため、TLS と SSL は複数のアプリケーション層プロトコルをサポートできます。

TLS および SSL は、接続指向のトランスポート (通常は TCP) が使用されていることを前提としています。 このプロトコルを使用すると、クライアントアプリケーションとサーバーアプリケーションは、次のセキュリティリスクを検出できます。

-   メッセージの改ざん

-   メッセージ傍受

-   メッセージ偽造

TLS および SSL プロトコルは、2つの層に分けることができます。 最初の層は、アプリケーションプロトコルと3つのハンドシェイクプロトコルで構成されます。ハンドシェイクプロトコルは、ハンドシェイクプロトコル、変更暗号仕様プロトコル、およびアラートプロトコルです。 2番目のレイヤーは、レコードプロトコルです。 次の図は、さまざまなレイヤーとその要素を示しています。

**TLS および SSL プロトコルレイヤー**


Schannel SSP は、TLS と SSL プロトコルを変更せずに実装します。 SSL プロトコルは専用ですが、インターネット技術標準化委員会によって、パブリック TLS 仕様が生成されます。 Windows のバージョンでサポートされている TLS または SSL のバージョンの詳細については、「 [tls/ssl (SCHANNEL SSP) のプロトコル](/windows/win32/secauthn/protocols-in-tls-ssl--schannel-ssp-)」を参照してください。 次の表に、各 TLS バージョンの仕様を示します。 各仕様には、次の情報が含まれています。

-   TLS レコードプロトコル

-   TLS ハンドシェイクプロトコル: \- 暗号仕様プロトコル \- アラートプロトコルの変更

-   暗号化の計算

-   必須の暗号スイート

-   アプリケーションデータプロトコル

[RFC 5246-トランスポート層セキュリティ (TLS) プロトコルバージョン1.2](http://tools.ietf.org/html/rfc5246)

[RFC 4346 - トランスポート層セキュリティ (TLS) プロトコル バージョン 1.1](http://tools.ietf.org/html/rfc4346)

[RFC 2246 - TLS プロトコル バージョン 1.0](http://tools.ietf.org/html/rfc2246)

## <a name="tls-session-resumption"></a><a name="BKMK_SessionResumption"></a>TLS セッションの再開
Windows Server 2012 R2 で導入された Schannel SSP は、TLS セッションの再開のサーバー側の部分を実装しました。 RFC 5077 のクライアント側の実装は、Windows 8 で追加されました。

TLS をサーバーに接続するデバイスは、頻繁に再接続する必要があります。 Tls セッションの再開では、短い TLS ハンドシェイクが必要になるため、TLS 接続を確立するためのコストが削減されます。 これにより、TLS サーバーのグループが互いの TLS セッションを再開できるようになるため、より多くの再開を容易に行うことができます。 この変更により、Windows Phone と Windows RT デバイスを含む、RFC 5077 をサポートするすべての TLS クライアントに対して次の節約が実現されます。

-   サーバー上のリソース使用量の削減

-   使用帯域幅の削減によるクライアント接続の効率の向上

-   接続の再開のために TLS ハンドシェイクに費やした時間が短縮されました

ステートレスな TLS セッションの再開の詳細については、IETF のドキュメントの [RFC 5077](http://www.ietf.org/rfc/rfc5077) を参照してください。

## <a name="application-protocol-negotiation"></a><a name="BKMK_AppProtocolNego"></a>アプリケーション プロトコルのネゴシエーション
 Windows Server 2012 R2 および Windows 8.1 では、クライアント側の TLS アプリケーションプロトコルネゴシエーションを可能にするサポートが導入されました。 アプリケーションでは、HTTP 2.0 標準開発の一部としてプロトコルを利用できます。また、ユーザーは、SPDY プロトコルを実行するアプリを使用して、Google や Twitter などのオンラインサービスにアクセスできます。

アプリケーション プロトコルのネゴシエーションのしくみについては、[トランスポート層セキュリティ (TLS) のアプリケーション レイヤー プロトコルのネゴシエーション拡張](http://tools.ietf.org/search/draft-ietf-tls-applayerprotoneg-05)に関するページを参照してください。

## <a name="tls-support-for-server-name-indication-extensions"></a><a name="BKMK_SNI"></a>Server Name Indication 拡張機能の TLS サポート
Server Name Indication (SNI) は SSL プロトコルと TLS プロトコルを拡張する機能で、1 台のサーバーでいくつもの仮想イメージを実行している場合にサーバーを適切に認識できるようにします。 仮想ホスティングのシナリオでは、(それぞれが異なる可能性のある証明書を持つ) 複数のドメインが1つのサーバーでホストされます。 この場合、サーバーは、クライアントに送信する証明書を事前に把握する方法がありません。 SNI を使用すると、クライアントはプロトコルの前にターゲットドメインを通知できます。これにより、サーバーは適切な証明書を正しく選択できます。

この追加機能によって、次のことが可能になります。

-   1つのインターネットプロトコルとポートの組み合わせで複数の SSL web サイトをホストできます。

-   1 台の Web サーバーに複数の SSL Web サイトをホストする場合に、メモリ使用量を削減できます

-   より多くのユーザーが SSL web サイトに同時に接続できるようになります