---
title: "Kerberos 認証の概要"
description: "Windows Server のセキュリティ"
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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="kerberos-authentication-overview"></a>Kerberos 認証の概要

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

Kerberos は、ユーザーまたはホストの身元を確認するために使用する認証プロトコルです。 このトピックには、Windows Server 2012 および Windows 8 での Kerberos 認証に関する情報が含まれています。

## <a name="BKMK_OVER"></a>機能の説明
The Windows Server operating systems implement the Kerberos version 5 authentication protocol and extensions for public key authentication, transporting authorization data, and delegation. Kerberos 認証クライアントが実装されているセキュリティ サポート プロバイダーとして \(SSP\)、およびそれをセキュリティ サポート プロバイダー インターフェイス \(SSPI\) を通じてアクセスできます。 初回ユーザー認証は Winlogon シングル sign\ のアーキテクチャと統合されています。

The Kerberos Key Distribution Center \(KDC\) is integrated with other Windows Server security services that run on the domain controller. KDC では、そのセキュリティ アカウント データベースとして、ドメインの Active Directory ドメイン サービス データベースを使用します。 Active Directory ドメイン サービスでは、ドメインまたはフォレスト内の既定の Kerberos 実装に必要です。

## <a name="kerb_tr_Kerb_Benefits"></a>実際の適用
Kerberos \servername ベースの認証を使用する利点は次のとおりです。

-   **委任された認証します。**

    Windows オペレーティング システムで実行されるサービスは、クライアントの代理でリソースにアクセスするときに、クライアント コンピューターを偽装できます。 多くの場合、サービスは、ローカル コンピューター上のリソースにアクセスして、クライアントに対する処理を完了できます。 クライアント コンピューターをサービスに認証、NTLM と Kerberos プロトコルは、サービスがクライアント コンピューターにローカルに偽装する必要がある認証情報を提供します。 ただし、分散アプリケーションによっては、front\ バックエンド サービスは他のコンピューターで back\ バックエンド サービスに接続すると、クライアント コンピューターの ID を使用する必要がありますように設計されています。 Kerberos 認証は、他のサービスに接続するときに、そのクライアントの代わりとして、サービスをできる委任メカニズムをサポートしています。

-   **シングル サインオンします。**

    Kerberos を使用してドメイン内またはフォレスト内の認証には、ユーザーまたはサービス管理者の資格情報に対する複数の要求なしで許可されているリソースへのアクセスができるようにします。 初期のドメインのサインオン Winlogon を通じて後のリソースへのアクセスが試行されるたびに、Kerberos は、フォレスト内のすべての資格情報を管理します。

-   **相互運用性。**

    マイクロソフトによる Kerberos V5 プロトコルの実装は、インターネット技術標準化委員 \(IETF\) に推奨される standards\ トラック仕様に基づいています。 その結果、Windows オペレーティング システムで Kerberos プロトコルの基盤となって、Kerberos プロトコルが認証の使用は、他のネットワークとの相互運用性。 さらに、Microsoft は、Kerberos プロトコルを実装するための Windows プロトコルのドキュメントを公開します。 ドキュメントには、技術要件、制限事項、依存関係、および Kerberos プロトコルの Microsoft の実装についてや、windows に固有のプロトコルの動作が含まれています。

-   **サーバーに対するより効率的な認証します。**

    Kerberos、する前に NTLM 認証可能性があります、アプリケーション サーバー、ドメイン コントローラーに接続する必要がありますを認証できるすべてのクライアント コンピューターまたはサービスです。 Kerberos プロトコルと更新可能なセッション チケット pass\ を通じて認証の代わりにします。 サーバーがドメイン コントローラーに移動する必要はありません \ (特記のない特権属性証明書 \(PAC\)\) を検証する必要があります。 代わりに、サーバーは、クライアントから提示された資格情報を調べることによって、クライアント コンピューターを認証できます。 クライアント コンピューターでは、特定のサーバーに対する資格情報を一度入手したらでき、それらの資格情報をネットワーク ログオン セッション全体で再利用することができます。

-   **相互認証します。**

    一方のネットワーク接続のパーティーは、Kerberos プロトコルを使用して、もう一方の端にパーティーが本物であるエンティティであるを確認できます。 NTLM は、サーバーの身元を確認または別の身元を検証する 1 つのサーバーを有効にするクライアントを有効になりません。 NTLM 認証は、正規のものであると想定されたサーバーのネットワーク環境向けに設計されました。 Kerberos プロトコルには、このような想定はありません。

## <a name="see-also"></a>参照してください。
[Windows 認証の概要](../windows-authentication/windows-authentication-overview.md)


