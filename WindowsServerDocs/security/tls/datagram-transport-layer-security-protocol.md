---
title: "データグラム トランスポート層セキュリティ プロトコル"
description: "Windows Server のセキュリティ"
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
ms.date: 10/12/2016
ms.openlocfilehash: 31c1cf1f3218c0511a4407b560be30d0c6f86233
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# データグラム トランスポート層セキュリティ プロトコル

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

IT プロフェッショナル向けのこのリファレンス トピックでは、データグラム トランスポート層セキュリティ (DTLS) プロトコルは、Schannel セキュリティ サポート プロバイダー (SSP) の一部であるについて説明します。

## <a name="BKMK_DTLS"></a>
Schannel SSP では、Windows Server 2012 および Windows 8 で導入された、DTLS プロトコルは、データグラム プロトコルの通信プライバシーを提供します。 バージョンはバージョンの Windows でサポートされているどの DTLS については、次を参照してください。 [TLS/SSL (Schannel SSP) のプロトコル](https://msdn.microsoft.com/en-us/library/windows/desktop/mt808159(v=vs.85).aspx)します。 このプロトコルには、盗聴、改ざん、メッセージ偽造などを防ぐように設計された方法で通信するために、クライアントとサーバーのアプリケーションができます。 DTLS プロトコルは、トランスポート層セキュリティ (TLS) プロトコルに基づいており、IPsec を使用する必要が少なく、カスタム アプリケーション層のセキュリティ プロトコルを設計または同等のセキュリティ保証を提供します。

データグラムは、ゲームまたはセキュリティで保護されたビデオ会議などのメディアをストリーミングで共通です。 開発者は、クライアントとサーバー間の通信をセキュリティで保護する Windows 認証セキュリティ サポート プロバイダー インターフェイス (SSPI) モデルのコンテキスト内で DTLS プロトコルを使用するアプリケーションを開発できます。 DTLS プロトコルは、ユーザー データグラム プロトコル (UDP) 上に構築されています。 DTLS は、新しいセキュリティ発明を最小限に抑えるとコードとインフラストラクチャの再利用の量を最大化することができる限り TLS にする設計されています。

構成可能な暗号スイートでは、ほぼ同様 TLS を構成することができます。 RC4 は許可されていません。 Schannel は引き続き Cryptography Next Generation (CNG) を使用します。 これは、Windows Vista で導入された、FIPS 140 認定の活用します。

## 参照してください。

[IETF RFC 4347 データグラム トランスポート層セキュリティ](http://tools.ietf.org/html/rfc4347)


