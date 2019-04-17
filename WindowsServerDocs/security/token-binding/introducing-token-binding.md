---
title: "トークンのバインドの概要"
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 4623a48c-cefd-4a27-9173-2af58ac212f2
manager: alanth
author: justinha
ms.technology: security-authentication
ms.date: 11/09/2016
ms.openlocfilehash: 2a0bb8c75fe3ca7f7befe0bd67eb3d363a5ad7a9
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="introducing-token-binding"></a>トークンのバインドの概要

>適用対象: Windows Server 2016 および Windows 10

TLS レイヤーとリプレイ攻撃のトークンの盗難の軽減に暗号によって、セキュリティ トークンをバインドするには、アプリケーションとサービスでは、トークンのバインドのプロトコル。 長期間維持される、一意に識別 TLS [RFC5246] バインドは、複数の TLS セッションとの接続にまたがることができます。

バージョンのサポート:

- Windows 10 バージョン 1507 – 既定でオフ
    - トークンのバインドのプロトコルが追加された[[下書き-ietf-tokbind-プロトコル-01]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/01/)
    - WinInet & HTTP.SYS [[下書き-ietf-tokbind-https-01]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/01/)
- Windows 10 バージョン 1511 および 1607 および Windows Server 2016 – で既定では
    - トークンの更新のバインドのプロトコル[[下書き-ietf-tokbind-プロトコル-01]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/01/)
    - 追加のトークンのバインド ネゴシエーションの TLS 拡張[[下書き-popov-tokbind-ネゴシエーション-00]](https://tools.ietf.org/html/draft-popov-tokbind-negotiation-00)
    - WinInet & HTTP.SYS [[下書き-ietf-tokbind-https-02]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/02/)
- Windows 10 バージョン 1507 更新プログラムのサービスで[KB4034668](https://support.microsoft.com/kb/KB4034668)、Windows 10 更新プログラムのサービスでバージョン 1511 [KB4034660](https://support.microsoft.com/kb/KB4034660)、Windows 10 バージョン 1607 および Windows Server 2016 の更新プログラムのサービス[KB4034658](https://support.microsoft.com/kb/KB4034658)で既定ではトークンのバインドのプロトコルの version 0.10 – をサポート
    - トークンの更新のバインドのプロトコル[[下書き-ietf-tokbind-プロトコル-10]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/10/)
    - 追加のトークンのバインド ネゴシエーションの TLS 拡張[[下書き-ietf-tokbind-ネゴシエーション-05]](https://tools.ietf.org/html/draft-ietf-tokbind-negotiation-05)
    - WinInet & HTTP.SYS [[下書き-ietf-tokbind-https-06]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/06/)
- Windows 10 バージョン 1703 トークンのバインドのプロトコルの version 0.10 – で既定でサポートします。
    - トークンの更新のバインドのプロトコル[[下書き-ietf-tokbind-プロトコル-10]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/10/)
    - 追加のトークンのバインド ネゴシエーションの TLS 拡張[[下書き-ietf-tokbind-ネゴシエーション-05]](https://tools.ietf.org/html/draft-ietf-tokbind-negotiation-05)
    - WinInet & HTTP.SYS [[下書き-ietf-tokbind-https-06]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/06/)
    - 仮想化ベースのセキュリティを有効になっていると、Windows デバイスが実行中のオペレーティング システムから分離された保護環境でトークンのバインドのキーが保管されます。

ASP .NET のサポートについてを参照することができます、[.NET Framework リファレンス ソース](https://referencesource.microsoft.com/#System.Web/ITlsTokenBindingInfo.cs,4a5e5668f5c31170)します。 

についての .NET Framework は、次のトピックを参照してください。

- [ネットワークの機能拡張](https://blogs.msdn.microsoft.com/dotnet/2015/11/30/net-framework-4-6-1-is-now-available/#networking)

- [.NET TokenBinding クラス](https://msdn.microsoft.com/library/system.security.authentication.extendedprotection.tokenbinding.aspx)
