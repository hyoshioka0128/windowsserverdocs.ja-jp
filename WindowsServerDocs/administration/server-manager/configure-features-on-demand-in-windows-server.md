---
title: Configure Features on Demand in Windows Server
description: サーバー マネージャー
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-server-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e663bbea-d025-41fa-b16c-c2bff00a88e8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f834ca2e4c4acd045ccaeb4f46142dcc0e86f674
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383267"
---
# <a name="configure-features-on-demand-in-windows-server"></a>Configure Features on Demand in Windows Server

>適用先:Windows Server 2016

このトピックでは、Uninstall-WindowsFeature コマンドレットを使用してオンデマンド機能の構成で機能ファイルを削除する方法について説明します。

オンデマンド機能は、Windows 8 および Windows Server 2012 で導入された機能です。この機能を使用すると、ディスク領域を節約するために役割や機能のファイル (機能の*ペイロード*とも呼ばれます) をオペレーティングシステムから削除し、の役割と機能をインストールすることができます。ローカルコンピューターからではなく、リモートの場所またはインストールメディア。 機能ファイルは、実行中の物理コンピューターまたは仮想コンピューターから削除できます。 また、Windows イメージ (WIM) ファイルまたはオフラインの仮想ハード ディスク (VHD) で機能ファイルを追加または削除して、オンデマンド機能の構成の再現可能なコピーを作成することもできます。

オンデマンド機能の構成では、コンピューターで機能ファイルを使用できない場合、インストールでこれらの機能ファイルが必要な場合、Windows Server 2012 R2 または Windows Server 2012 をサイドバイサイド機能ストア (共有フォルダー) から取得するように指示することができます。これには、機能ファイルが格納され、ネットワーク上のコンピューターで使用できるようになります)、Windows Update、またはインストールメディアから取得できます。 オンデマンド機能の既定の動作では、対象サーバーで機能ファイルを利用できない場合、次のタスクを表示されている順序で実行して見つからない機能ファイルを検索します。

1.  役割と機能の追加ウィザードまたは DISM インストールコマンドのユーザーによって指定された場所を検索しています

2.  グループポリシー設定の構成を評価するコンピューターの構成 **\ 管理用テンプレート \ オプションコンポーネントのインストールおよびコンポーネントの修復の設定を指定する**

3.  Windows Update を検索する

オンデマンド機能の既定の動作は、次のいずれかの方法で変更できます。

-   `Install-WindowsFeature` コマンドレットに `Source` パラメーターを追加して代替ソース パスを指定する

-   役割と機能の追加ウィザードを使用して機能をインストールするときに **[インストールオプションの確認]** ページで代替ソースパスを指定する

-   グループ ポリシー設定 **"オプション コンポーネントのインストールおよびコンポーネントの修復のための設定を指定する"** を構成する

このトピックは次のセクションで構成されます。

-   [機能ファイルまたはサイドバイサイドストアを作成する](#BKMK_store)

-   [機能ファイルを削除する方法](#BKMK_methods)

-   [Uninstall-Add-windowsfeature を使用して機能ファイルを削除する](#BKMK_remove)

## <a name="BKMK_store"></a>機能ファイルまたはサイドバイサイドストアを作成する
このセクションでは、Windows Server 2012 R2 または Windows Server 2012 を実行しているサーバーに役割、役割サービス、および機能をインストールするために必要なファイルを格納する、リモート機能ファイル共有フォルダー (サイドバイサイドストアとも呼ばれます) を設定する方法について説明します。 機能ストアをセットアップした後、これらのオペレーティングシステムを実行しているサーバーに役割、役割サービス、および機能をインストールし、機能ストアをインストールソースファイルの場所として指定できます。

#### <a name="to-create-a-feature-file-store"></a>機能ファイル ストアを作成するには

1.  ネットワーク上のサーバーに共有フォルダーを作成します たとえば、 *\\ \ network\share\sxs*のようになります。

2.  機能ストアに対する適切なアクセス許可が割り当てられていることを確認します。 ソースパスまたはファイル共有では、 **Everyone**グループ (セキュリティ上の理由から推奨されません)、またはインストールを計画しているサーバーのコンピューターアカウント (*ドメイン*\\*SERverNAME*$) のいずれかに**読み取り**アクセス許可を付与する必要があります。この機能ストアを使用した機能ユーザーアカウントへのアクセスを許可するだけでは不十分です。

    ファイル共有およびアクセス許可の設定にアクセスするには、Windows デスクトップで次のどちらかを実行します。

    -   共有フォルダーを右クリックして **[プロパティ]** をクリックし、 **[セキュリティ]** タブで、許可されるユーザーとそのアクセス権を変更します。

    -   共有フォルダーを右クリックして **[共有]** をポイントし、 **[特定のユーザー]** をクリックします。

    > [!NOTE]
    > 外部のファイル共有に対する**読み取り**アクセス許可がワークグループ サーバーのコンピューター アカウントに割り当てられている場合でも、ワークグループ内のサーバーからは、外部の共有にアクセスすることはできません。 ワークグループ サーバーで使用できる代替ソースは、インストール メディア、Windows Update、およびローカルのワークグループ サーバーに格納されている VHD ファイルと WIM ファイルです。

3.  Windows Server のインストール メディアから手順 1. で作成した共有フォルダーに **Sources\SxS** フォルダーをコピーします。

## <a name="BKMK_methods"></a>機能ファイルを削除する方法
オンデマンド機能の構成では、2 種類の方法で Windows Server から機能ファイルを削除できます。

-   @No__t-1 コマンドレットの `remove` パラメーターを使用すると、Windows Server 2012 R2 または Windows Server 2012 を実行しているサーバーまたはオフラインの仮想ハードディスク (VHD) から機能ファイルを削除できます。 @No__t-0 パラメーターの有効な値は、ロール、ロールサービス、および機能の名前です。

-   展開イメージのサービスと管理 (DISM) コマンドを使用すると、不要な機能ファイルや他のリモート ソースから取得できる機能ファイルを省くことでディスク領域を節約できるカスタムの WIM ファイルを作成できます。 DISM を使用したカスタム イメージの準備の詳細については、「 [Windows の機能を有効または無効にする方法](https://technet.microsoft.com/library/hh824822.aspx)」を参照してください。

## <a name="BKMK_remove"></a>Uninstall-Add-windowsfeature を使用して機能ファイルを削除する
Windows Server 2012 R2 または Windows Server 2012 を実行しているサーバーおよびオフライン Vhd から役割、役割サービス、および機能をアンインストールしたり、機能ファイルを削除したりするには、Uninstall コマンドレットを使用します。 必要に応じて、同じコマンドで同じ役割、役割サービス、および機能をアンインストールおよび削除することができます。

> [!IMPORTANT]
> 役割、役割サービス、または機能、削除するファイルに依存する役割、役割サービス、および機能の機能ファイルも削除すると、削除されます。 役割サービスやサブ機能の機能ファイルを削除する場合は、親の役割または機能の役割サービスやサブ機能がほかにインストールされていなければ、親の役割または機能に対するファイルが削除されます。 `Uninstall-WindowsFeature -remove` コマンドで削除されるすべての機能ファイルを表示するには、コマンドに `whatif` パラメーターを追加して実行します。これにより、機能ファイルを実際に削除せずに結果を確認することができます。

#### <a name="to-remove-role-and-feature-files-by-using-uninstall-windowsfeature"></a>Uninstall-WindowsFeature を使用して役割と機能のファイルを削除するには

1.  次のいずれかを実行して、管理者特権を使って Windows PowerShell セッションを開きます。

    > [!NOTE]
    > リモートサーバーから役割と機能をアンインストールする場合は、管理者特権で Windows PowerShell を実行する必要はありません。

    -   Windows デスクトップで、タスク バーの **[Windows PowerShell]** を右クリックし、 **[管理者として実行]** をクリックします。

    -   Windows の**スタート**画面で、windows PowerShell タイルを右クリックし、アプリバーの **管理者として実行** をクリックします。

    -   Server Core インストールオプションを実行しているサーバーで、コマンドプロンプトに「 **PowerShell** 」と入力し、 **enter キーを**押します。

2.  次のように入力して **Enter**キーを押します。

    ```
    Uninstall-WindowsFeature -Name <feature_name> -computerName <computer_name> -remove
    ```

    **例:** リモート デスクトップ サービスの役割サービスのうち、インストールされている残りのサービスがリモート デスクトップ ライセンスだけであるとします。 この場合、次のコマンドを実行すると、リモート デスクトップ ライセンスがアンインストールされ、指定したサーバー ( *contoso_1*) からリモート デスクトップ サービスの役割全体の機能ファイルが削除されます。

    ```
    Uninstall-WindowsFeature -Name rdS-Licensing -computerName contoso_1 -remove
    ```

    **例:** 次の例では、active directory ドメインサービスとグループポリシー管理をオフライン VHD から削除します。 最初に役割と機能がアンインストールされ、さらにそれらの機能ファイルがオフライン VHD ( *Contoso.vhd*) から完全に削除されます。

    > [!NOTE]
    > Windows 8.1 または Windows 8 を実行しているコンピューターからコマンドレットを実行している場合は、`computerName` パラメーターを追加する必要があります。
    > 
    > ネットワーク共有から VHD ファイルの名前を入力する場合、その共有は、VHD をマウントするために選択したサーバーのコンピューターアカウントに**読み取り**と**書き込み**のアクセス許可を付与する必要があります。 ユーザー専用のアカウントにアクセス許可を与えるだけでは不十分です。 ネットワーク共有では、**読み取り**アクセス許可と**書き込み**アクセス許可を **Everyone** グループに付与し、VHD へのアクセスを許可することができますが、セキュリティ上の理由からこの方法はお勧めしません。

    ```
    Uninstall-WindowsFeature -Name AD-Domain-Services,GPMC -VHD C:\WS2012VHDs\Contoso.vhd -computerName ContosoDC1
    ```

## <a name="see-also"></a>関連項目
[役割、役割サービス、または機能をインストールまたはアンインストール](install-or-uninstall-roles-role-services-or-features.md)
[Windows Server インストールオプション](https://technet.microsoft.com/library/hh831786.aspx)
[windows の機能を有効または無効にする方法](https://technet.microsoft.com/library/hh824822.aspx)
[展開イメージのサービスと管理 (DISM) の概要](https://technet.microsoft.com/library/hh825236.aspx)


