---
title: "トランスポート層セキュリティ プロトコル"
description: "Windows Server のセキュリティ"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-tls-ssl
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: de510bb0-a9f6-4bbe-8f8a-8dd7473bbae8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 94c81a79e5f3fd8fc22eafde3de8bd3d0bdd73f0
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# トランスポート層セキュリティ プロトコル

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

IT プロフェッショナル向けのこのトピックでは、どのトランスポート層セキュリティ (TLS) プロトコルが動作するリンクを提供、IETF Rfc に TLS 1.0、TLS 1.1、および TLS 1.2 について説明します。

TLS (と SSL) プロトコルは、アプリケーション プロトコル レイヤーと、セキュリティで保護し、トランスポート層にアプリケーション データを送信、TCP/IP 層の間に配置されます。 プロトコルでは、動作ため、アプリケーション層とトランスポート層の間、TLS と SSL は複数のアプリケーション レイヤー プロトコルをサポートできます。

TLS と SSL は、通常の TCP 接続指向のトランスポートが使用されていると仮定します。 プロトコルには、次のセキュリティ リスクを検出するために、クライアントとサーバーのアプリケーションことができます。

-   メッセージの改ざん

-   メッセージのインターセプト

-   メッセージ偽造など

TLS と SSL プロトコルは、2 つのレイヤーに分けることができます。 アプリケーション プロトコルと 3 つのハンドシェイク プロトコルの最初のレイヤーで構成されます。ハンドシェイク プロトコル、変更、暗号仕様プロトコル、およびアラート プロトコルです。 2 番目の層は、レコード プロトコルです。 次の図は、さまざまなレイヤーとその要素を示しています。

**TLS と SSL プロトコル層**


Schannel SSP では、変更せず、TLS と SSL プロトコルを実装します。 SSL プロトコルが、独自には、インターネット技術標準化委員はパブリック TLS 仕様を生成します。 バージョンの Windows でどの TLS や SSL のバージョンがサポートされているについては、次を参照してください。[TLS/SSL (Schannel SSP) のプロトコル](https://msdn.microsoft.com/en-us/library/windows/desktop/mt808159(v=vs.85).aspx)します。 次の表は、TLS バージョンごとの仕様を示します。 各仕様には、に関する情報が含まれています。

-   TLS レコード プロトコル

-   TLS ハンドシェイク プロトコル: \-変更暗号仕様プロトコル \-プロトコルのアラート

-   暗号化の計算

-   必須の暗号スイート

-   アプリケーション データのプロトコル

[RFC 5246 - トランスポート層セキュリティ (TLS) プロトコルのバージョン 1.2](http://tools.ietf.org/html/rfc5246)

[RFC 4346 - トランスポート層セキュリティ (TLS) プロトコルのバージョン 1.1](http://tools.ietf.org/html/rfc4346)

[RFC 2246 - TLS プロトコル バージョン 1.0](http://tools.ietf.org/html/rfc2246)

## <a name="BKMK_SessionResumption"></a>TLS セッションの再開
Windows Server 2012 R2 で導入された、Schannel SSP は TLS セッションの再開のサーバー側の部分を実装します。 RFC 5077 のクライアント側の実装は、Windows 8 で追加されました。

頻繁に TLS をサーバーに接続するデバイスは、再接続する必要があります。 TLS セッションの再開は、再開省略形の TLS ハンドシェイクが含まれるために、TLS 接続を確立するのにかかるコストを削減します。 これにより、他の TLS セッションの再開 TLS サーバー グループの再開を試みますが容易になります。 この変更は、Windows Phone および Windows RT デバイスを含め、RFC 5077 をサポートしている任意の TLS クライアントを次の削減効果を示します。

-   サーバー上の削減リソース使用率

-   クライアント接続の効率を向上させ、帯域幅の制限

-   接続の再開のための TLS ハンドシェイクに費やされた時間の短縮

ステートレスな TLS セッションの再開の詳細については、IETF のドキュメントを参照してください。[RFC 5077 します。](http://www.ietf.org/rfc/rfc5077)

## <a name="BKMK_AppProtocolNego"></a>アプリケーション プロトコルのネゴシエーション
 Windows Server 2012 R2 および Windows 8.1 ではクライアント側の TLS アプリケーション プロトコルのネゴシエーションのサポートが導入されました。 アプリケーションは、HTTP 2.0 標準開発の一部としてプロトコルを利用することができ、ユーザーは SPDY プロトコルを実行しているアプリを使用して Google、Twitter などのオンライン サービスにアクセスできます。

アプリケーション プロトコルのネゴシエーションのしくみの詳細については、次を参照してください。[トランスポート層セキュリティ (TLS) アプリケーション レイヤー プロトコルのネゴシエーション拡張](http://tools.ietf.org/search/draft-ietf-tls-applayerprotoneg-05)します。

## <a name="BKMK_SNI"></a>TLS が Server Name Indication 拡張機能をサポートします。
Server Name Indication (SNI) 機能は、多数の仮想イメージを 1 台のサーバーで実行しているときに、サーバーの適切な ID を許可するように TLS と SSL プロトコルを拡張します。 仮想ホスティング シナリオでは、(それぞれが異なる可能性がある証明書が) 複数のドメインが 1 つのサーバーでホストされています。 この場合、サーバーには、クライアントに送信する証明書をあらかじめ知る方法がありません。 SNI により、クライアントは、ターゲット ドメインをプロトコル内で事前に通知して、これにより、サーバーを正しく適切な証明書を選択します。

この追加機能。

-   1 つのインターネット プロトコルとポートの組み合わせでの複数の SSL Web サイトをホストすることができます。

-   複数の SSL Web サイトが 1 つの Web サーバーでホストされている場合は、メモリ使用量を削減します。

-   SSL Web サイトに同時に接続できるユーザーします。



