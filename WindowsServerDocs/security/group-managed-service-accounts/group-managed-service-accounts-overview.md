---
title: Group Managed Service Accounts Overview
description: Windows Server のセキュリティ
ms.topic: article
ms.assetid: cef0693c-f861-48a7-a1c0-8d1bc06143ce
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 09405b940e9fd862372fe80c4a5194caa205e5ea
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87991497"
---
# <a name="group-managed-service-accounts-overview"></a>Group Managed Service Accounts Overview

>適用先:Windows Server (半期チャネル)、Windows Server 2016

IT 担当者向けのこのトピックでは、実際のアプリケーション、Microsoft の実装の変更点、およびハードウェアとソフトウェアの要件について説明することで、グループの管理されたサービスアカウントについて説明します。


## <a name="feature-description"></a><a name="BKMK_OVER"></a>機能の説明
スタンドアロンの管理されたサービスアカウント (sMSA) は、パスワードの自動管理、簡略化されたサービスプリンシパル名 (SPN) の管理、および他の管理者に管理を委任する機能を提供する、管理されたドメインアカウントです。 この種類の管理されたサービス アカウント (MSA) は、Windows Server 2008 R2 および Windows 7 で導入されました。

グループの管理されたサービスアカウント (gMSA) は、ドメイン内で同じ機能を提供しますが、その機能を複数のサーバーに拡張することもできます。 ネットワーク負荷分散ソリューションなど、サーバーファームでホストされているサービスに接続する場合、相互認証をサポートする認証プロトコルでは、サービスのすべてのインスタンスが同じプリンシパルを使用する必要があります。 GMSA がサービスプリンシパルとして使用されている場合、Windows オペレーティングシステムは、管理者に依存してパスワードを管理するのではなく、アカウントのパスワードを管理します。

Microsoft キー配布サービスkdssvc.dllは、 \( \) Active Directory アカウントのキー識別子を使用して、最新のキーまたは特定のキーを安全に取得するためのメカニズムを提供します。 キー配布サービスは、アカウントのキーの作成に使用されるシークレットを共有します。 これらのキーは定期的に変更されます。 GMSA の場合、ドメインコントローラーは、gMSA の他の属性に加えて、キー配布サービスによって提供されるキーのパスワードを計算します。  メンバーホストは、ドメインコントローラーに接続することにより、現在と以前のパスワード値を取得できます。

## <a name="practical-applications"></a><a name="BKMK_APP"></a>実際の適用例
gMSAs は、サーバーファームまたはネットワーク Load Balancer の背後にあるシステムで実行されているサービスに対して単一の id ソリューションを提供します。 GMSA ソリューションを提供することで、新しい gMSA プリンシパル用にサービスを構成でき、パスワード管理が Windows によって処理されます。

GMSA、サービス、またはサービス管理者は、サービスインスタンス間のパスワード同期を管理する必要はありません。 GMSA は、長時間にわたってオフラインになっているホストと、サービスのすべてのインスタンスのメンバーホストの管理をサポートしています。 つまり、既存のクライアント コンピューターが接続先のサービス インスタンスを把握しなくても認証できる単一 ID がサポートされたサーバー ファームを展開できます。

フェールオーバー クラスターでは、gMSA をサポートしていません。 ただし、クラスター サービスの上位で実行されるサービスは、それが Windows サービス、アプリケーション プール、またはスケジュールされたタスクである場合、あるいは gMSA/sMSA をネイティブにサポートしている場合、gMSA または sMSA を使用できます。

## <a name="software-requirements"></a><a name="BKMK_SOFT"></a>ソフトウェア要件

\-GMSAs の管理に使用される Windows PowerShell コマンドを実行するには、64ビットアーキテクチャが必要です。

管理されたサービス アカウントは、Kerberos でサポートされる暗号化の種類によって決まります。Kerberos を使用するサーバーに対してクライアント コンピューターが認証されると、DC とサーバーの両方でサポートされる暗号化で保護される Kerberos サービスが DC で作成されます。 DC は、 \- サーバーがサポートする暗号化の種類を決定するために、アカウントの種類を使用します。属性がない場合は、クライアントコンピューターがより強力な暗号化の種類をサポートしていないと想定しています。 ホストが RC4 をサポートしないように構成されている場合、認証は常に失敗します。 このため、AES は常に MSA 用に明示的に構成する必要があります。

> [!NOTE]
> Windows Server 2008 R2 以降、既定では、DES が無効になっています。 サポートされる暗号化の種類の詳細については、「 [Kerberos 認証の変更点](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd560670(v=ws.10))」を参照してください。

gMSAs は、windows Server 2012 より前の Windows オペレーティングシステムには適用されません。

## <a name="server-manager-information"></a>サーバー マネージャー情報
サーバーマネージャーまたは Install Add-windowsfeature コマンドレットを使用して、MSA と gMSA を実装するために必要な構成手順はありません \- 。

## <a name="see-also"></a><a name="BKMK_LINKS"></a>関連項目
次の表に、管理されたサービス アカウントとグループの管理されたサービス アカウントに関連する追加リソースへのリンクを掲載します。

|コンテンツ タイプ|参考資料|
|--------|-------|
|**製品評価**|[What's New for Managed Service Accounts](what-s-new-for-managed-service-accounts.md)<p>[Windows 7 および Windows Server 2008 R2 向けの管理されたサービス アカウントのドキュメント](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff641731(v=ws.10))<p>[サービスアカウントのステップ \- バイ \- ステップガイド](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd548356(v=ws.10))|
|**計画**|まだ使用できません|
|**デプロイ**|まだ使用できません|
|**操作**|[Active Directory における管理されたサービス アカウントに関するページ](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd378925(v=ws.10))|
|**トラブルシューティング**|まだ使用できません|
|**評価**|[グループの管理されたサービスアカウントを使用したはじめに](getting-started-with-group-managed-service-accounts.md)|
|**ツールと設定**|[Active Directory Domain Services における管理されたサービス アカウントに関するページ](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd378925(v=ws.10))|
|**コミュニティ リソース**|[Managed Service Accounts:Understanding, Implementing, Best Practices, and Troubleshooting (管理されたサービス アカウント: 理解、実装、ベスト プラクティス、およびトラブルシューティング)](/archive/blogs/askds/managed-service-accounts-understanding-implementing-best-practices-and-troubleshooting)|
|**関連テクノロジ**|[Active Directory Domain Services の概要](active-directory-domain-services-overview.md)|