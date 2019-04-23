---
title: トークンのバインドの概要
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 4623a48c-cefd-4a27-9173-2af58ac212f2
manager: alanth
author: justinha
ms.technology: security-authentication
ms.date: 11/09/2016
ms.openlocfilehash: 2a0bb8c75fe3ca7f7befe0bd67eb3d363a5ad7a9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884233"
---
# <a name="introducing-token-binding"></a>トークンのバインドの概要

>適用先:Windows Server 2016 および Windows 10

トークン バインディング プロトコルは、暗号化された TLS レイヤーや再生攻撃をトークンの盗難を軽減するために、セキュリティ トークンをバインドするには、アプリケーションとサービスにできます。 有効期間が長い、一意に識別できる TLS [RFC5246] バインドは、複数の TLS セッションと接続にまたがることができます。

バージョンのサポート:

- Windows 10 バージョン 1507 – 既定ではオフ
    - トークン バインディング プロトコルが追加[[draft-ietf-tokbind-プロトコル-01]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/01/)
    - WinInet & HTTP。HTTP 経由でのトークンのバインドのサポートを SYS [[draft-ietf-tokbind-https-01]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/01/)
- Windows 10、バージョン 1511、1607、および Windows Server 2016 の場合 – 既定では
    - トークン バインディング プロトコルの更新[[draft-ietf-tokbind-プロトコル-01]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/01/)
    - 追加されたトークンのバインドのネゴシエーションの TLS 拡張機能[[draft-popov-tokbind-ネゴシエーション-00]](https://tools.ietf.org/html/draft-popov-tokbind-negotiation-00)
    - WinInet & HTTP。トークンのバインドを更新する HTTP 経由でのサポートを SYS [[draft-ietf-tokbind-https-02]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/02/)
- Windows 10 バージョン 1507 サービス更新プログラムで[KB4034668](https://support.microsoft.com/kb/KB4034668)、Windows 10 バージョン 1511 でサービス更新プログラム[KB4034660](https://support.microsoft.com/kb/KB4034660)、Windows 10、バージョン 1607 および Windows Server 2016 サービス更新プログラムwith[KB4034658](https://support.microsoft.com/kb/KB4034658)で既定ではトークン バインディング プロトコル バージョン 0.10 – をサポート
    - トークン バインディング プロトコルの更新[[draft-ietf-tokbind-プロトコル-10]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/10/)
    - 追加されたトークンのバインドのネゴシエーションの TLS 拡張機能[[draft-ietf-tokbind-ネゴシエーション-05]](https://tools.ietf.org/html/draft-ietf-tokbind-negotiation-05)
    - WinInet & HTTP。トークンのバインドを更新する HTTP 経由でのサポートを SYS [[draft-ietf-tokbind-https-06]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/06/)
- Windows 10 バージョン 1703 トークン バインディング プロトコル バージョン 0.10 – で既定でサポートします。
    - トークン バインディング プロトコルの更新[[draft-ietf-tokbind-プロトコル-10]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/10/)
    - 追加されたトークンのバインドのネゴシエーションの TLS 拡張機能[[draft-ietf-tokbind-ネゴシエーション-05]](https://tools.ietf.org/html/draft-ietf-tokbind-negotiation-05)
    - WinInet & HTTP。トークンのバインドを更新する HTTP 経由でのサポートを SYS [[draft-ietf-tokbind-https-06]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/06/)
    - 仮想化ベースのセキュリティが有効な Windows デバイスは、実行中のオペレーティング システムから分離された保護された環境で、トークンのバインド キーを保持します。

ASP .NET のサポートに関する情報をご覧、 [.NET Framework Reference Source](https://referencesource.microsoft.com/#System.Web/ITlsTokenBindingInfo.cs,4a5e5668f5c31170)します。 

.NET Framework については、次のトピックを参照してください。

- [ネットワークの拡張](https://blogs.msdn.microsoft.com/dotnet/2015/11/30/net-framework-4-6-1-is-now-available/#networking)

- [.NET TokenBinding クラス](https://msdn.microsoft.com/library/system.security.authentication.extendedprotection.tokenbinding.aspx)
