---
title: Windows 認証のアーキテクチャ
description: Windows Server のセキュリティ
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855863"
---
# <a name="windows-authentication-architecture"></a>Windows 認証のアーキテクチャ

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

IT プロフェッショナル向けのこの概要トピックでは、Windows 認証の基本的なアーキテクチャ パターンについて説明します。

認証は、ユーザーのログオンやサインイン情報、システムを検証するプロセスです。 ユーザーの名とパスワードは、承認されたリストと比較され、一致が検出されると、そのユーザーのアクセス許可の一覧で指定したエクステントにアクセスが許可します。

拡張可能なアーキテクチャの一部として、Windows Server オペレーティング システムは、Negotiate、Kerberos プロトコル、NTLM、Schannel (セキュリティで保護されたチャネル)、ダイジェスト認証セキュリティ サポート プロバイダーの既定のセットを実装します。 これらのプロバイダーによって使用されるプロトコルは、ユーザー、コンピューター、およびサービスの認証を有効にして、認証プロセスは、安全な方法でリソースにアクセスするには、承認されたユーザーとサービスを使用します。

Windows server では、アプリケーションは認証への呼び出しを抽象化するため、SSPI を使用してユーザーを認証します。 したがって、開発者は、特定の認証プロトコルの複雑さを理解またはアプリケーションに認証プロトコルをビルドするのには必要ありません。

Windows Server オペレーティング システムには、Windows のセキュリティ モデルを構成するセキュリティ コンポーネントのセットが含まれます。 これらのコンポーネントは、アプリケーションが認証と承認のないリソースへのアクセスを取得できないことを確認します。 次のセクションでは、認証のアーキテクチャの要素について説明します。

### <a name="local-security-authority"></a>ローカル セキュリティ機関
ローカル セキュリティ機関 (LSA) では、保護されたサブシステムを認証し、ローカル コンピューターにユーザーがサインインです。 さらに、LSA はあらゆる側面に関する情報ローカル セキュリティのコンピューターで (これらの側面は、ローカル セキュリティ ポリシーとしてまとめて呼ばれます) を保持します。 また、さまざまなサービス名とセキュリティ識別子 (Sid) の間の変換も提供します。

セキュリティ ポリシーとは、コンピューター システム上にあるアカウント、セキュリティ サブシステムの追跡。 場合は、ドメイン コント ローラー、これらのポリシーおよびアカウントはドメイン コント ローラーが配置されているドメインの有効となっています。 これらのポリシーとアカウントは、Active Directory に格納されます。 監査メッセージをユーザーの権限をチェックし、生成する、LSA サブシステムは、オブジェクトへのアクセスを検証するためのサービスを提供します。

### <a name="security-support-provider-interface"></a>セキュリティ サポート プロバイダー インターフェイス
セキュリティ サポート プロバイダー インターフェイス (SSPI) は、認証、メッセージの整合性、メッセージのプライバシーおよびセキュリティ サービスが品質の任意の分散アプリケーション プロトコル用の統合のセキュリティ サービスを取得する API です。

SSPI は、Generic Security Service API (GSSAPI) の実装です。 SSPI は、使用される分散アプリケーションを呼び出すことができます、セキュリティ プロトコルの詳細の知識がなくても認証された接続を取得するいくつかのセキュリティ プロバイダーのいずれかのメカニズムを提供します。

## <a name="see-also"></a>関連項目

-   [セキュリティ サポート プロバイダー インターフェイスのアーキテクチャ](security-support-provider-interface-architecture.md)

-   [Windows 認証で資格情報の処理](credentials-processes-in-windows-authentication.md)

-   [Windows 認証の技術概要](https://technet.microsoft.com/library/dn169029.aspx)


