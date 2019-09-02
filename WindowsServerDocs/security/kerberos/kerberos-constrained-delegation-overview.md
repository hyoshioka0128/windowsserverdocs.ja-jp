---
title: Kerberos Constrained Delegation Overview
description: Windows Server のセキュリティ
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
ms.openlocfilehash: 02677c8d9db4129ebbd7edd79027e0a6348372b5
ms.sourcegitcommit: 6f968368c12b9dd699c197afb3a3d13c2211f85b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/26/2019
ms.locfileid: "68544613"
---
# <a name="kerberos-constrained-delegation-overview"></a>Kerberos Constrained Delegation Overview

>適用先:Windows Server (半期チャネル)、Windows Server 2016

IT プロフェッショナル向けのこの概要トピックでは、Windows Server 2012 R2 および Windows Server 2012 での Kerberos の制約付き委任の新機能について説明します。

**機能の説明**

Kerberos の制約付き委任は、サービスで使用できる、より安全な形の委任を提供するために Windows Server 2003 で導入されました。 制約付き委任を構成すると、指定されたサーバーがユーザーの代理として動作できる対象のサービスが制限されます。 これには、サービスに対してドメイン アカウントを構成するためにドメイン管理者特権が必要であり、そのアカウントは 1 つのドメインに制限されます。 今日の企業では、フロントエンドサービスは、ドメイン内のサービスのみとの統合に限定されるように設計されていません。

ドメイン管理者がサービスを構成していた従来のオペレーティング システムでは、サービス管理者には、所有しているリソース サービスに委任されるフロントエンド サービスを把握する有効な手立てがありませんでした。 また、リソース サービスに委任できるフロントエンド サービスは攻撃ポイントになる可能性がありました。 フロントエンド サービスをホストしているサーバーが攻撃を受けたときに、それがリソース サービスに委任されるように構成されていた場合、リソース サービスも危険にさらされる可能性がありました。

Windows Server 2012 R2 および Windows Server 2012 では、サービスの制約付き委任を構成する機能がドメイン管理者からサービス管理者に転送されました。 これにより、バックエンド サービス管理者はフロントエンド サービスを許可または拒否することができます。

Windows Server 2003 で導入された制約付き委任の詳細については、「 [Microsoft Windows Server 2003: Kerberos のプロトコル遷移と制約付き委任](https://technet.microsoft.com/library/cc739587(v=ws.10))」を参照してください。

Windows Server 2012 R2 および Windows Server 2012 の Kerberos プロトコルの実装には、制約付き委任専用の拡張機能が含まれています。  Service for User to Proxy (S4U2Proxy) は、サービスがユーザー用の Kerberos サービス チケットを使用して、キー配布センター (KDC) からバックエンド サービスへのサービス チケットを取得できるようにします。 これらの拡張機能を使用すると、別のドメインにあるバックエンドサービスのアカウントで制約付き委任を構成できます。 これらの拡張機能の詳細につい[ては、\]「 \[MS SFU:Kerberos プロトコル拡張機能:MSDN ライブラリのユーザーと制約付き委任](https://msdn.microsoft.com/library/cc246071(PROT.13).aspx)プロトコルの仕様のサービス。

**実用的なアプリケーション**

制約付き委任を使用すると、サービス管理者は、アプリケーションサービスがユーザーの代理として動作できる範囲を制限することで、アプリケーションの信頼境界を指定して適用することができます。 サービス管理者は、どのフロントエンド サービス アカウントがそれぞれのバックエンド サービスに委任できるのかを構成できます。

Windows Server 2012 R2 および Windows Server 2012 のドメイン間で制約付き委任をサポートすることで、Microsoft Internet Security and セラレーション (ISA) Server、Microsoft Forefront Threat Management Gateway、Microsoft Exchange などのフロントエンドサービスがサポートされます。Outlook Web アクセス (OWA)、および Microsoft SharePoint Server は、他のドメインのサーバーに対する認証に制約付き委任を使用するように構成できます。 これにより、既存の Kerberos インフラストラクチャを使用して、ドメインをまたがるサービス ソリューションがサポートされます。 Kerberos の制約付き委任は、ドメイン管理者またはサービス管理者が管理できます。

## <a name="resource-based-constrained-delegation-across-domains"></a>リソースに基づくドメイン間の制約付き委任

フロントエンド サービスとリソース サービスが同じドメイン内にない場合に、Kerberos の制約付き委任を使用して制約付き委任を設定できます。 サービス管理者は、リソース サービスのアカウント オブジェクト上でユーザーを偽装できるフロントエンド サービスのドメイン アカウントを指定することによって、新しい委任を構成することができます。

**この変更の利点**

ドメインをまたがる制約付き委任をサポートすることで、別のドメイン内のサーバーに対する認証に、制約のない委任を使用するのではなく、制約付き委任を使用するようにサービスを構成できます。 これにより、あらゆるサービスに対して委任するようにフロントエンド サービスを信頼する必要がなくなり、既存の Kerberos インフラストラクチャを使用して、ドメインをまたがるサービス ソリューション向けの認証がサポートされます。

これにより、ドメイン管理者からリソース所有者への委任された id のソースをサーバーが信頼する必要があるかどうかも決定されます。

**動作の相違点**

基盤となるプロトコルに対する変更により、ドメインをまたがる制約付き委任が可能になります。 Windows Server 2012 R2 および Windows Server 2012 の Kerberos プロトコルの実装には、User to Proxy (S4U2Proxy) プロトコル用のサービスの拡張機能が含まれています。 これは、Kerberos プロトコルに対する一連の拡張であり、サービスがユーザー用の Kerberos サービス チケットを使用して、キー配布センター (KDC) からバックエンド サービスへのサービス チケットを取得できるようにします。

これらの拡張機能の実装につい[ては、\]「 \[MS SFU:Kerberos プロトコル拡張機能:MSDN でのユーザーおよび制約付き委任](https://msdn.microsoft.com/library/cc246071(PROT.10).aspx)プロトコルの仕様のサービス。

Service for User (S4U) 拡張機能と比較した、転送されたチケット保証チケット (TGT) を使用した Kerberos 委任の基本的なメッセージシーケンスの詳細については、「 [1.3.3 Protocol の概要](https://msdn.microsoft.com/library/cc246080(v=prot.10).aspx)」を参照してください。Kerberos プロトコル拡張機能:ユーザーおよび制約付き委任プロトコルの仕様のサービス。

**リソースベースの制約付き委任のセキュリティへの影響**

リソースベースの制約付き委任では、アクセスされるリソースを所有する管理者に委任を制御します。 これは、委任のために信頼されているサービスではなく、リソースサービスの属性に依存します。 その結果、リソースベースの制約付き委任では、以前にプロトコル遷移を制御していた、信頼できる認証前のビットを使用できません。 KDC は、ビットが設定されているかのように、リソースベースの制約付き委任を実行するときに常にプロトコル遷移を許可します。

KDC ではプロトコルの遷移が制限されないため、このコントロールをリソース管理者に提供するために、2つの既知の Sid が新しく導入されました。  これらの Sid は、プロトコル遷移が発生したかどうかを識別し、標準のアクセス制御リストと共に使用して、必要に応じてアクセスを許可または制限することができます。

|SID|説明|
|-------|--------|
|AUTHENTICATION_AUTHORITY_ASSERTED_IDENTITY<br />S-1-18-1|クライアントの資格情報の所有証明に基づく認証機関によってクライアントの id がアサートされることを示す SID。|
|SERVICE_ASSERTED_IDENTITY<br />S-1-18-2|クライアントの id がサービスによってアサートされることを示す SID。|

バックエンドサービスでは、標準の ACL 式を使用して、ユーザーの認証方法を決定できます。

**リソースベースの制約付き委任を構成するにはどうすればよいですか。**

ユーザーの代理でフロントエンド サービス アクセスを許可するようにリソース サービスを構成するには、Windows PowerShell コマンドレットを使用します。

-   プリンシパルの一覧を取得するには、 **PrincipalsAllowedToDelegateToAccount**パラメーターを指定して、 **get Adcomputer**、 **get Adserviceaccount**、および**get adcomputer**コマンドレットを使用します。

-   リソースサービスを構成するには、**新しい**-adcomputer、 **New Adserviceaccount**、 **New ADComputer**、 **Set adcomputer**、Set **adserviceaccount**、および**set adcomputer**コマンドレットを使用します **。PrincipalsAllowedToDelegateToAccount**パラメーター。

## <a name="BKMK_SOFT"></a>ソフトウェア要件
リソースベースの制約付き委任は、Windows Server 2012 R2 および Windows Server 2012 を実行しているドメインコントローラーでのみ構成できますが、混在モードのフォレスト内で適用できます。

次の修正プログラムは、Windows Server より前のオペレーティングシステムを実行しているフロントエンドドメインとバックエンドドメイン間の参照パスで、ユーザーアカウントドメイン内の Windows Server 2012 を実行しているすべてのドメインコントローラーに適用する必要があります。Windows Server 2008 R2 ベースのドメインコントローラー (https://support.microsoft.com/en-gb/help/2665790/resource-based-constrained-delegation-kdc-err-policy-failure-in-enviro) ) を持つ環境では、リソースベースの制約付き委任 KDC_ERR_POLICY エラーが発生します。
