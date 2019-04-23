---
title: TLS/SSL (Schannel SSP) の概要
description: Windows Server のセキュリティ
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
ms.date: 05/16/2018
ms.openlocfilehash: a6571e5e06e07fd62ad4cf39bab322b45c90a9f9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848603"
---
# <a name="tlsssl-overview-schannel-ssp"></a>TLS/SSL (Schannel SSP) の概要

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10

このトピックで、IT プロフェッショナルが Windows Schannel セキュリティ サービス プロバイダー (SSP) を使用して、実際の適用を記述することで、TLS と SSL の実装を紹介変更では、Microsoft の実装、およびソフトウェア要件は、plusWindows Server 2012 および Windows 8 の他のリソース。

## <a name="BKMK_OVER"></a>説明
Schannel は、インターネットで標準的に用いられている 2 種類の認証プロトコル、Secure Sockets Layer (SSL) とトランスポート層セキュリティ (TLS) を実装するセキュリティ サポート プロバイダー (SSP) です。

セキュリティ サポート プロバイダー インターフェイス (SSPI) は、認証など、セキュリティ関係の機能を実行するために Windows システムで用いられる API の 1 種です。 Schannel SSP を含む、いくつかの Ssp を共通のインターフェイスとして SSPI 関数

TLS バージョン 1.0、1.1、1.2、SSL バージョン 2.0、3.0、データグラム トランスポート層のセキュリティと\(DTLS\)プロトコル バージョン 1.0、およびプライベート通信トランスポート\(PCT\)プロトコルに基づく公開キーの暗号化。 Schannel 認証プロトコル スイートは、これらのプロトコルを備えています。 どの Schannel プロトコルでも、クライアント/サーバー モデルが使用されています。

## <a name="BKMK_APP"></a>アプリケーション
ネットワークを管理するにあたっての問題の 1 つは、アプリケーション間で信頼できないネットワークを経由して送信されるデータのセキュリティを確保することです。 TLS と SSL を使用するには、サーバーとクライアント コンピューターを認証し、プロトコルを使用して、認証された当事者間でメッセージを暗号化します。

たとえば、TLS/SSL を使うと次のようなことができます。

-   E コマース Web サイトとのトランザクションの SSL による保護
-   SSL で保護された Web サイトにアクセスするクライアントの認証
-   リモート アクセス
-   SQL アクセス
-   [電子メール]

## <a name="BKMK_SOFT"></a>要件
TLS と SSL プロトコルは、クライアント/サーバー モデルを使用され、証明書の認証は、公開キー インフラストラクチャが必要に基づいています。

## <a name="BKMK_INSTALL"></a>サーバー マネージャーの情報
TLS、SSL、Schannel を実装するために必要な構成手順はありません。

## <a name="see-also"></a>関連項目 ##

-   [Schannel セキュリティ パッケージ](https://docs.microsoft.com/windows/desktop/com/schannel)
-   [セキュリティで保護されたチャネル](https://docs.microsoft.com/windows/desktop/SecAuthN/secure-channel)
-   [トランスポート層セキュリティ プロトコル](https://docs.microsoft.com/windows/desktop/SecAuthN/transport-layer-security-protocol)
