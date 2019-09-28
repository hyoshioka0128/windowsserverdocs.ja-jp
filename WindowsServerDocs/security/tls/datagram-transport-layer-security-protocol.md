---
title: データグラム トランスポート層セキュリティ プロトコル
description: Windows Server のセキュリティ
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: security-tls-ssl
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 57b8873a-ad9c-4f2c-93e0-a2af352c6965
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 05/16/2018
ms.openlocfilehash: f603dc0c5616619088537ffcbd06f64baece0e23
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402297"
---
# <a name="datagram-transport-layer-security-protocol"></a>データグラム トランスポート層セキュリティ プロトコル

Windows Server (半期チャネル)、Windows Server 2016、Windows 10

IT プロフェッショナル向けのこのリファレンストピックでは、Schannel セキュリティサポートプロバイダー (SSP) の一部であるデータグラムトランスポート層セキュリティ (DTLS) プロトコルについて説明します。

## <a name="BKMK_DTLS"></a>
Windows Server 2012 および Windows 8 の Schannel SSP で導入された DTLS プロトコルは、データグラムプロトコルの通信プライバシーを提供します。 Windows のバージョンでサポートされている DTLS のバージョンの詳細については、「 [TLS/SSL (SCHANNEL SSP) のプロトコル](https://msdn.microsoft.com/library/windows/desktop/mt808159(v=vs.85).aspx)」を参照してください。 クライアントとサーバーのアプリケーションはこのプロトコルにより、盗聴、改ざん、メッセージ偽造などを防ぐように設計された方法で通信できます。 DTLS プロトコルは、トランスポート層セキュリティ (TLS) プロトコルを基にしたものであり、TLS と同等のセキュリティ保証を提供します。これにより、IPsec を使う必要性が低下すると共に、アプリケーション層のセキュリティ プロトコルのカスタム設計が可能になります。

データグラムは、ゲームやセキュリティで保護されたビデオ会議などのストリーミングメディアに共通です。 開発者は、Windows 認証セキュリティサポートプロバイダインターフェイス (SSPI) モデルのコンテキスト内で DTLS プロトコルを使用して、クライアントとサーバー間の通信をセキュリティで保護するアプリケーションを開発できます。 DTLS プロトコルは、ユーザーデータグラムプロトコル (UDP) の上に構築されています。 DTLS は、新しいセキュリティの発明を最小限に抑え、コードとインフラストラクチャの再利用を最大化するために、できるだけ TLS と同様のものになるように設計されています。

構成に使用できる暗号スイートは、TLS 用に構成できるようになった後に、パターン化されます。 RC4 は許可されていません。 Schannel では、Cryptography Next Generation (CNG) が引き続き使用されます。 これは、Windows Vista で導入された FIPS 140 認定を利用しています。

## <a name="see-also"></a>関連項目

[IETF RFC 4347 データグラムトランスポート層のセキュリティ](http://tools.ietf.org/html/rfc4347)


