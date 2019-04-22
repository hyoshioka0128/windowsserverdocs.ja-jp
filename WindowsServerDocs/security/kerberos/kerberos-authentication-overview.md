---
title: Kerberos Authentication Overview
description: Windows Server のセキュリティ
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-kerberos
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 646c6309-e865-4be2-b415-44dd125af5c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 9f8878fb959c34663b1e1f3858fa7e0b6e7b6105
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824113"
---
# <a name="kerberos-authentication-overview"></a>Kerberos Authentication Overview

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

Kerberos は、ユーザーまたはホストの身元を確認するために使用される認証プロトコルです。 このトピックでは、Windows Server 2012 および Windows 8 で Kerberos 認証に関する情報を格納します。

## <a name="BKMK_OVER"></a>機能の説明
Windows Server オペレーティング システムには、公開キー認証、承認データの転送、委任のために、Kerberos Version 5 認証プロトコルと拡張機能が実装されています。 Kerberos 認証クライアントは、セキュリティ サポート プロバイダーとして実装\(SSP\)、セキュリティ サポート プロバイダー インターフェイスを使用してアクセスすることができますと\(SSPI\)します。 初期のユーザー認証は Winlogon シングル サインオンと統合\-アーキテクチャ。

Kerberos キー配布センター \(KDC\)はドメイン コント ローラー上で実行されるその他の Windows Server セキュリティ サービスと統合します。 KDC では、そのセキュリティ アカウント データベースとして、ドメインの Active Directory Domain Services データベースを使用します。 ドメインまたはフォレスト内の既定の Kerberos 実装には、Active Directory Domain Services が必要です。

## <a name="kerb_tr_Kerb_Benefits"></a>実際の適用
ドメインに対して Kerberos を使用して、メリットが得られる\-ベースの認証には。

-   **委任された認証。**

    Windows オペレーティング システムで実行されるサービスは、クライアントの代理でリソースにアクセスするときに、クライアント コンピューターを偽装できます。 多くの場合、サービスは、ローカル コンピューター上のリソースにアクセスしてクライアントに対する処理を完了できます。 クライアント コンピューターがサービスに対して認証を行うとき、NTLM と Kerberos プロトコルは、サービスがクライアント コンピューターをローカルに偽装するために必要な承認情報を提供します。 しかし、一部の分散アプリケーションを設計ようにフロント\-エンド サービスがバックアップに接続するときに、クライアント コンピューターの id を使用する必要があります\-他のコンピューター上のサービスを終了します。 Kerberos 認証は、サービスがクライアントの代わりとして他のサービスに接続できる委任メカニズムをサポートしています。

-   **シングル サインオン。**

    ドメイン内またはフォレスト内で Kerberos 認証を使用すると、ユーザーまたはサービスは、管理者によって許可されたリソースに、資格情報を繰り返し要求されることなくアクセスできます。 最初に Winlogon を使用してドメインにサインオンした後は、フォレスト内でリソースへのアクセスが試行されるたびに、Kerberos が資格情報を管理します。

-   **相互運用性。**

    Microsoft による Kerberos V5 プロトコルの実装は標準に基づく\-追跡に、Internet Engineering Task Force は推奨されている仕様\(IETF\)します。 そのため、Windows オペレーティング システムでは、Kerberos プロトコルが認証に使用される他のネットワークとの相互運用性に対しては、Kerberos プロトコルが基盤になります。 さらに、Microsoft は、Kerberos プロトコルを実装するために Windows プロトコルのドキュメントを公開しています。 ドキュメントには、技術的な要件、制限事項、依存関係、および Windows が含まれています。\-Kerberos プロトコルの Microsoft の実装の特定のプロトコルの動作。

-   **サーバーに対する認証をより効率的です。**

    Kerberos の前は NTLM 認証を使用できましたが、アプリケーション サーバーはすべてのクライアント コンピューターやサービスを認証するためにドメイン コント ローラーに接続する必要がありました。 更新可能なセッション チケットは Kerberos プロトコルとパスを置き換える\-認証を使用します。 サーバーがドメイン コント ローラーに移動する必要はありません\(特権属性証明書を検証する必要がある場合を除き、 \(PAC\)\)します。 その代わりに、サーバーは、クライアント コンピューターから提示された資格情報を調べてクライアントを認証できます。 クライアント コンピューターは特定のサーバーに対する資格情報を一度入手したら、それをネットワーク ログオン セッション全体で再利用できます。

-   **相互認証。**

    Kerberos プロトコルを使用すると、ネットワーク接続の一方のエンティティは、相手側が本物のエンティティであることを検証できます。 NTLM は、サーバーの id を確認します。 または、別の id を確認する 1 つのサーバーを有効にするクライアントを有効になりません。 NTLM 認証は、サーバーが本物であることが前提となっているネットワーク環境向けの方式でした。 Kerberos プロトコルにはこのような前提はありません。

## <a name="see-also"></a>関連項目
[Windows 認証の概要](../windows-authentication/windows-authentication-overview.md)


