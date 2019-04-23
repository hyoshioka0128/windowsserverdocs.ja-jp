---
title: データグラム トランスポート層セキュリティ プロトコル
description: Windows Server のセキュリティ
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: b32ebafff5e41d5c3140f008f6f391852f2f3474
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870793"
---
# <a name="datagram-transport-layer-security-protocol"></a>データグラム トランスポート層セキュリティ プロトコル

Windows Server (半期チャネル)、Windows Server 2016、Windows 10

IT プロフェッショナル向けのこのリファレンス トピックでは、Schannel セキュリティ サポート プロバイダー (SSP) の一部であるデータグラム トランスポート層セキュリティ (DTLS) プロトコルについて説明します。

## <a name="BKMK_DTLS"></a>
Windows Server 2012 と Windows 8 での Schannel SSP で導入された、DTLS プロトコルは、データグラム プロトコルの通信プライバシーを提供します。 バージョンは、Windows のバージョンでサポートされているどの DTLS については、次を参照してください。 [in TLS/SSL (Schannel SSP) プロトコル](https://msdn.microsoft.com/en-us/library/windows/desktop/mt808159(v=vs.85).aspx)します。 クライアントとサーバーのアプリケーションはこのプロトコルにより、盗聴、改ざん、メッセージ偽造などを防ぐように設計された方法で通信できます。 DTLS プロトコルは、トランスポート層セキュリティ (TLS) プロトコルを基にしたものであり、TLS と同等のセキュリティ保証を提供します。これにより、IPsec を使う必要性が低下すると共に、アプリケーション層のセキュリティ プロトコルのカスタム設計が可能になります。

データグラムは、ストリーミング メディア、ゲームやセキュリティで保護されたビデオ会議などで共通です。 開発者は、クライアントとサーバー間の通信をセキュリティで保護する、Windows 認証セキュリティ サポート プロバイダー インターフェイス (SSPI) モデルのコンテキスト内で DTLS プロトコルを使用するアプリケーションを開発できます。 DTLS プロトコルは、ユーザー データグラム プロトコル (UDP) の上に構築されています。 DTLS はできるだけ最小限に抑える新しいセキュリティ発明と、コードとインフラストラクチャの再利用量を最大化する TLS と同等のように設計されています。

構成で利用可能な暗号スイートとほぼ TLS 用に構成することができます。 RC4 は許可されていません。 Schannel は、Cryptography Next Generation (CNG) を使用し続けます。 これは、Windows Vista で導入された FIPS 140 認定を利用します。

## <a name="see-also"></a>関連項目

[IETF RFC 4347 データグラム トランスポート層セキュリティ](http://tools.ietf.org/html/rfc4347)


