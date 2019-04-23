---
title: トランスポート層セキュリティ プロトコル
description: Windows Server のセキュリティ
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-tls-ssl
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: de510bb0-a9f6-4bbe-8f8a-8dd7473bbae8
author: justinha
ms.author: justinha
manager: brianlic-msft
ms.date: 05/16/2018
ms.openlocfilehash: 77e3ee9d89bff7ab6e95ea47ffa141e6e1004ba4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853023"
---
# <a name="transport-layer-security-protocol"></a>トランスポート層セキュリティ プロトコル

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10

IT プロフェッショナルは、このトピックでは、トランスポート層セキュリティ (TLS) プロトコルの動作し、TLS 1.0、TLS 1.1、および TLS 1.2 には、IETF Rfc へのリンクを示しますについて説明します。

TLS (および SSL) プロトコルは、アプリケーション プロトコル レイヤーと、セキュリティで保護し、トランスポート層にアプリケーション データを送信、TCP/IP 層の間にあります。 アプリケーション層とトランスポート層の間、プロトコルの動作のため、TLS と SSL は複数のアプリケーション レイヤー プロトコルをサポートできます。

TLS と SSL は、通常の TCP 接続指向のトランスポートで使用されていると仮定します。 プロトコルは、次のセキュリティ リスクを検出するために、クライアントとサーバー アプリケーションを使用できます。

-   メッセージの改ざん

-   メッセージのインターセプト

-   メッセージ偽造

TLS と SSL プロトコルは、2 つのレイヤーに分割できます。 アプリケーション プロトコルと 3 つのハンドシェイク プロトコルの最初のレイヤーで構成されます。 ハンドシェイク プロトコル、変更、cipher spec プロトコル、およびアラートのプロトコル。 2 番目のレイヤーは、レコード プロトコルです。 次の図は、さまざまなレイヤーとその要素を示しています。

**TLS と SSL プロトコル レイヤー**


Schannel SSP では、変更しなくても TLS と SSL プロトコルを実装します。 SSL プロトコルが、独自には、Internet Engineering Task Force は、TLS の公開仕様が生成されます。 Windows のバージョンでどの TLS または SSL のバージョンがサポートされているは、次を参照してください。 [in TLS/SSL (Schannel SSP) プロトコル](https://msdn.microsoft.com/en-us/library/windows/desktop/mt808159(v=vs.85).aspx)します。 次の表では、TLS のバージョンごとの仕様を示します。 各仕様には、に関する情報が含まれています。

-   TLS レコード プロトコル

-   TLS ハンドシェイク プロトコル:\- Cipher spec プロトコル変更\-プロトコルのアラート

-   暗号化の計算

-   必須の暗号スイート

-   アプリケーション データ プロトコル

[RFC 5246 - トランスポート層セキュリティ (TLS) プロトコル バージョン 1.2](http://tools.ietf.org/html/rfc5246)

[RFC 4346 - トランスポート層セキュリティ (TLS) プロトコル バージョン 1.1](http://tools.ietf.org/html/rfc4346)

[RFC 2246 - TLS プロトコル バージョン 1.0](http://tools.ietf.org/html/rfc2246)

## <a name="BKMK_SessionResumption"></a>TLS セッションの再開
Windows Server 2012 R2 で導入された、Schannel SSP は TLS セッションの再開のサーバー側の部分を実装します。 RFC 5077 のクライアント側の実装は、Windows 8 で追加されました。

TLS をサーバーに接続するデバイスは、頻繁に再接続する必要があります。 TLS セッションの再開には、再開には、省略の TLS ハンドシェイクが含まれているため、TLS 接続を確立するコストが削減されます。 により、互いの TLS セッションの再開の TLS サーバーのグループの複数の再開試行が実行を容易になります。 この変更は、Windows Phone および Windows RT デバイスを含め、RFC 5077 をサポートする任意の TLS クライアントの次の削減を提供します。

-   サーバー上のリソース使用量の削減

-   使用帯域幅の削減によるクライアント接続の効率の向上

-   接続の再開のための TLS ハンドシェイクに費やされた時間の短縮

ステートレスな TLS セッションの再開については、IETF のドキュメントを参照してください。 [RFC 5077 します。](http://www.ietf.org/rfc/rfc5077)

## <a name="BKMK_AppProtocolNego"></a>アプリケーション プロトコルのネゴシエーション
 Windows Server 2012 R2 および Windows 8.1 には、クライアント側の TLS アプリケーション プロトコルのネゴシエーションを許可するためのサポートが導入されました。 アプリケーションは、HTTP 2.0 標準開発の一部としてプロトコルを利用し、ユーザーは SPDY プロトコルを実行中のアプリを使用して、Google、Twitter などのオンライン サービスにアクセスできます。

アプリケーション プロトコルのネゴシエーションの動作については、次を参照してください。[トランスポート層セキュリティ (TLS) アプリケーション レイヤー プロトコルのネゴシエーション拡張](http://tools.ietf.org/search/draft-ietf-tls-applayerprotoneg-05)します。

## <a name="BKMK_SNI"></a>TLS が Server Name Indication 拡張機能をサポートします。
Server Name Indication (SNI) は SSL プロトコルと TLS プロトコルを拡張する機能で、1 台のサーバーでいくつもの仮想イメージを実行している場合にサーバーを適切に認識できるようにします。 仮想ホスティング シナリオでは、複数のドメイン (それぞれに異なる可能性がある証明書) が 1 つのサーバーでホストされます。 この場合、サーバーでは、クライアントに送信する証明書の事前に知る方法がありません。 SNI は、プロトコルでは、前のターゲット ドメインを通知するために、クライアント、サーバーを適切な証明書を正しく選択できます。

この追加機能によって、次のことが可能になります。

-   1 つのインターネット プロトコルとポートの組み合わせでの複数の SSL web サイトをホストすることができます。

-   1 台の Web サーバーに複数の SSL Web サイトをホストする場合に、メモリ使用量を削減できます

-   多くのユーザーが同時に web サイトに SSL 接続を許可します。



