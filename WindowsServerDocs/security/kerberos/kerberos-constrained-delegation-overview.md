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
ms.openlocfilehash: d77dd6f6f310ae71a4d9e2d52b44cc9b1bef6401
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821933"
---
# <a name="kerberos-constrained-delegation-overview"></a>Kerberos Constrained Delegation Overview

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

IT プロフェッショナル向けのこの概要トピックでは、Windows Server 2012 R2 および Windows Server 2012 での Kerberos の制約付き委任に対する新機能について説明します。

**機能の説明**

Kerberos の制約付き委任は、サービスで使用できる、より安全な形の委任を提供するために Windows Server 2003 で導入されました。 制約付き委任を構成すると、指定されたサーバーがユーザーの代理として動作できる対象のサービスが制限されます。 これには、サービスに対してドメイン アカウントを構成するためにドメイン管理者特権が必要であり、そのアカウントは 1 つのドメインに制限されます。 今日のエンタープライズ環境でフロント エンド サービスは、ドメイン内のサービスだけとの統合に制限する限りません。

ドメイン管理者がサービスを構成していた従来のオペレーティング システムでは、サービス管理者には、所有しているリソース サービスに委任されるフロントエンド サービスを把握する有効な手立てがありませんでした。 また、リソース サービスに委任できるフロントエンド サービスは攻撃ポイントになる可能性がありました。 フロントエンド サービスをホストしているサーバーが攻撃を受けたときに、それがリソース サービスに委任されるように構成されていた場合、リソース サービスも危険にさらされる可能性がありました。

Windows Server 2012 R2 および Windows Server 2012 では、サービスの制約付き委任を構成する機能をドメイン管理者からサービス管理者に変更されましたが。 これにより、バックエンド サービス管理者はフロントエンド サービスを許可または拒否することができます。

Windows Server 2003 で導入された制約付き委任の詳細については、「 [Microsoft Windows Server 2003: Kerberos のプロトコル遷移と制約付き委任](https://technet.microsoft.com/library/cc739587(v=ws.10))」を参照してください。

Kerberos プロトコルの Windows Server 2012 R2 および Windows Server 2012 の実装には、制約付き委任向けの拡張機能が含まれます。  Service for User to Proxy (S4U2Proxy) は、サービスがユーザー用の Kerberos サービス チケットを使用して、キー配布センター (KDC) からバックエンド サービスへのサービス チケットを取得できるようにします。 これらの拡張機能は、別のドメインであることができるバックエンド サービスのアカウントで設定する制約付き委任を許可します。 これらの拡張機能の詳細については、次を参照してください[ \[MS-SFU\]:。Kerberos プロトコル拡張:Service for User および制約付き委任プロトコルの仕様](https://msdn.microsoft.com/library/cc246071(PROT.13).aspx)MSDN ライブラリ。

**実際の適用**

制約付き委任が使用するサービス管理者を指定およびアプリケーション サービスがユーザーの代理として動作できる範囲を制限することで、アプリケーションの信頼境界を適用できます。 サービス管理者は、どのフロントエンド サービス アカウントがそれぞれのバックエンド サービスに委任できるのかを構成できます。

Windows Server 2012 R2 および Windows Server 2012、Microsoft Internet Security and Acceleration (ISA) Server、Microsoft Forefront Threat Management Gateway、Microsoft Exchange などのフロント エンドのサービスでのドメイン間で制約付き委任をサポートして制約付き委任を使用して、他のドメイン内のサーバーに認証するには、outlook Web Access (OWA)、および Microsoft SharePoint Server を構成できます。 これにより、既存の Kerberos インフラストラクチャを使用して、ドメインをまたがるサービス ソリューションがサポートされます。 Kerberos の制約付き委任は、ドメイン管理者またはサービス管理者が管理できます。

## <a name="resource-based-constrained-delegation-across-domains"></a>リソースに基づくドメイン間の制約付き委任

フロントエンド サービスとリソース サービスが同じドメイン内にない場合に、Kerberos の制約付き委任を使用して制約付き委任を設定できます。 サービス管理者は、リソース サービスのアカウント オブジェクト上でユーザーを偽装できるフロントエンド サービスのドメイン アカウントを指定することによって、新しい委任を構成することができます。

**この変更の利点**

ドメインをまたがる制約付き委任をサポートすることで、別のドメイン内のサーバーに対する認証に、制約のない委任を使用するのではなく、制約付き委任を使用するようにサービスを構成できます。 これにより、あらゆるサービスに対して委任するようにフロントエンド サービスを信頼する必要がなくなり、既存の Kerberos インフラストラクチャを使用して、ドメインをまたがるサービス ソリューション向けの認証がサポートされます。

これは、サーバーが、リソースの所有者に委任からドメイン管理者から委任された id のソースを信頼するかどうかの決定も移動します。

**動作の相違点**

基盤となるプロトコルに対する変更により、ドメインをまたがる制約付き委任が可能になります。 Kerberos プロトコルの Windows Server 2012 R2 および Windows Server 2012 の実装には、service for User to Proxy (S4U2Proxy) プロトコルの拡張機能が含まれます。 これは、Kerberos プロトコルに対する一連の拡張であり、サービスがユーザー用の Kerberos サービス チケットを使用して、キー配布センター (KDC) からバックエンド サービスへのサービス チケットを取得できるようにします。

これらの拡張機能の実装については、次を参照してください[ \[MS-SFU\]:。Kerberos プロトコル拡張:Service for User および制約付き委任プロトコルの仕様](https://msdn.microsoft.com/library/cc246071(PROT.10).aspx)MSDN にします。

セクションを参照して、転送されたチケット保証チケット (TGT) サービスと比較して User (S4U) 拡張機能を使用して Kerberos 委任用の基本的なメッセージ シーケンスの詳細については、 [1.3.3 プロトコルの概要](https://msdn.microsoft.com/library/cc246080(v=prot.10).aspx)で [MS-SFU]。Kerberos プロトコル拡張:Service for User および制約付き委任プロトコルの仕様。

**リソースに基づく制約付き委任のセキュリティの影響**

リソース ベースの制約付きアクセス対象のリソースを所有している管理者の手に委任の配置の制御を委任します。 これは、委任で信頼されているサービスではなく、リソース サービスの属性とは異なります。 その結果、リソースに基づく制約付き委任は、以前のプロトコル遷移を制御する信頼済みに-認証-の-委任ビットを使用できません。 ビットが設定された場合と同様、委任を制約付きリソースに基づくを実行するときに、KDC は常にプロトコル遷移を許可します。

KDC では、プロトコル遷移を制限しないため、リソース管理者にこのコントロールを提供する 2 つの新しい既知の Sid が導入されました。  これらの Sid は、プロトコル遷移が発生し、標準的なアクセス制御リストで許可または必要に応じてアクセスを制限するために使用するかどうかを特定します。

|SID|説明|
|-------|--------|
|AUTHENTICATION_AUTHORITY_ASSERTED_IDENTITY<br />S-1-18-1|クライアントの id を意味する SID は、クライアントの資格情報の所有に基づいた認証機関によってアサートされます。|
|SERVICE_ASSERTED_IDENTITY<br />S-1-18-2|クライアントの id を意味するための SID は、サービスによってアサートされます。|

バックエンド サービスでは、ユーザーが認証方法を決定するのに標準の ACL の式を使用できます。

**リソース ベースの制約付き委任を構成する方法**

ユーザーの代理でフロントエンド サービス アクセスを許可するようにリソース サービスを構成するには、Windows PowerShell コマンドレットを使用します。

-   プリンシパルの一覧を取得する、 **Get-adcomputer**、 **Get-adserviceaccount**、および**Get-aduser**では、コマンドレット、**プロパティPrincipalsAllowedToDelegateToAccount**パラメーター。

-   リソース サービスを構成するには、使用、 **New-adcomputer**、 **New-adserviceaccount**、 **New-aduser**、 **Set-adcomputer**、 **Set-adserviceaccount**、および**Set-aduser**では、コマンドレット、 **PrincipalsAllowedToDelegateToAccount**パラメーター。

## <a name="BKMK_SOFT"></a>ソフトウェアの要件
リソースに基づく制約付き委任は、Windows Server 2012 R2 および Windows Server 2012 を実行するドメイン コント ローラー上でのみ構成できますが、混在モードのフォレスト内で適用できます。

すべてのドメイン コント ローラーで実行されている Windows Server 2012 でユーザー アカウント ドメインの参照パス Windows Server よりも前のオペレーティング システムを実行している、フロント エンドとバックエンド ドメイン間には、次の修正プログラムを適用する必要があります。リソース ベースの制約付き委任 KDC_ERR_POLICY エラーが Windows Server 2008 R2 ベースのドメイン コント ローラー環境でします。
