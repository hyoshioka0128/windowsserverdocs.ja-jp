---
ms.assetid: c54b544f-cc32-4837-bb2d-a8656b22f3de
title: Introduction to Active Directory Replication and Topology Management Using Windows PowerShell (Level 100)
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 62ba9e757195861989fcd6d9eca395a47262aa7e
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87967779"
---
# <a name="introduction-to-active-directory-replication-and-topology-management-using-windows-powershell-level-100"></a>Introduction to Active Directory Replication and Topology Management Using Windows PowerShell (Level 100)

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

Active Directory 用 Windows PowerShell には、レプリケーション、サイト、ドメイン、フォレスト、ドメイン コントローラー、およびパーティションの管理機能が含まれます。 従来の管理ツール ("Active Directory サイトとサービス" スナップイン、repadmin.exe など) のユーザーにとっては、同様の機能を Active Directory 用 Windows PowerShell のコンテキスト内で利用できることになります。 加えて、これらのコマンドレットは既存の Active Directory 用 Windows PowerShell コマンドレットと互換性があるため、エクスペリエンスが合理化されると共に、ユーザーは簡単に自動化スクリプトを作成できます。

> [!NOTE]
> Active Directory 用 Windows PowerShell レプリケーションおよびトポロジ コマンドレットは、次の環境で使用できます。
>
> -    Windows Server 2012 ドメインコントローラー
> -    AD DS および AD LDS のリモートサーバー管理ツールがインストールされた Windows Server 2012。
> -   &reg;AD DS および AD LDS のリモートサーバー管理ツールがインストールされた Windows 8。

## <a name="installing-the-active-directory-module-for-windows-powershell"></a>Windows PowerShell 用 Active Directory モジュールのインストール
Windows Server 2012 を実行しているサーバーに AD DS サーバーの役割がインストールされている場合、Windows PowerShell の Active Directory モジュールは既定でインストールされます。 サーバー役割を追加する以外に、追加の手順は必要ありません。 リモートサーバー管理ツールをインストールして、Windows Server 2012 を実行しているサーバーに Active Directory モジュールをインストールすることもできます。また、[リモートサーバー管理ツール (RSAT)](https://www.microsoft.com/download/details.aspx?id=28972)をダウンロードしてインストールすることにより、windows 8 を実行しているコンピューターに Active Directory モジュールをインストールできます。 インストール手順については、「[Instructions (手順)](https://www.microsoft.com/download/details.aspx?id=28972)」を参照してください。

## <a name="scenarios-for-testing-windows-powershell-for-active-directory-replication-and-topology-management-cmdlets"></a>Active Directory 用 Windows PowerShell レプリケーションおよびトポロジ管理コマンドレットをテストするためのシナリオ
次に示すのは、管理者が新しい管理コマンドレットを理解できるように設計されたシナリオです。

-   すべてのドメイン コントローラーと対応するサイトの一覧を取得する

-   レプリケーション トポロジを管理する

-   レプリケーションの状態および情報を表示する

## <a name="lab-requirements"></a>ラボ要件

-   Contoso.com ドメインの一部であり、そのドメイン内の企業サイトに存在する2つの Windows Server 2012 ドメインコントローラー: **DC1**と**DC2** 。

## <a name="view-domain-controllers-and-their-sites"></a>ドメイン コントローラーとそのサイトの表示
この手順では、Windows PowerShell 用 Active Directory モジュールを使用して、既存のドメイン コントローラーとドメインのレプリケーション トポロジを表示します。

次の手順を実行するには、Domain Admins グループのメンバーであるか、または同等のアクセス許可を持っている必要があります。

#### <a name="to-view-all-active-directory-sites"></a>すべての Active Directory サイトを表示するには

1.  **DC1** のタスク バーで **Windows PowerShell** をクリックします。

2.  次のコマンドを入力します。

    `Get-ADReplicationSite -Filter *`

    それぞれのサイトに関する詳細な情報が返されます。 `Filter` パラメーターは、各種 Active Directory PowerShell コマンドレットで返されるオブジェクトのリストを制限するために使用します。 この場合のアスタリスク (*) は、すべてのサイト オブジェクトを表します。

    > [!TIP]
    > Tab キーを使用すると、オートコンプリート機能を使用して Windows PowerShell のコマンドを入力できます。
    >
    > 例: 「`Get-ADRep`」と入力した後、Tab キーを押すと、対応するコマンドが表示されます。ここでは、Tab キーを何度か押して `Get-ADReplicationSite` を取得します。 オートコンプリート機能は、`Filter` などのパラメーター名にも有効です。

    コマンドからの出力をテーブルとして書式設定し、特定のフィールドに表示を制限するには、パイプを使用して `Get-ADReplicationSite` 出力をコマンドに渡し `Format-Table` `ft` ます (短い場合は "")。

    `Get-ADReplicationSite -Filter * | ft Name`

    このコマンドを実行すると、Name フィールドのみが含まれる、短いバージョンのサイト リストが返されます。

#### <a name="to-produce-a-table-of-all-domain-controllers"></a>すべてのドメイン コントローラーの表を生成するには

-   **[Windows PowerShell の Active Directory モジュール]** のプロンプトで、次のコマンドを入力します。

    `Get-ADDomainController -Filter * | ft Hostname,Site`

    このコマンドを実行すると、ドメイン コントローラー ホスト名とそのサイトの関連性が返されます。

## <a name="manage-replication-topology"></a>レプリケーション トポロジを管理する
前の手順では、`Get-ADDomainController -Filter * | ft Hostname,Site` コマンドを実行した後で **DC2** が **CORPORATE** サイトの一部として表示されました。 ここでは、新しいブランチ オフィス サイトの **BRANCH1** を作成し、新しいサイト リンクを作成します。次に、サイト リンク コストとレプリケーションの頻度を設定し、**DC2** を **BRANCH1** に移動します。

次の手順を実行するには、Domain Admins グループのメンバーであるか、または同等のアクセス許可を持っている必要があります。

#### <a name="to-create-a-new-site"></a>新しいサイトを作成するには

-   **[Windows PowerShell の Active Directory モジュール]** のプロンプトで、次のコマンドを入力します。

    `New-ADReplicationSite BRANCH1`

    このコマンドにより、新しいブランチ オフィス サイトの branch1 が作成されます。

#### <a name="to-create-a-new-site-link"></a>新しいサイト リンクを作成するには

-   **[Windows PowerShell の Active Directory モジュール]** のプロンプトで、次のコマンドを入力します。

    `New-ADReplicationSiteLink 'CORPORATE-BRANCH1'  -SitesIncluded CORPORATE,BRANCH1 -OtherAttributes @{'options'=1}`

    このコマンドにより、**BRANCH1** へのサイト リンクが作成され、変更通知プロセスが有効になります。

    > [!TIP]
    > Tab キーによるオートコンプリート機能を使用してパラメーター名 ( `-SitesIncluded` 、 `-OtherAttributes` ) を入力すると、手動で入力する手間を省くことができます。

#### <a name="to-set-the-site-link-cost-and-replication-frequency"></a>サイト リンク コストとレプリケーションの頻度を設定するには

-   **[Windows PowerShell の Active Directory モジュール]** のプロンプトで、次のコマンドを入力します。

    `Set-ADReplicationSiteLink CORPORATE-BRANCH1 -Cost 100 -ReplicationFrequencyInMinutes 15`

    このコマンドは、**BRANCH1** へのサイト リンク コストを **100** に設定し、サイトのレプリケーションの頻度を **15** 分に設定します。

#### <a name="to-move-a-domain-controller-to-a-different-site"></a>ドメイン コントローラーを別のサイトに移動するには

-   **[Windows PowerShell の Active Directory モジュール]** のプロンプトで、次のコマンドを入力します。

    `Get-ADDomainController DC2 | Move-ADDirectoryServer -Site BRANCH1`

    このコマンドは、ドメイン コントローラー **DC2** を **BRANCH1** サイトに移動します。

### <a name="verification"></a>検証

##### <a name="to-verify-site-creation-new-site-link-and-cost-and-replication-frequency"></a>サイトの作成、新しいサイト リンク、コスト、およびレプリケーションの頻度を検証するには

-   **[サーバー マネージャー]** をクリックし、**[ツール]** をクリックします。次に、**[Active Directory サイトとサービス]** をクリックし、次のことを確認します。

    **BRANCH1** サイトに Windows PowerShell コマンドの正しい値がすべて含まれていることを確認します。

    **CORPORATE-BRANCH1** サイト リンクが作成され、**BRANCH1** サイトと **CORPORATE** サイトが接続されていることを確認します。

    **DC2** が **BRANCH1** サイトに属していることを確認します。 または、**[Windows PowerShell の Active Directory モジュール]** を開き、次のコマンドを入力して、**DC2** が **BRANCH1** サイトに属していることを確認できます: `Get-ADDomainController -Filter * | ft Hostname,Site`。

## <a name="view-replication-status-information"></a>レプリケーションの状態情報を表示する
ここでは、Active Directory 用 Windows PowerShell レプリケーションおよびトポロジ管理コマンドレットの `Get-ADReplicationUpToDatenessVectorTable DC1` を使用して、各ドメイン コントローラーによって保守される最新のベクター テーブルを使用した単純なレプリケーション レポートを生成します。 この最新のベクター テーブルは、フォレスト内の各ドメイン コントローラーから見た最大発信書き込み USN を追跡します。

次の手順を実行するには、Domain Admins グループのメンバーであるか、または同等のアクセス許可を持っている必要があります。

#### <a name="to-view-the-up-to-dateness-vector-table-for-a-single-domain-controller"></a>単一のドメイン コントローラーの最新のベクター テーブルを表示するには

1.  **[Windows PowerShell の Active Directory モジュール]** のプロンプトで、次のコマンドを入力します。

    `Get-ADReplicationUpToDatenessVectorTable DC1`

    このコマンドは、フォレスト内のすべてのドメイン コントローラーについて **DC1** から見た最大 USN のリストを表示します。 **Server** 値は、テーブルを保守しているサーバーを表します (この場合は **DC1**)。 **Partner** 値は、変更が加えられた (直接または間接) レプリケーション パートナーを表します。 UsnFilter 値は、Partner の **DC1** から見た最大 USN です。 新しいドメインコントローラーがフォレストに追加された場合、新しいドメインコントローラーは、新しいドメインからの変更を**dc1**が受け取るまで**dc1**のテーブルに表示されません。

#### <a name="to-view-the-up-to-dateness-vector-table-for-all-domain-controllers-in-a-domain"></a>ドメイン内のすべてのドメイン コントローラーの最新のベクター テーブルを表示するには

1.  [Windows PowerShell の Active Directory モジュール] のプロンプトで、次のコマンドを入力します。

    `Get-ADReplicationUpToDatenessVectorTable * | sort Partner,Server | ft Partner,Server,UsnFilter`

    このコマンドでは、すべてのドメイン コントローラーの最新のベクター テーブルを収集するために、前のコマンドの **DC1** が `*` に置き換えられています。 データは、**Partner** と **Server** に基づいて並べ替えられた後、表形式で表示されます。

    並べ替えを行うことで、特定のレプリケーション パートナーに関して各ドメイン コントローラーから見た最後の USN を簡単に比較できます。 これにより、環境でレプリケーションが発生しているかどうかを簡単に調べることができます。 レプリケーションが適切に動作している場合、特定のレプリケーション パートナーに対して報告される UsnFilter 値は、すべてのドメイン コントローラーで類似しています。

## <a name="see-also"></a>参照
[Windows PowerShell &#40;レベル 200&#41;を使用した高度な Active Directory レプリケーションおよびトポロジ管理](Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md)


