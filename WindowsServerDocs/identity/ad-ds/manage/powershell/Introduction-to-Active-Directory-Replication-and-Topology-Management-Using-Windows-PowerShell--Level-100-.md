---
ms.assetid: c54b544f-cc32-4837-bb2d-a8656b22f3de
title: "Active Directory レプリケーションおよびトポロジ管理の Windows PowerShell (レベル 100) の使用の概要"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 006179bb3220f7bccfc7510e1b8ef69678321074
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="introduction-to-active-directory-replication-and-topology-management-using-windows-powershell-level-100"></a>Active Directory レプリケーションおよびトポロジ管理の Windows PowerShell (レベル 100) の使用の概要

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Active Directory 用 Windows PowerShell には、レプリケーション、サイト、ドメインとフォレスト、ドメイン コントローラー、およびパーティションを管理する機能が含まれています。 ユーザーは、Active Directory サイトとサービスなどの書面による事前の管理ツールのスナップイン、repadmin.exe なりますと同様の機能は、Windows PowerShell 用 Active Directory のコンテキスト内で利用できるようになりました。 さらに、コマンドレットは、既存用 Windows PowerShell の Active Directory コマンドレット、したがって合理化されたエクスペリエンスを作成して、簡単に自動化スクリプトを作成することも可能に対応。

> [!NOTE]
> Active Directory レプリケーションおよびトポロジ コマンドレット用の Windows PowerShell は、次の環境で使用できます。
> 
> -    Windows Server 2012 ドメイン コントローラー
> -    Windows Server 2012 の AD DS および AD LDS 用リモート サーバー管理ツールをインストールします。
> -   Windows&reg; 8 AD DS および AD LDS がインストールされているため、リモート サーバー管理ツールにします。

## <a name="installing-the-active-directory-module-for-windows-powershell"></a>Windows PowerShell 用 Active Directory モジュールをインストールします。
Windows Server 2012 を実行しているサーバーに AD DS サーバー役割がインストールされているときに、既定では、Active Directory 用 Windows PowerShell モジュールがインストールされます。 追加の手順は、サーバーの役割を追加する以外は必要ありません。 リモート サーバー管理ツールをインストールすることによって、Windows Server 2012 を実行しているサーバー上の Active Directory モジュールをインストールすることもでき、ダウンロードしてインストールして Windows 8 を実行するコンピューターで Active Directory モジュールをインストールすることができます、[リモート サーバー管理ツール (RSAT)](https://www.microsoft.com/download/details.aspx?id=28972)します。 参照してください[指示](https://www.microsoft.com/download/details.aspx?id=28972)手順についてはインストールします。

## <a name="scenarios-for-testing-windows-powershell-for-active-directory-replication-and-topology-management-cmdlets"></a>Active Directory レプリケーションおよびトポロジ管理コマンドレットを Windows PowerShell をテストするためのシナリオ
次のシナリオは、新しい管理コマンドレットに慣れるために管理者向けに設計されました。

-   すべてのドメイン コントローラーとその対応するサイトの一覧を取得します。

-   レプリケーション トポロジを管理します。

-   レプリケーション ステータスの表示と情報

## <a name="lab-requirements"></a>ラボ要件

-   次の 2 つの Windows Server 2012 ドメイン コントローラー: **DC1**と**DC2** contoso.com ドメインの一部であるし、企業内のサイトにそのドメインに存在します。

## <a name="view-domain-controllers-and-their-sites"></a>ドメイン コントローラーとそのサイトを表示します。
この手順では、既存のドメイン コントローラーとドメインのレプリケーション トポロジを表示するのに、Active Directory 用 Windows PowerShell モジュールを使用します。

次の手順の手順を完了するには、Domain Admins グループのメンバーであるか、同等のアクセス許可がある必要があります。

#### <a name="to-view-all-active-directory-sites"></a>すべての Active Directory サイトを表示するには

1.  [ **DC1**、] をクリックして**Windows PowerShell**タスク バーにします。

2.  次のコマンドを入力します。

    `Get-ADReplicationSite -Filter *`

    これは、各サイトに関する詳細情報を返します。 `Filter`パラメーターは、各種 Active Directory PowerShell コマンドレットで返されるオブジェクトのリストを制限する使用します。 この場合は、アスタリスク (*) では、すべてのサイト オブジェクトを示します。

    > [!TIP]
    > Windows PowerShell でオートコンプリート コマンドに Tab キーを使用することができます。
    > 
    > 例: 入力`Get-ADRep`tab キーを複数回表示されるまで、対応するコマンドをスキップして`Get-ADReplicationSite`します。 オートコンプリートでも、パラメーター名になど`Filter`します。

    出力を書式設定する、`Get-ADReplicationSite`テーブルとしてコマンドを実行し、表示を制限する特定のフィールドにはその出力をパイプ処理することができます、`Format-Table`コマンド (または"`ft`"を短い)。

    `Get-ADReplicationSite -Filter * | ft Name`

    これは、短いバージョンの名前] フィールドを含む、サイト一覧を返します。

#### <a name="to-produce-a-table-of-all-domain-controllers"></a>すべてのドメイン コントローラーのテーブルを作成するには

-   次のコマンドを入力、**Windows PowerShell 用 Active Directory モジュール**プロンプト。

    `Get-ADDomainController -Filter * | ft Hostname,Site`

    このコマンドは、ドメイン コントローラー ホスト名だけでなく、サイトの関連付けを返します。

## <a name="manage-replication-topology"></a>レプリケーション トポロジを管理します。
コマンドを実行した後、前の手順で`Get-ADDomainController -Filter * | ft Hostname,Site`、**DC2**の一部として表示されている、**企業**サイト。 以下の手順では、新しいブランチ オフィス サイトを作成する**BRANCH1**は、新しいサイト リンクを作成し、サイト リンク コストとレプリケーションの頻度を設定、移動**DC2**に**BRANCH1**します。

次の手順の手順を完了するには、Domain Admins グループのメンバーであるか、同等のアクセス許可がある必要があります。

#### <a name="to-create-a-new-site"></a>新しいサイトを作成するには

-   次のコマンドを入力、**Windows PowerShell 用 Active Directory モジュール**プロンプト。

    `New-ADReplicationSite BRANCH1`

    このコマンドは、新しいブランチ オフィス サイトの branch1 を作成します。

#### <a name="to-create-a-new-site-link"></a>新しいサイト リンクを作成するには

-   次のコマンドを入力、**Windows PowerShell 用 Active Directory モジュール**プロンプト。

    `New-ADReplicationSiteLink 'CORPORATE-BRANCH1'  -SitesIncluded CORPORATE,BRANCH1 -OtherAttributes @{'options'=1}`

    このコマンドは、サイト リンクを作成**BRANCH1**され、変更通知プロセスで有効になります。

    > [!TIP]
    > など、オートコンプリートのパラメーター名にタブを使用して`-SitesIncluded`と`-OtherAttributes`を省くことを手動でします。

#### <a name="to-set-the-site-link-cost-and-replication-frequency"></a>サイト リンク コストとレプリケーションの頻度を設定するには

-   次のコマンドを入力、**Windows PowerShell 用 Active Directory モジュール**プロンプト。

    `Set-ADReplicationSiteLink CORPORATE-BRANCH1 -Cost 100 -ReplicationFrequencyInMinutes 15`

    このコマンドでは、サイト リンク コストを設定**BRANCH1**で**100**するようにサイトのレプリケーションの頻度を設定および**15 分**します。

#### <a name="to-move-a-domain-controller-to-a-different-site"></a>ドメイン コントローラーを別のサイトに移動するには

-   次のコマンドを入力、**Windows PowerShell 用 Active Directory モジュール**プロンプト。

    `Get-ADDomainController DC2 | Move-ADDirectoryServer -Site BRANCH1`

    このコマンドは、ドメイン コントローラーを移動**DC2**を**BRANCH1**サイト。

### <a name="verification"></a>検証

##### <a name="to-verify-site-creation-new-site-link-and-cost-and-replication-frequency"></a>サイトの作成、新しいサイト リンク、コストとレプリケーションの頻度を確認するには

-   をクリックして**サーバー マネージャー**、] をクリックして**ツール**] をクリックし、**Active Directory サイトとサービス**し、次のことを確認します。

    いることを確認、**BRANCH1**サイトには、すべての Windows PowerShell コマンドの正しい値が含まれています。

    確認、**corporate-branch1**サイト リンクを作成し、接続、**BRANCH1**と**企業**サイト。

    確認**DC2**のようになりましたが、**BRANCH1**サイト。 または、開くことができます、**Active Directory 用 Windows PowerShell モジュール**ことを確認するには、次のコマンドを入力し、**DC2**のようになりましたが、**BRANCH1**サイト:`Get-ADDomainController -Filter * | ft Hostname,Site`します。

## <a name="view-replication-status-information"></a>レプリケーションの状態情報の表示
次の手順で使用する Windows PowerShell のいずれかの Active Directory レプリケーションおよび管理コマンドレット、`Get-ADReplicationUpToDatenessVectorTable DC1`、各ドメイン コントローラーによって維持される最新のベクター テーブルを使用するシンプルなレプリケーション レポートを作成します。 この最新のベクター テーブルは、フォレスト内の各ドメイン コントローラーから見た最大発信書き込み USN を追跡を維持します。

次の手順の手順を完了するには、Domain Admins グループのメンバーであるか、同等のアクセス許可がある必要があります。

#### <a name="to-view-the-up-to-dateness-vector-table-for-a-single-domain-controller"></a>1 つのドメイン コントローラーの最新のベクター テーブルを表示するには

1.  次のコマンドを入力、**Windows PowerShell 用 Active Directory モジュール**プロンプト。

    `Get-ADReplicationUpToDatenessVectorTable DC1`

    これはから見た最大 Usn のリストを示しています**DC1**フォレスト内のすべてのドメイン コントローラー。 **サーバー**値がここで、テーブルを保守しているサーバーを指す**DC1**します。 **パートナー**値の変更が加えられたレプリケーション パートナー (直接または間接) を参照します。 UsnFilter 値から見た最大 USN **DC1**パートナーからです。 フォレストに新しいドメイン コントローラーを追加する場合に表示されません**DC1**までのテーブル**DC1**、新しいドメインから発信された変更を受信します。

#### <a name="to-view-the-up-to-dateness-vector-table-for-all-domain-controllers-in-a-domain"></a>ドメイン内のすべてのドメイン コントローラーの最新のベクター テーブルを表示するには

1.  Active Directory モジュールの Windows PowerShell プロンプトで、次のコマンドを入力します。

    `Get-ADReplicationUpToDatenessVectorTable * | sort Partner,Server | ft Partner,Server,UsnFilter`

    このコマンドは置き換えます**DC1**で`*`、したがってすべてのドメイン コントローラーから最新のベクター テーブルのデータを収集します。 データを並べ替える**パートナー**と**サーバー**し、表形式で表示します。

    並べ替えを行うには、特定のレプリケーション パートナーの各ドメイン コントローラーから見た最後の USN を簡単に比較することができます。 これは、レプリケーションが、環境全体で発生していることを確認する簡単です。 レプリケーションは正しく動作している場合、特定のレプリケーション パートナーに対して報告される UsnFilter 値する必要がありますとほとんど同じすべてのドメイン コントローラー間でします。

## <a name="see-also"></a>参照してください。
[Active Directory レプリケーションおよびトポロジ管理の Windows PowerShell (&) #40; を使用して高度なレベル 200 & #41 です。](Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md)


