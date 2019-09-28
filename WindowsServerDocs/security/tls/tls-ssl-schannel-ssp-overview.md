---
title: TLS/SSL の概要 (Schannel SSP)
description: Windows Server のセキュリティ
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 51e3886339b7864951b322d210e1a05bef4dc1e1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403364"
---
# <a name="tlsssl-overview-schannel-ssp"></a>TLS/SSL の概要 (Schannel SSP)

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10

IT 担当者向けのこのトピックでは、Schannel セキュリティサービスプロバイダー (SSP) を使用した Windows での TLS と SSL の実装について説明します。これは、実際のアプリケーション、Microsoft の実装の変更点、およびソフトウェアの要件と、Windows Server 2012 および Windows 8 に関するその他のリソース。

## <a name="BKMK_OVER"></a>説明
Schannel は、インターネットで標準的に用いられている 2 種類の認証プロトコル、Secure Sockets Layer (SSL) とトランスポート層セキュリティ (TLS) を実装するセキュリティ サポート プロバイダー (SSP) です。

セキュリティ サポート プロバイダー インターフェイス (SSPI) は、認証など、セキュリティ関係の機能を実行するために Windows システムで用いられる API の 1 種です。 SSPI は、Schannel SSP を含む複数の Ssp に共通のインターフェイスとして機能します。

TLS バージョン1.0、1.1、1.2、SSL バージョン2.0 と3.0、データグラムトランスポート層セキュリティ @no__t-no__t-1 プロトコルバージョン1.0、プライベート通信トランスポート \(PCT @ no__t プロトコルは、公開キー暗号化に基づいていますが、このようになります。 Schannel 認証プロトコル スイートは、これらのプロトコルを備えています。 どの Schannel プロトコルでも、クライアント/サーバー モデルが使用されています。

## <a name="BKMK_APP"></a>プログラム
ネットワークを管理するにあたっての問題の 1 つは、アプリケーション間で信頼できないネットワークを経由して送信されるデータのセキュリティを確保することです。 TLS と SSL を使用してサーバーとクライアントコンピューターを認証し、そのプロトコルを使用して認証されたパーティ間のメッセージを暗号化することができます。

たとえば、TLS/SSL を使うと次のようなことができます。

-   E コマース Web サイトとのトランザクションの SSL による保護
-   SSL で保護された Web サイトにアクセスするクライアントの認証
-   リモート アクセス
-   SQL アクセス
-   [電子メール]

## <a name="BKMK_SOFT"></a>必要性
TLS および SSL プロトコルは、クライアント/サーバーモデルを使用し、公開キー基盤を必要とする証明書認証に基づいています。

## <a name="BKMK_INSTALL"></a>サーバーマネージャー情報
TLS、SSL、または Schannel を実装するために必要な構成手順はありません。

## <a name="see-also"></a>関連項目 ##

-   [Schannel セキュリティパッケージ](https://docs.microsoft.com/windows/desktop/com/schannel)
-   [セキュリティで保護されたチャネル](https://docs.microsoft.com/windows/desktop/SecAuthN/secure-channel)
-   [トランスポート層セキュリティプロトコル](https://docs.microsoft.com/windows/desktop/SecAuthN/transport-layer-security-protocol)
