---
title: Kerberos Authentication Overview
description: Windows Server のセキュリティ
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 33712dc8502035bd9e47e1d2bdd4583eb8347dec
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386307"
---
# <a name="kerberos-authentication-overview"></a>Kerberos Authentication Overview

>適用先:Windows Server (半期チャネル)、Windows Server 2016

Kerberos は、ユーザーまたはホストの身元を確認するために使用される認証プロトコルです。 このトピックには、Windows Server 2012 および Windows 8 での Kerberos 認証に関する情報が含まれています。

## <a name="BKMK_OVER"></a>機能の説明
Windows Server オペレーティング システムには、公開キー認証、承認データの転送、委任のために、Kerberos Version 5 認証プロトコルと拡張機能が実装されています。 Kerberos 認証クライアントは、セキュリティサポートプロバイダー @no__t 0SSP @ no__t に実装され、セキュリティサポートプロバイダーインターフェイス \(SSPI @ no__t を使用してアクセスできます。 初期のユーザー認証は、Winlogon single sign @ no__t-0on アーキテクチャに統合されています。

Kerberos キー配布センター @no__t 0KDC @ no__t は、ドメインコントローラーで実行されている他の Windows Server セキュリティサービスと統合されています。 KDC は、そのセキュリティアカウントデータベースとしてドメインの Active Directory Domain Services データベースを使用します。 ドメインまたはフォレスト内の既定の Kerberos 実装には、Active Directory Domain Services が必要です。

## <a name="kerb_tr_Kerb_Benefits"></a>実用的なアプリケーション
ドメイン @ no__t ベースの認証に Kerberos を使用すると、次の利点が得られます。

-   **委任された認証。**

    Windows オペレーティングシステムで実行されるサービスは、クライアントの代わりにリソースにアクセスするときに、クライアントコンピューターの権限を借用できます。 多くの場合、サービスは、ローカル コンピューター上のリソースにアクセスしてクライアントに対する処理を完了できます。 クライアント コンピューターがサービスに対して認証を行うとき、NTLM と Kerberos プロトコルは、サービスがクライアント コンピューターをローカルに偽装するために必要な承認情報を提供します。 ただし、一部の分散アプリケーションは、他のコンピューター上の @ no__t-1end サービスに接続するときに、フロント @ no__t-0end サービスがクライアントコンピューターの id を使用するように設計されています。 Kerberos 認証は、サービスがクライアントの代わりとして他のサービスに接続できる委任メカニズムをサポートしています。

-   **シングルサインオン。**

    ドメイン内またはフォレスト内で Kerberos 認証を使用すると、ユーザーまたはサービスは、管理者によって許可されたリソースに、資格情報を繰り返し要求されることなくアクセスできます。 最初に Winlogon を使用してドメインにサインオンした後は、フォレスト内でリソースへのアクセスが試行されるたびに、Kerberos が資格情報を管理します。

-   **共存.**

    Microsoft による Kerberos V5 プロトコルの実装は、Internet Engineering Task Force \(IETF @ no__t-2 に推奨される標準の @ no__t-0track 仕様に基づいています。 そのため、Windows オペレーティング システムでは、Kerberos プロトコルが認証に使用される他のネットワークとの相互運用性に対しては、Kerberos プロトコルが基盤になります。 さらに、Microsoft は、Kerberos プロトコルを実装するために Windows プロトコルのドキュメントを公開しています。 このドキュメントには、Microsoft による Kerberos プロトコルの実装に関する技術的な要件、制限事項、依存関係、および Windows @ no__t 固有のプロトコルの動作が含まれています。

-   **サーバーに対するより効率的な認証。**

    Kerberos の前は NTLM 認証を使用できましたが、アプリケーション サーバーはすべてのクライアント コンピューターやサービスを認証するためにドメイン コント ローラーに接続する必要がありました。 Kerberos プロトコルを使用すると、更新可能なセッションチケットは、認証によって渡されます。 サーバーは、特権属性証明書を検証する必要がない限り、ドメインコントローラー \(unless 必要はありません。-1PAC @ no__t-2 @ no__t その代わりに、サーバーは、クライアント コンピューターから提示された資格情報を調べてクライアントを認証できます。 クライアント コンピューターは特定のサーバーに対する資格情報を一度入手したら、それをネットワーク ログオン セッション全体で再利用できます。

-   **相互認証。**

    Kerberos プロトコルを使用すると、ネットワーク接続の一方のエンティティは、相手側が本物のエンティティであることを検証できます。 NTLM では、クライアントがサーバーの id を検証したり、サーバーが別のサーバーの id を確認できるようにしたりすることはできません。 NTLM 認証は、サーバーが本物であることが前提となっているネットワーク環境向けの方式でした。 Kerberos プロトコルにはこのような前提はありません。

## <a name="see-also"></a>関連項目
[Windows 認証の概要](../windows-authentication/windows-authentication-overview.md)


