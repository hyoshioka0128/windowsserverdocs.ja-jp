---
title: Configure Features on Demand in Windows Server
description: サーバー マネージャー
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: c77bd088a02d405b17a4f7decd6093785296d5e8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818933"
---
# <a name="configure-features-on-demand-in-windows-server"></a>Configure Features on Demand in Windows Server

>適用先:Windows Server 2016

このトピックでは、Uninstall-WindowsFeature コマンドレットを使用してオンデマンド機能の構成で機能ファイルを削除する方法について説明します。

オンデマンド機能は、Windows 8 および Windows Server 2012、役割と機能のファイルを削除することができますを導入している機能 (機能とも呼ばれる*ペイロード*) ディスクの領域を節約して、役割をインストールするには、オペレーティング システムからリモートの場所またはローカル コンピューターからの代わりに、インストール メディアからの機能です。 機能ファイルは、実行中の物理コンピューターまたは仮想コンピューターから削除できます。 また、Windows イメージ (WIM) ファイルまたはオフラインの仮想ハード ディスク (VHD) で機能ファイルを追加または削除して、オンデマンド機能の構成の再現可能なコピーを作成することもできます。

On Demand の構成、機能のインストールには、それらの機能ファイルが必要な場合、コンピューターで利用できない機能ファイルが Windows Server 2012 R2 または Windows Server 2012 できますが表示でサイド バイ サイド機能ストア (共有フォルダーからファイルを取得するには機能ファイルを含む、ネットワーク上のコンピューターで利用可能)、Windows Update、またはインストール メディアから。 オンデマンド機能の既定の動作では、対象サーバーで機能ファイルを利用できない場合、次のタスクを表示されている順序で実行して見つからない機能ファイルを検索します。

1.  追加の役割と機能のウィザード、または DISM インストール コマンドのユーザーが指定されている場所で検索

2.  グループ ポリシー設定の構成を評価する**オプション コンポーネントのインストールおよびコンポーネントの修復のコンピューターの構成 \ 管理用 \ 設定**

3.  Windows Update を検索する

オンデマンド機能の既定の動作は、次のいずれかの方法で変更できます。

-   `Install-WindowsFeature` コマンドレットに `Source` パラメーターを追加して代替ソース パスを指定する

-   代替ソース パスを指定する、**インストール オプションを確認**役割の追加と機能のウィザードを使用して機能をインストールするときにページ

-   グループ ポリシー設定 **"オプション コンポーネントのインストールおよびコンポーネントの修復のための設定を指定する"** を構成する

このトピックは次のセクションで構成されます。

-   [機能のファイルまたはサイド バイ サイド ストアを作成します。](#BKMK_store)

-   [機能ファイルを削除する方法](#BKMK_methods)

-   [Uninstall-windowsfeature を使用して機能ファイルを削除します。](#BKMK_remove)

## <a name="BKMK_store"></a>機能のファイルまたはサイド バイ サイド ストアを作成します。
このセクションでは、(サイド バイ サイド ストアとも呼ばれます) では、Windows Server 2012 R2 を実行しているサーバーまたは Windows Server 2012 の役割、役割サービス、および機能のインストールに必要なファイルを格納するリモート機能ファイルの共有フォルダーを設定する方法について説明します。 機能ストアをセットアップした後は、これらのオペレーティング システムを実行しているサーバーの役割、役割サービス、および機能をインストールし、インストール ソース ファイルの場所として機能ストアを指定できます。

#### <a name="to-create-a-feature-file-store"></a>機能ファイル ストアを作成するには

1.  ネットワーク上のサーバーに共有フォルダーを作成します たとえば、  *\\\network\share\sxs*します。

2.  機能ストアに対する適切なアクセス許可が割り当てられていることを確認します。 ソース パスまたはファイル共有を許可する必要があります**読み取り**アクセス許可のいずれか、 **Everyone** (推奨されませんセキュリティ上の理由)、グループまたはコンピューター アカウントに (*ドメイン*\\ *SERverNAME*$) のサーバーがこの機能ストアを使用して機能をインストールする; ユーザー アカウントのアクセス許可を与えるには不十分です。

    ファイル共有およびアクセス許可の設定にアクセスするには、Windows デスクトップで次のどちらかを実行します。

    -   共有フォルダーを右クリックして **[プロパティ]** をクリックし、 **[セキュリティ]** タブで、許可されるユーザーとそのアクセス権を変更します。

    -   共有フォルダーを右クリックして **[共有]** をポイントし、 **[特定のユーザー]** をクリックします。

    > [!NOTE]
    > 外部のファイル共有に対する**読み取り**アクセス許可がワークグループ サーバーのコンピューター アカウントに割り当てられている場合でも、ワークグループ内のサーバーからは、外部の共有にアクセスすることはできません。 ワークグループ サーバーで使用できる代替ソースは、インストール メディア、Windows Update、およびローカルのワークグループ サーバーに格納されている VHD ファイルと WIM ファイルです。

3.  Windows Server のインストール メディアから手順 1. で作成した共有フォルダーに **Sources\SxS** フォルダーをコピーします。

## <a name="BKMK_methods"></a>機能ファイルを削除する方法
オンデマンド機能の構成では、2 種類の方法で Windows Server から機能ファイルを削除できます。

-   `remove`のパラメーター、`Uninstall-WindowsFeature`コマンドレットを使用して、サーバーまたはオフライン仮想ハード_ディスク (VHD) が実行されているは、Windows Server 2012 R2 または Windows Server 2012 から機能ファイルを削除できます。 有効な値、`remove`パラメーターは、役割、役割サービス、および機能の名前を示します。

-   展開イメージのサービスと管理 (DISM) コマンドを使用すると、不要な機能ファイルや他のリモート ソースから取得できる機能ファイルを省くことでディスク領域を節約できるカスタムの WIM ファイルを作成できます。 DISM を使用したカスタム イメージの準備の詳細については、「 [Windows の機能を有効または無効にする方法](https://technet.microsoft.com/library/hh824822.aspx)」を参照してください。

## <a name="BKMK_remove"></a>Uninstall-windowsfeature を使用して機能ファイルを削除します。
サーバーまたは Windows Server 2012 R2 または Windows Server 2012 を実行しているオフライン Vhd から役割、役割サービス、および機能をアンインストールして、機能ファイルを削除するのには、Uninstall-windowsfeature コマンドレットを使用できます。 アンインストールし、必要な場合は、同じの役割、役割サービス、および同じコマンドで機能を削除します。

> [!IMPORTANT]
> ロール機能ファイルを削除するときに、役割サービス、または機能、役割、役割サービス、および削除するファイルに依存する機能も削除されます。 役割サービスやサブ機能の機能ファイルを削除する場合は、親の役割または機能の役割サービスやサブ機能がほかにインストールされていなければ、親の役割または機能に対するファイルが削除されます。 `Uninstall-WindowsFeature -remove` コマンドで削除されるすべての機能ファイルを表示するには、コマンドに `whatif` パラメーターを追加して実行します。これにより、機能ファイルを実際に削除せずに結果を確認することができます。

#### <a name="to-remove-role-and-feature-files-by-using-uninstall-windowsfeature"></a>Uninstall-WindowsFeature を使用して役割と機能のファイルを削除するには

1.  次のいずれかを実行して、管理者特権を使って Windows PowerShell セッションを開きます。

    > [!NOTE]
    > リモート サーバーから役割と機能をアンインストールする場合は、管理者特権で Windows PowerShell を実行する必要はありません。

    -   Windows デスクトップで、タスク バーの **[Windows PowerShell]** を右クリックし、 **[管理者として実行]** をクリックします。

    -   Windows で**開始**画面、Windows PowerShell タイルを右クリックし、アプリ バーでクリックして**管理者として実行**します。

    -   Server Core インストール オプションを実行しているサーバーで次のように入力します。 **PowerShell**にコマンド プロンプトを押してから**Enter**。

2.  次のように入力して **Enter**キーを押します。

    ```
    Uninstall-WindowsFeature -Name <feature_name> -computerName <computer_name> -remove
    ```

    **例:** リモート デスクトップ サービスの役割サービスのうち、インストールされている残りのサービスがリモート デスクトップ ライセンスだけであるとします。 この場合、次のコマンドを実行すると、リモート デスクトップ ライセンスがアンインストールされ、指定したサーバー ( *contoso_1*) からリモート デスクトップ サービスの役割全体の機能ファイルが削除されます。

    ```
    Uninstall-WindowsFeature -Name rdS-Licensing -computerName contoso_1 -remove
    ```

    **例:** 次の例では、コマンドは、オフライン VHD から active directory Domain Services とグループ ポリシー管理を削除します。 最初に役割と機能がアンインストールされ、さらにそれらの機能ファイルがオフライン VHD ( *Contoso.vhd*) から完全に削除されます。

    > [!NOTE]
    > 追加する必要があります、`computerName`コマンドレットを実行する、コンピューターからいる場合は、パラメーターには、Windows 8.1 または Windows 8 が実行されています。
    > 
    > ネットワーク共有から VHD ファイルの名前を入力するかどうか、その共有を許可する必要があります**読み取り**と**書き込み**VHD のマウント先に選択したサーバーのコンピューター アカウントにアクセス許可。 ユーザー専用のアカウントにアクセス許可を与えるだけでは不十分です。 ネットワーク共有では、**読み取り**アクセス許可と**書き込み**アクセス許可を **Everyone** グループに付与し、VHD へのアクセスを許可することができますが、セキュリティ上の理由からこの方法はお勧めしません。

    ```
    Uninstall-WindowsFeature -Name AD-Domain-Services,GPMC -VHD C:\WS2012VHDs\Contoso.vhd -computerName ContosoDC1
    ```

## <a name="see-also"></a>関連項目
[インストールまたは役割、役割サービス、または機能をアンインストール](install-or-uninstall-roles-role-services-or-features.md)
[Windows Server Installation Options](https://technet.microsoft.com/library/hh831786.aspx)
[を有効にするか、Windows の機能を無効にする方法](https://technet.microsoft.com/library/hh824822.aspx)
[Deployment Image Servicing and Management (DISM) の概要](https://technet.microsoft.com/library/hh825236.aspx)


