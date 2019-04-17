---
title: "Kerberos の制約付き委任の概要"
description: "Windows Server のセキュリティ"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-kerberos
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 51923b0a-0c1a-47b2-93a0-d36f8e295589
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: e90aa5e395fa43a3f94cccb13444fd6991ac1074
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="kerberos-constrained-delegation-overview"></a>Kerberos の制約付き委任の概要

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

IT プロフェッショナル向けのこの概要トピックでは、Windows Server 2012 R2 および Windows Server 2012 での Kerberos の制約付き委任に対する新機能について説明します。

## <a name="feature-description"></a>機能の説明
Kerberos の制約付き委任は、サービスで使用可能な委任の安全な形を提供する Windows Server 2003 で導入されました。 構成されている場合、制約付き委任は、ユーザーの代理として動作できる、指定したサーバーをサービスを制限します。 これは、サービスに対してドメイン アカウントを構成するドメイン管理者特権が必要で、単一のドメインにアカウントを制限します。 今日の企業でフロント エンド サービスは、ドメイン内のサービスだけとの統合に制限するのには設計されていません。

ドメイン管理者がサービスを構成する以前のオペレーティング システム、サービス管理者がありませんでした便利な方法を所有しているリソース サービスに委任されるフロント エンド サービスを知ること。 され、リソース サービスに委任でした任意のフロント エンド サービスが潜在的な攻撃ポイントを表示します。 フロント エンド サービスをホストするサーバーが侵害された、リソース サービスに委任するように構成された場合は、リソース サービスが侵害も可能性があります。

Windows Server 2012 R2 および Windows Server 2012 で、サービスの制約付き委任を構成する機能が変更されましたドメイン管理者からサービス管理者にします。 これにより、バックエンド サービス管理者は、許可またはフロント エンド サービスを拒否します。

制約付き委任の詳細については、Windows Server 2003 で導入されたを参照してください[Kerberos プロトコル遷移と制約付き委任](https://technet.microsoft.com/library/cc739587(v=ws.10))します。

Windows Server 2012 R2 および Windows Server 2012 における Kerberos プロトコルの実装には、制約付き委任向けの特別の拡張機能が含まれています。  User to Proxy (S4U2Proxy) 用サービスにより、バックエンド サービスにキー配布センター (KDC) からのサービス チケットを取得するユーザー用の Kerberos サービス チケットを使用するサービスです。 これらの拡張制約付き委任を別のドメイン内になる可能性がバックエンド サービスのアカウントで構成します。 これらの拡張機能の詳細については、次を参照してください。[\[MS-SFU\]: Kerberos プロトコル拡張: Service for User および制約付き委任プロトコルの仕様](https://msdn.microsoft.com/library/cc246071(PROT.13).aspx)Msdn にします。

## <a name="practical-applications"></a>実際の適用
制約付き委任、サービス管理者を指定し、アプリケーション サービスがユーザーの代理として動作できる範囲を制限することによってアプリケーションの信頼境界を適用できます。 フロント エンド サービス アカウントは、バックエンド サービスに委任できますサービス管理者を構成できます。

Windows Server 2012 R2 および Windows Server 2012 でのドメイン間で制約付き委任をサポートすることによって、他のドメイン内のサーバーに対する認証に制約付き委任を使用する Microsoft Internet Security と Acceleration (ISA) Server、Microsoft Forefront Threat Management Gateway、Microsoft Exchange Outlook Web Access (OWA)、および Microsoft SharePoint Server などのフロント エンド サービスを構成できます。 これによりのサポート ドメイン間でサービス ソリューションで既存の Kerberos インフラストラクチャを使用します。 Kerberos の制約付き委任は、ドメイン管理者またはサービス管理者を管理できます。

## <a name="new-and-changed-functionality"></a>新機能と変更された機能
**ドメイン間でリソースに基づく制約付き委任**

Kerberos の制約付き委任を使用して、同じドメイン内、フロント エンド サービスとリソース サービスがにない場合に、制約付き委任を提供することができます。 サービス管理者は、リソース サービスのアカウント オブジェクト上のユーザーを偽装できるフロント エンド サービスのドメイン アカウントを指定して、新しい委任を構成することです。

**この変更はどのような値を追加しますか。**

ドメイン間で制約付き委任をサポートすることによって、無制限の委任を使用するのではなく、その他のドメイン内のサーバーを認証に制約付き委任を使用するサービスを構成することができます。 任意のサービスに委任するフロント エンド サービスを信頼することがなく、既存の Kerberos インフラストラクチャを使用して、ドメイン サービス ソリューション全体の認証のサポートを提供します。

**動作の相違点**

基盤となるプロトコルに変更は、ドメイン間で制約付き委任を使用します。 Windows Server 2012 R2 および Windows Server 2012 における Kerberos プロトコルの実装には、ユーザーのサービスを to Proxy (S4U2Proxy) プロトコルの拡張機能が含まれています。 これは、バックエンド サービスにキー配布センター (KDC) からのサービス チケットを取得するユーザー用の Kerberos サービス チケットを使用するサービスを許可する、Kerberos プロトコルに対する拡張機能のセットです。

これらの拡張機能の実装については、次を参照してください。[\[MS-SFU\]: Kerberos プロトコル拡張: Service for User および制約付き委任プロトコルの仕様](https://msdn.microsoft.com/library/cc246071(PROT.10).aspx)MSDN にします。

Kerberos の委任で、転送されたチケット保証チケット (TGT) サービスと比較してユーザー (S4U) 拡張機能の基本的なメッセージ シーケンスの詳細については、セクションを参照してください。[1.3.3 プロトコルの概要](https://msdn.microsoft.com/library/cc246080(v=prot.10).aspx)で [MS-SFU]: Kerberos プロトコル拡張: Service for User および制約付き委任プロトコルの仕様です。

ユーザーの代理でフロント エンド サービス アクセスを許可するようにリソース サービスを構成するのには、Windows PowerShell コマンドレットを使用します。

-   プリンシパルの一覧を取得するを使用して、**Get-adcomputer**、**Get-adserviceaccount**、および**Get-aduser**コマンドレットと、**プロパティ PrincipalsAllowedToDelegateToAccount**パラメーター。

-   リソース サービスを構成するのには、使用、**New-adcomputer**、**New-adserviceaccount**、**New-aduser**、**Set-adcomputer**、**Set-adserviceaccount**、および**Set-aduser**コマンドレットと、**PrincipalsAllowedToDelegateToAccount**パラメーター。

## <a name="BKMK_SOFT"></a>ソフトウェアの要件
リソースに基づく制約付き委任は、Windows Server 2012 R2 および Windows Server 2012 を実行するドメイン コントローラー上でのみ構成できますが、混在モードのフォレスト内で適用することができます。

Windows Server 2012 上で実行するユーザーのアカウント ドメインの参照パス、フロント エンドおよびバックエンド ドメイン間で Windows Server より前のオペレーティング システムを実行しているすべてのドメイン コントローラーに次の修正プログラムを適用する必要があります: 制約付き委任 KDC_ERR_POLICY エラーを Windows Server 2008 R2 ベースのドメイン コントローラーが存在する環境でのリソースに基づきます。
