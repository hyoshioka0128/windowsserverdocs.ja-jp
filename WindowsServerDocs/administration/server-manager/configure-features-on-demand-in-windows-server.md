---
title: Configure Features on Demand in Windows Server
description: サーバー マネージャー
ms.topic: article
ms.assetid: e663bbea-d025-41fa-b16c-c2bff00a88e8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ffe38a896e7913d03cc8f4ad62d1e520cec6a0c2
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87991932"
---
# <a name="configure-features-on-demand-in-windows-server"></a>Configure Features on Demand in Windows Server

>適用先:Windows Server 2016

このトピックでは、Uninstall-WindowsFeature コマンドレットを使用してオンデマンド機能の構成で機能ファイルを削除する方法について説明します。

オンデマンド機能は、Windows 8 および Windows Server 2012 で導入された機能です。この機能を使用すると、ディスク領域を節約するために役割や機能のファイル (機能の*ペイロード*とも呼ばれます) をオペレーティングシステムから削除し、ローカルコンピューターからではなく、リモートの場所やインストールメディアから役割や機能をインストールできます。 機能ファイルは、実行中の物理コンピューターまたは仮想コンピューターから削除できます。 また、Windows イメージ (WIM) ファイルまたはオフラインの仮想ハード ディスク (VHD) で機能ファイルを追加または削除して、オンデマンド機能の構成の再現可能なコピーを作成することもできます。

オンデマンド機能の構成では、コンピューターで機能ファイルを使用できない場合、インストールでこれらの機能ファイルが必要な場合、Windows Server 2012 R2 または Windows Server 2012 をサイドバイサイド機能ストア (ネットワーク上のコンピューターで使用可能な機能ファイルを含む共有フォルダー) からファイルを取得するように指示することができ Windows Update、またはインストールメディアから。 オンデマンド機能の既定の動作では、ターゲット サーバーで機能ファイルを利用できない場合、次のタスクを表示されている順序で実行して見つからない機能ファイルを検索します。

1.  役割と機能の追加ウィザードまたは DISM インストールコマンドのユーザーによって指定された場所を検索しています

2.  グループポリシー設定の構成を評価するコンピューターの構成**\ 管理用テンプレート \ オプションコンポーネントのインストールおよびコンポーネントの修復の設定を指定する**

3.  Windows Update を検索する

オンデマンド機能の既定の動作は、次のいずれかの方法でオーバーライドできます。

-   `Install-WindowsFeature` コマンドレットに `Source` パラメーターを追加して代替ソース パスを指定する

-   役割と機能の追加ウィザードを使用して機能をインストールするときに [**インストールオプションの確認**] ページで代替ソースパスを指定する

-   グループ ポリシー設定 **"オプション コンポーネントのインストールおよびコンポーネントの修復のための設定を指定する"** を構成する

このトピックは、次のセクションで構成されています。

-   [機能ファイルまたはサイド バイ サイド ストアを作成する](#BKMK_store)

-   [機能ファイルを削除する方法](#BKMK_methods)

-   [Uninstall-WindowsFeature を使用して機能ファイルを削除する](#BKMK_remove)

## <a name="create-a-feature-file-or-side-by-side-store"></a><a name=BKMK_store></a>機能ファイルまたはサイド バイ サイド ストアを作成する
このセクションでは、Windows Server 2012 R2 または Windows Server 2012 を実行しているサーバーに役割、役割サービス、および機能をインストールするために必要なファイルを格納する、リモート機能ファイル共有フォルダー (サイドバイサイドストアとも呼ばれます) を設定する方法について説明します。 機能ストアをセットアップした後、これらのオペレーティングシステムを実行しているサーバーに役割、役割サービス、および機能をインストールし、機能ストアをインストールソースファイルの場所として指定できます。

#### <a name="to-create-a-feature-file-store"></a>機能ファイル ストアを作成するには

1.  ネットワーク上のサーバーに共有フォルダーを作成します たとえば、 * \\ \network\share\sxs*のようになります。

2.  機能ストアに対する適切なアクセス許可が割り当てられていることを確認します。 ソースパスまたはファイル共有では、**読み取り**アクセス許可を**Everyone**グループ (セキュリティ上の理由から推奨されません)、または*DOMAIN* \\ この機能ストアを使用して機能をインストールするサーバーのコンピューターアカウント (DOMAIN*SERverNAME*$) のいずれかに付与する必要があります。ユーザーアカウントのアクセス許可を付与するだけでは不十分です。

    ファイル共有およびアクセス許可の設定にアクセスするには、Windows デスクトップで次のどちらかを実行します。

    -   共有フォルダーを右クリックして **[プロパティ]** をクリックし、**[セキュリティ]** タブで、許可されるユーザーとそのアクセス権を変更します。

    -   共有フォルダーを右クリックして **[共有]** をポイントし、**[特定のユーザー]** をクリックします。

    > [!NOTE]
    > 外部のファイル共有に対する**読み取り**アクセス許可がワークグループ サーバーのコンピューター アカウントに割り当てられている場合でも、ワークグループ内のサーバーからは、外部の共有にアクセスすることはできません。 ワークグループ サーバーで使用できる代替ソースは、インストール メディア、Windows Update、およびローカルのワークグループ サーバーに格納されている VHD ファイルと WIM ファイルです。

3.  Windows Server のインストール メディアから手順 1. で作成した共有フォルダーに **Sources\SxS** フォルダーをコピーします。

## <a name="methods-of-removing-feature-files"></a><a name=BKMK_methods></a>機能ファイルを削除する方法
オンデマンド機能の構成では、2 種類の方法で Windows Server から機能ファイルを削除できます。

-   `remove`コマンドレットのパラメーターを使用すると、 `Uninstall-WindowsFeature` windows Server 2012 R2 または windows server 2012 を実行しているサーバーまたはオフラインの仮想ハードディスク (VHD) から機能ファイルを削除できます。 パラメーターの有効な値 `remove` は、ロール、ロールサービス、および機能の名前です。

-   展開イメージのサービスと管理 (DISM) コマンドを使用すると、不要な機能ファイルや他のリモート ソースから取得できる機能ファイルを省くことでディスク領域を節約できるカスタムの WIM ファイルを作成できます。 DISM を使用したカスタム イメージの準備の詳細については、「 [Windows の機能を有効または無効にする方法](/previous-versions/windows/it-pro/windows-8.1-and-8/hh824822(v=win.10))」を参照してください。

## <a name="remove-feature-files-by-using-uninstall-windowsfeature"></a><a name=BKMK_remove></a>Uninstall-WindowsFeature を使用して機能ファイルを削除する
Windows Server 2012 R2 または Windows Server 2012 を実行しているサーバーおよびオフライン Vhd から役割、役割サービス、および機能をアンインストールしたり、機能ファイルを削除したりするには、Uninstall コマンドレットを使用します。 必要に応じて、同じコマンドで同じ役割、役割サービス、および機能をアンインストールおよび削除することができます。

> [!IMPORTANT]
> 役割、役割サービス、または機能、削除するファイルに依存する役割、役割サービス、および機能の機能ファイルも削除すると、削除されます。 役割サービスやサブ機能の機能ファイルを削除する場合は、親の役割または機能の役割サービスやサブ機能がほかにインストールされていなければ、親の役割または機能に対するファイルが削除されます。 `Uninstall-WindowsFeature -remove` コマンドで削除されるすべての機能ファイルを表示するには、コマンドに `whatif` パラメーターを追加して実行します。これにより、機能ファイルを実際に削除せずに結果を確認することができます。

#### <a name="to-remove-role-and-feature-files-by-using-uninstall-windowsfeature"></a>Uninstall-WindowsFeature を使用して役割と機能のファイルを削除するには

1.  次のいずれかを実行して、管理者特権を使って Windows PowerShell セッションを開きます。

    > [!NOTE]
    > リモートサーバーから役割と機能をアンインストールする場合は、管理者特権で Windows PowerShell を実行する必要はありません。

    -   Windows デスクトップで、タスク バーの **[Windows PowerShell]** を右クリックし、**[管理者として実行]** をクリックします。

    -   Windows の**スタート**画面で、[windows PowerShell] タイルを右クリックし、アプリバーの [**管理者として実行**] をクリックします。

    -   Server Core インストールオプションを実行しているサーバーで、コマンドプロンプトに「 **PowerShell** 」と入力し、 **enter キーを**押します。

2.  次のように入力して **Enter** キーを押します。

    ```
    Uninstall-WindowsFeature -Name <feature_name> -computerName <computer_name> -remove
    ```

    **例:** リモート デスクトップ サービスの役割サービスのうち、インストールされている残りのサービスがリモート デスクトップ ライセンスだけであるとします。 この場合、次のコマンドを実行すると、リモート デスクトップ ライセンスがアンインストールされ、指定したサーバー (*contoso_1*) からリモート デスクトップ サービスの役割全体の機能ファイルが削除されます。

    ```
    Uninstall-WindowsFeature -Name rdS-Licensing -computerName contoso_1 -remove
    ```

    **例:** 次の例では、active directory ドメインサービスとグループポリシー管理をオフライン VHD から削除します。 最初に役割と機能がアンインストールされ、さらにそれらの機能ファイルがオフライン VHD (*Contoso.vhd*) から完全に削除されます。

    > [!NOTE]
    > `computerName`Windows 8.1 または Windows 8 を実行しているコンピューターからコマンドレットを実行する場合は、パラメーターを追加する必要があります。
    >
    > ネットワーク共有から VHD ファイルの名前を入力する場合、その共有は、VHD をマウントするために選択したサーバーのコンピューターアカウントに**読み取り**と**書き込み**のアクセス許可を付与する必要があります。 ユーザー専用のアカウントにアクセス許可を与えるだけでは不十分です。 ネットワーク共有では、**読み取り**アクセス許可と**書き込み**アクセス許可を **Everyone** グループに付与し、VHD へのアクセスを許可することができますが、セキュリティ上の理由からこの方法はお勧めしません。

    ```
    Uninstall-WindowsFeature -Name AD-Domain-Services,GPMC -VHD C:\WS2012VHDs\Contoso.vhd -computerName ContosoDC1
    ```

## <a name="see-also"></a>参照
[役割、役割サービス、または機能](install-or-uninstall-roles-role-services-or-features.md) 
 をインストールまたはアンインストールする[Windows Server インストールオプション](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831786(v=ws.11)) 
[Windows の機能](/previous-versions/windows/it-pro/windows-8.1-and-8/hh824822(v=win.10)) 
 を有効または無効にする方法[展開イメージのサービスと管理 (DISM) の概要](/previous-versions/windows/it-pro/windows-8.1-and-8/hh825236(v=win.10))