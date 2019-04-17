---
title: "Windows 認証のアーキテクチャ"
description: "Windows Server のセキュリティ"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-windows-auth
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 07c9d6bb-9b03-407d-89b6-97c7551b256b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: fd6e2cbc233a91b62e3c8c9caf1154f91c3863ac
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="windows-authentication-architecture"></a>Windows 認証のアーキテクチャ

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

IT プロフェッショナル向けのこの概要トピックでは、Windows 認証の基本的なアーキテクチャ スキームについて説明します。

認証は、ユーザーのログオンまたはサインイン情報システムを検証するプロセスです。 ユーザーの名とパスワードを承認済みリストと比較され、一致が検出されると、そのユーザーのアクセス許可の一覧で指定されている範囲において、アクセスが許可されます。

拡張性に優れたアーキテクチャの一部として、Windows Server オペレーティング システムは、Negotiate、Kerberos プロトコル、NTLM、Schannel (セキュリティで保護されたチャネル)、ダイジェスト認証セキュリティ サポート プロバイダーの既定のセットを実装します。 これらのプロバイダーによって使用されるプロトコルは、ユーザー、コンピューター、およびサービスの認証を有効にして、認証プロセスが安全な方法でリソースにアクセスするには、承認されたユーザーとサービスを有効します。

Windows server では、アプリケーションは、認証のための呼び出しを抽象化するため、SSPI を使用してユーザーを認証します。 このため、開発者は、特定の認証プロトコルの複雑さを理解または自社のアプリケーションの認証プロトコルをビルドするのには必要ありません。

Windows Server オペレーティング システムには、Windows のセキュリティ モデルを構成するセキュリティ コンポーネントのセットが含まれます。 これらのコンポーネントは、アプリケーションが認証および承認なしのリソースへのアクセスを取得できないことを確認します。 次のセクションでは、認証のアーキテクチャの要素について説明します。

### <a name="local-security-authority"></a>ローカル セキュリティ機関
ローカル セキュリティ機関 (LSA) を認証し、ローカル コンピューターにユーザーがサインインしている保護されたサブシステムです。 さらに、LSA に関する情報を保持すべての側面のローカル セキュリティ コンピューター (このような側面は、ローカル セキュリティ ポリシーと呼ばれます総称)。 さまざまなサービス名とセキュリティ識別子 (Sid) の間の変換も提供します。

セキュリティ サブシステムは、セキュリティ ポリシーとコンピューターのシステム上にあるアカウントの追跡します。 場合、ドメイン コントローラー、これらのポリシーおよびアカウントは、ドメイン コントローラーが配置されているドメインに適用されているものです。 これらのポリシーおよびアカウントは、Active Directory に格納されます。 ユーザーの権利を確認し、生成する監査メッセージ、LSA サブシステムがオブジェクトへのアクセスを検証するためのサービスを提供します。

### <a name="security-support-provider-interface"></a>セキュリティ サポート プロバイダー インターフェイス
セキュリティ サポート プロバイダー インターフェイス (SSPI) は、認証、メッセージの整合性、メッセージのプライバシー、およびセキュリティのサービス品質の分散アプリケーション プロトコルの統合セキュリティ サービスを取得する API です。

SSPI は、Generic Security Service API (GSSAPI) の実装です。 SSPI は、分散アプリケーション呼び出すことができます、セキュリティ プロトコルの詳細を知らないうちに認証された接続を取得するいくつかのセキュリティ プロバイダーのいずれかのメカニズムを提供します。

## <a name="see-also"></a>参照してください。

-   [セキュリティ サポート プロバイダー インターフェイスのアーキテクチャ](security-support-provider-interface-architecture.md)

-   [Windows 認証で資格情報の処理](credentials-processes-in-windows-authentication.md)

-   [Windows 認証の技術概要](https://technet.microsoft.com/library/dn169029.aspx)


