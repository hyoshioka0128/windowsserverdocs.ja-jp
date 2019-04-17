---
title: "TLS、SSL (Schannel SSP) の概要"
description: "Windows Server のセキュリティ"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-tls-ssl
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b7b0432-1bef-4912-8c9a-8989d47a4da9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: afd0b70264dba1e720f95e40d3d201c2c5bf1c64
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="tls---ssl-schannel-ssp-overview"></a>TLS、SSL (Schannel SSP) の概要

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

IT プロフェッショナル向けのこのトピックでは、実際の適用例、Microsoft の実装、およびソフトウェア要件、およびその他のリソースの変更の Windows Server 2012 および Windows 8 を記述することで、Schannel セキュリティ サービス プロバイダー (SSP) を使って Windows に TLS と SSL の実装が導入されています。

**Did you mean:**

-   [Schannel セキュリティ パッケージ](https://msdn.microsoft.com/library/ms678421.aspx)

-   [セキュリティで保護されたチャネル](https://msdn.microsoft.com/library/windows/desktop/aa380123.aspx)

-   [トランスポート層セキュリティ プロトコル](https://msdn.microsoft.com/library/windows/desktop/aa380516.aspx)

## <a name="BKMK_OVER"></a>Tls \ssl \(Schannel\) 説明
Schannel は、Secure Sockets Layer \(SSL\) とトランスポート層セキュリティ \(TLS\) を実装するセキュリティ サポート プロバイダー \(SSP\) インターネット標準の認証プロトコルです。

セキュリティ サポート プロバイダー インターフェイス \(SSPI\) は、認証を含む security\ に関連する機能を実行する Windows システムで使用される API です。 SSPI は、Schannel SSP を含む、いくつかのセキュリティ サポート プロバイダー \(SSPs\) に共通のインターフェイスとして機能します。

トランスポート層セキュリティ \(TLS\) プロトコル バージョン 1.0、1.1、1.2、Secure Sockets Layer \(SSL\) プロトコルの version 2.0、3.0、データグラム トランスポート層セキュリティ \(DTLS\) バージョン 1.0、および Private 通信トランスポート \(PCT\) プロトコルは、公開キーの暗号化に基づいています。 セキュリティ チャネル \(Schannel\) 認証プロトコル スイートは、これらのプロトコルを提供します。 すべての Schannel プロトコルでは、クライアント/サーバー モデルを使用します。

## <a name="BKMK_APP"></a>実際の適用
ネットワークを管理するときに問題の 1 つは、信頼されていないネットワーク経由でアプリケーション間で送信されるデータのセキュリティ保護します。 Tls \ssl を使用して、サーバーとクライアント コンピューターを認証し、プロトコルを使用して、認証された当事者間のメッセージを暗号化することができます。

たとえばの tls \ssl を使用できます。

-   E\ コマースの Web サイトと SSL\ で保護されたトランザクション

-   SSL\ で保護された Web サイトにアクセス クライアントの認証

-   リモート アクセス

-   SQL アクセス

-   E\ メール

## <a name="BKMK_SOFT"></a>ソフトウェアの要件
Tls \ssl プロトコルは、client\server モデルが使用され、証明書の認証は、公開キー インフラストラクチャが必要ですに基づいています。

## <a name="BKMK_INSTALL"></a>サーバー マネージャー情報
TLS、SSL、Schannel を実装するために必要な構成手順はありません。

