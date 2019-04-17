---
title: グループの管理されたサービス アカウントの概要
description: Windows Server のセキュリティ
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-gmsa
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cef0693c-f861-48a7-a1c0-8d1bc06143ce
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 4912ae273e603b4a3362c4984da710f780c3e8b3
ms.sourcegitcommit: f26d2668f57624a3865ca4ffd36a698eea7b503e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2018
---
# <a name="group-managed-service-accounts-overview"></a>グループの管理されたサービス アカウントの概要

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックの「IT 担当者向けの実際の適用を記述することグループの管理されたサービス アカウントが導入されています変更では、Microsoft 実装およびハードウェアとソフトウェアの要件。


## <a name="BKMK_OVER"></a>機能の説明
スタンドアロンの管理されたサービス アカウント、Windows Server 2008 R2 および Windows 7 で導入されたは、パスワードの自動管理と他の管理者への管理の委任を含む、簡素化された SPN の管理を提供する管理されたドメイン アカウントです。

グループ管理されたサービス アカウントはドメイン内で同じ機能を提供するが、その機能を複数のサーバーに拡張することも。 ネットワーク負荷分散などのサーバー ファームでホストされているサービスに接続するときに相互認証をサポートする認証プロトコルは、サービスのすべてのインスタンスが同じプリンシパルを使用している必要があります。 グループの管理されたサービス アカウントをサービス プリンシパルとして使用する場合、Windows オペレーティング システムは、パスワードを管理する管理者ではなく、アカウントのパスワードを管理します。

Microsoft キー配布サービス \(kdssvc.dll\) では、最新のキーまたは Active Directory アカウントのキー識別子を持つ特定のキーを安全に取得するためのメカニズムを提供します。 キー配布サービスは、キー、アカウントの作成に使用されるシークレットを共有します。 これらのキーは定期的に変更します。 グループの管理されたサービス アカウントのドメイン コント ローラーは、グループの管理されたサービス アカウントの他の属性をさらに、キー配布サービスから提供されているキーのパスワードを計算します。  メンバー ホストは、ドメイン コント ローラーに接続して、現在または以前のパスワード値を取得できます。

## <a name="BKMK_APP"></a>実際の適用
グループ管理サービス アカウントは、サーバー ファームの場合、またはネットワーク負荷分散の背後のシステムで実行されているサービスの単一の id ソリューションを提供します。 グループの MSA ソリューションを提供して新しいグループの MSA プリンシパルのサービスを構成して、パスワード管理が Windows によって行われます。

グループを使用して、サービス インスタンス間のパスワード同期を管理する管理されたサービス アカウント、サービス自体もサービス管理者は必要ありません。 グループ管理されたサービス アカウントには、長期間、およびサービスのすべてのインスタンスのメンバー ホストの管理をオフラインに保持されるホストがサポートしています。 つまり、既存のクライアント コンピューターが、接続しているサービスのインスタンスを把握しなくても認証できる単一の id をサポートしているサーバー ファームを展開することができます。

フェールオーバー クラスターは、Gmsa をサポートしていません。 ただし、クラスタ サービス上で実行されるサービスが Windows サービス、アプリケーション プール、スケジュールされたタスクや gMSA または sMSA をネイティブでサポート、gMSA または sMSA を使用できます。

## <a name="BKMK_SOFT"></a>ソフトウェアの要件

グループ管理サービス アカウントの管理に使用される Windows PowerShell コマンドを実行するには、64 ビット アーキテクチャが必要です。

管理されたサービス アカウントは、Kerberos がサポートされている暗号化の種類によって異なります。クライアント コンピューターがドメイン コント ローラーを作成する Kerberos を使用してサーバーを認証する際に Kerberos サービス チケットは DC とサーバーの両方のサポートを暗号で保護します。 DC では、アカウントの msDS\ SupportedEncryptionTypes 属性を使用して、対象の決定、サーバーの暗号化をサポートし、クライアント コンピューターはより強力な暗号化の種類をサポートしていません属性がない場合は、想定しています。 ホストが RC4 をサポートしないように構成されている場合、認証は常に失敗します。 このため、AES 常に明示的に向けに構成される Msa します。

> [!NOTE]
> Windows Server 2008 R2 以降、DES が既定で無効にします。 サポートされている暗号化の種類の詳細については、次を参照してください。 [Kerberos 認証の変更点](https://technet.microsoft.com/library/dd560670(WS.10).aspx)します。

グループ管理サービス アカウントでは、Windows Server 2012 より前の Windows オペレーティング システムに適用されません。

## <a name="server-manager-information"></a>サーバー マネージャー情報
MSA およびグループのサーバー マネージャーまたは Install\ WindowsFeature コマンドレットを使用して MSA を実装するために必要な構成手順はありません。

## <a name="BKMK_LINKS"></a>参照してください。
次の表は、管理されたサービス アカウントとグループ管理サービス アカウントに関連するその他のリソースへのリンクを提供します。

|コンテンツの種類|参照|
|--------|-------|
|**製品評価**|[管理されたサービス アカウント向けの新機能](what-s-new-for-managed-service-accounts.md)<br /><br />[管理されたサービス アカウントの Windows 7 および Windows Server 2008 R2 のドキュメント](https://technet.microsoft.com/library/ff641731(v=ws.10).aspx)<br /><br />[サービス アカウント Step\ の単位ステップ ガイド](https://technet.microsoft.com/library/dd548356(v=ws.10).aspx)|
|**計画**|まだ利用できません。|
|**展開**|まだ利用できません。|
|**操作**|[Active Directory 内のサービス アカウントの管理](https://technet.microsoft.com/library/dd378925(v=ws.10).aspx)|
|**トラブルシューティング**|まだ利用できません。|
|**評価版**|[管理されたサービス アカウントをグループの概要](getting-started-with-group-managed-service-accounts.md)|
|**ツールと設定**|[Active Directory ドメイン サービスでサービス アカウントの管理](https://technet.microsoft.com/library/dd378925(v=WS.10).aspx)|
|**コミュニティ リソース**|[管理されたサービス アカウント: 理解、実装、ベスト プラクティス、およびトラブルシューティング](http://blogs.technet.com/b/askds/archive/2009/09/10/managed-service-accounts-understanding-implementing-best-practices-and-troubleshooting.aspx)|
|**関連するテクノロジ**|[Active Directory ドメイン サービスの概要](active-directory-domain-services-overview.md)|


