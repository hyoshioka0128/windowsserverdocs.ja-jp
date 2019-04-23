---
title: Group Managed Service Accounts Overview
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
ms.openlocfilehash: 24e3e3c15544de2f3bed4a7ef177b659e8095385
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836973"
---
# <a name="group-managed-service-accounts-overview"></a>Group Managed Service Accounts Overview

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

このトピックで、IT プロフェッショナルには、実際の適用を記述することでのグループ管理サービス アカウントが導入されていますは、Microsoft の実装、およびハードウェアとソフトウェアの要件に変更します。


## <a name="BKMK_OVER"></a>機能の説明
スタンドアロンの管理されたサービス アカウント (sMSA) は、パスワードの自動管理、簡素化されたサービス プリンシパル名 (SPN) の管理、および管理を他の管理者に委任する機能を提供する管理対象ドメイン アカウントです。 この種類の管理されたサービス アカウント (MSA) は、Windows Server 2008 R2 および Windows 7 で導入されました。

グループ管理サービス アカウント (gMSA) は、ドメイン内で同じ機能を提供しますが、複数サーバー上でその機能を拡張しても。 ソリューションのネットワーク負荷分散などのサーバー ファームでホストされているサービスに接続するときに相互認証をサポートする認証プロトコルでは、サービスのすべてのインスタンスが同じプリンシパルを使用することが必要です。 GMSA を使用すると、サービス プリンシパルとして、Windows オペレーティング システムは、管理者パスワードを管理するのではなく、アカウントのパスワードを管理します。

Microsoft キー配布サービス\(kdssvc.dll\)最新のキーまたは Active Directory アカウントのキー識別子と特定のキーを安全に取得するためのメカニズムを提供します。 キー配布サービスは、アカウントのキーの作成に使用されるシークレットを共有します。 これらのキーは定期的に変更されます。 GMSA ドメイン コント ローラーは gMSA の他の属性だけでなく、キー配布サービスが提供されたキーのパスワードを計算します。  メンバー ホストは、ドメイン コント ローラーに連絡して、現在および以前のパスワード値を取得できます。

## <a name="BKMK_APP"></a>実際の適用
Gmsa は、ネットワーク ロード バランサーの背後のシステムまたはサーバー ファームで実行中のサービスの単一の id ソリューションを提供します。 GMSA のソリューションを用意すると、新しい gMSA をプリンシパルのサービスを構成してパスワード管理は、Windows によって処理されます。

GMSA を使用して、サービスまたはサービス管理者必要はありません、サービス インスタンス間のパスワード同期を管理します。 GMSA は、長期間、およびサービスのすべてのインスタンス メンバー ホストの管理をオフラインで保持されているホストをサポートします。 つまり、既存のクライアント コンピューターが接続先のサービス インスタンスを把握しなくても認証できる単一 ID がサポートされたサーバー ファームを展開できます。

フェールオーバー クラスターでは、gMSA をサポートしていません。 ただし、クラスター サービスの上位で実行されるサービスは、それが Windows サービス、アプリケーション プール、またはスケジュールされたタスクである場合、あるいは gMSA/sMSA をネイティブにサポートしている場合、gMSA または sMSA を使用できます。

## <a name="BKMK_SOFT"></a>ソフトウェアの要件

64\-Gmsa の管理に使用される Windows PowerShell コマンドを実行するビットのアーキテクチャが必要です。

管理されたサービス アカウントは、Kerberos でサポートされる暗号化の種類によって決まります。Kerberos を使用するサーバーに対してクライアント コンピューターが認証されると、DC とサーバーの両方でサポートされる暗号化で保護される Kerberos サービスが DC で作成されます。 DC は、アカウントの msDS\-SupportedEncryptionTypes 属性を決定する、サーバーの暗号化をサポートし、クライアント コンピューターはより強力な暗号化の種類をサポートしていない属性がない場合は、想定しています。 ホストが RC4 をサポートしないように構成する場合の認証は失敗常にします。 このため、AES は常に MSA 用に明示的に構成する必要があります。

> [!NOTE]
> Windows Server 2008 R2 以降、既定では、DES が無効になっています。 サポートされる暗号化の種類の詳細については、「 [Kerberos 認証の変更点](https://technet.microsoft.com/library/dd560670(WS.10).aspx)」を参照してください。

Gmsa では、Windows Server 2012 より前の Windows オペレーティング システムに適用できません。

## <a name="server-manager-information"></a>サーバー マネージャー情報
MSA およびサーバー マネージャーまたはインストールを使用して gMSA を実装するために必要な構成手順がない\-WindowsFeature コマンドレット。

## <a name="BKMK_LINKS"></a>参照してください。
次の表に、管理されたサービス アカウントとグループの管理されたサービス アカウントに関連する追加リソースへのリンクを掲載します。

|コンテンツの種類|参考資料|
|--------|-------|
|**製品評価**|[管理されたサービス アカウントの新機能については](what-s-new-for-managed-service-accounts.md)<br /><br />[管理されたサービス アカウントの Windows 7 および Windows Server 2008 R2 のドキュメント](https://technet.microsoft.com/library/ff641731(v=ws.10).aspx)<br /><br />[サービス アカウント ステップ\-によって\-ステップ ガイド](https://technet.microsoft.com/library/dd548356(v=ws.10).aspx)|
|**計画**|現在は入手不能|
|**展開**|現在は入手不能|
|**運用**|[Active Directory のサービス アカウントの管理](https://technet.microsoft.com/library/dd378925(v=ws.10).aspx)|
|**トラブルシューティング**|現在は入手不能|
|**評価版**|[管理されたサービス アカウント グループの概要](getting-started-with-group-managed-service-accounts.md)|
|**ツールと設定**|[Active Directory Domain Services のサービス アカウントの管理](https://technet.microsoft.com/library/dd378925(v=WS.10).aspx)|
|**コミュニティ リソース**|[管理されたサービス アカウント。理解、実装、ベスト プラクティス、およびトラブルシューティング](http://blogs.technet.com/b/askds/archive/2009/09/10/managed-service-accounts-understanding-implementing-best-practices-and-troubleshooting.aspx)|
|**関連テクノロジ**|[Active Directory Domain Services の概要](active-directory-domain-services-overview.md)|


