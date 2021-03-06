---
title: Windows Admin Center のための環境の準備
description: Windows Admin Center (Project Honolulu) のための環境の準備
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 06/07/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: d018ea65ce61cab67fe2041b9ef885d32de51b17
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811918"
---
# <a name="prepare-your-environment-for-windows-admin-center"></a>Windows Admin Center のための環境の準備

> 適用対象:Windows Admin Center、Windows Admin Center プレビュー

Windows Admin Center で管理する準備が完了する前に、追加の準備が必要ないくつかの Server バージョンがあります。

- [Windows Server 2012 および 2012 R2](#prepare-windows-server-2012-and-2012-r2)
- [Windows Server 2008 R2](#prepare-windows-server-2008-r2)
- [Microsoft Hyper-V Server 2016](#prepare-microsoft-hyper-v-server-2016)
- [Microsoft Hyper-V Server 2012 R2](#prepare-microsoft-hyper-v-server-2012-r2)

## <a name="prepare-windows-server-2012-and-2012-r2"></a>Prepare Windows Server 2012 および 2012 R2

### <a name="install-wmf-version-51-or-higher"></a>WMF バージョン 5.1 以上のインストール

Windows Admin Center には、既定で Windows Server 2012 および 2012 R2 に含まれていない PowerShell 機能が必要です。 Windows Admin Center で Windows Server 2012 または 2012 R2 を管理するには、それらのサーバーに WMF バージョン 5.1 以上をインストールする必要があります。

PowerShell で `$PSVersiontable` を入力して、WMF がインストールされていること、またバージョンが 5.1 以上であることを確認します。

インストールされていない場合は、[WMF 5.1 をダウンロードしてインストール](https://docs.microsoft.com/powershell/wmf/5.1/install-configure)できます。

## <a name="prepare-windows-server-2008-r2"></a>Windows Server 2008 R2 の準備

### <a name="install-wmf-version-51-or-higher"></a>WMF バージョン 5.1 以上のインストール

Windows Admin Center では、既定で Windows Server 2008 R2 に含まれていない PowerShell 機能が必要です。 Windows Admin Center で Windows Server 2008 R22 を管理するには、それらのサーバーに WMF バージョン 5.1 以上をインストールする必要があります。 

いることを確認[.NET Framework 4.5.2 以降](https://docs.microsoft.com/dotnet/framework/install/on-windows-7)が既にコンピューターにインストールされています。

PowerShell で `$PSVersiontable` を入力して、WMF がインストールされていること、またバージョンが 5.1 以上であることを確認します。

インストールされていない場合は、[WMF 5.1 をダウンロードしてインストール](https://docs.microsoft.com/powershell/wmf/5.1/install-configure)できます。

PowerShell コンソールで `Enable-PSRemoting –force` を実行して Powershell リモート接続を有効にします。 

### <a name="enable-remote-desktop"></a>リモート デスクトップの有効化

Windows Admin Center 内でリモート デスクトップを使用するには、Windows Server 2008 R2 サーバーでリモート デスクトップを有効にする必要があります。

**サーバー マネージャー**で、 **[リモート デスクトップの構成]** に移動します。 リモート デスクトップを有効にし、リモート デスクトップを実行しているコンピューターからの接続を許可します。

## <a name="prepare-microsoft-hyper-v-server-2016"></a>Microsoft Hyper-V Server 2016 の準備

Windows Admin Center で Microsoft Hyper-V Server 2016 を管理するには、事前に有効にする必要のあるサーバーの役割がいくつかあります。

### <a name="to-manage-microsoft-hyper-v-server-2016-with-windows-admin-center"></a>Windows Admin Center で Microsoft Hyper-V Server 2016 を管理するには:

1. リモート管理を有効にします。
2. ファイル サーバーの役割を有効にします。
3. PowerShell 用 Hyper-V モジュールを有効にします。

### <a name="step-1-enable-remote-management"></a>**手順 1:** リモート管理の有効化

Hyper-V Server でリモート管理を有効にするには:

1. Hyper-V Server にログインします。
2. **サーバー構成** (SCONFIG) ツールで、**4** を入力してリモート管理を構成します。
3. **1** を入力してリモート管理を有効にします。
4. **4** を入力してメイン メニューに戻ります。

### <a name="step-2-enable-file-server-role"></a>**手順 2:** ファイル サーバーの役割の有効化

基本的なファイル共有とリモート管理のためにファイル サーバー ロールを有効にするには:

1. **[ツール]** メニューで **[役割と機能]** をクリックします。
2. **[役割と機能]** で、 **[ファイルおよび記憶域サービス]** を見つけて、 **[ファイルおよび iSCSI サービス]** と **[ファイル サーバー]** をオンにします。

![スクリーン ショットの役割と機能のファイルおよび iSCSI サービスの役割の選択の表示](../media/prepare-environment/c6c30b812d96afcc1edcdb6f52f0e13c.png)

### <a name="step-3-enable-hyper-v-module-for-powershell"></a>**手順 3:** PowerShell の Hyper-V モジュールの有効化

PowerShell 機能の Hyper-V モジュールを有効にするには:

1. **[ツール]** メニューで **[役割と機能]** をクリックします。
2. **[役割と機能]** で、 **[リモート サーバー管理ツール]** を見つけて **[役割管理ツール]** と **[PowerShell 用 Hyper-V モジュール]** をオンにします。

![スクリーン ショットの役割と機能が選択されている、HYPER-V ロールを示す](../media/prepare-environment/7ab0999602b7083733525bd0c1ba2747.png)

これで、Microsoft Hyper-V Server 2016 は、Windows Admin Center で管理するための準備が整いました。

## <a name="prepare-microsoft-hyper-v-server-2012-r2"></a>Microsoft Hyper-V Server 2012 R2 の準備

Windows Admin Center で Microsoft Hyper-V Server 2012 R2 を管理するには、事前に有効にする必要があるサーバーの役割がいくつかあります。  また、WMF バージョン 5.1 以上をインストールする必要があります。

### <a name="to-manage-microsoft-hyper-v-server-2012-r2-with-windows-admin-center"></a>Windows Admin Center で Microsoft Hyper-V Server 2012 R2 を管理するには:

1. Windows Management Framework (WMF) バージョン 5.1 以上のインストール
2. リモート管理の有効化
3. ファイル サーバーの役割の有効化
4. PowerShell の Hyper-V モジュールの有効化

### <a name="step-1-install-windows-management-framework-51"></a>手順 1:Windows Management Framework 5.1 をインストールします。

Windows Admin Center では、既定で Microsoft Hyper-V Server 2012 R2 に含まれていない PowerShell 機能が必要です。 Windows Admin Center で Microsoft Hyper-V Server 2012 R2 を管理するには、WMF バージョン 5.1 以上をインストールする必要があります。

PowerShell で `$PSVersiontable` を入力して、WMF がインストールされていること、またバージョンが 5.1 以上であることを確認します。 

インストールされていない場合は、[WMF 5.1 をダウンロード](https://docs.microsoft.com/powershell/wmf/5.1/install-configure)することができます。

### <a name="step-2-enable-remote-management"></a>手順 2:リモート管理の有効化

Hyper-V Server のリモート管理を有効にするには:

1. Hyper-V Server にログインします。
2. **サーバー構成** (SCONFIG) ツールで、**4** を入力してリモート管理を構成します。
3. **1** を入力してリモート管理を有効にします。
4. **4** を入力してメイン メニューに戻ります。

### <a name="step-3-enable-file-server-role"></a>手順 3:ファイル サーバーの役割の有効化

基本的なファイル共有とリモート管理のためにファイル サーバー ロールを有効にするには:

1. **[ツール]** メニューで **[役割と機能]** をクリックします。
2. **[役割と機能]** で、 **[ファイルおよび記憶域サービス]** を見つけて、 **[ファイルおよび iSCSI サービス]** と **[ファイル サーバー]** をオンにします。

![スクリーン ショットの役割と機能のファイルおよび iSCSI サービスの役割の選択の表示](../media/prepare-environment/c6c30b812d96afcc1edcdb6f52f0e13c.png)

### <a name="step-4-enable-hyper-v-module-for-powershell"></a>手順 4:PowerShell の Hyper-V モジュールの有効化

PowerShell 機能の Hyper-V モジュールを有効にするには:

1. **[ツール]** メニューで **[役割と機能]** をクリックします。
2. **[役割と機能]** で、 **[リモート サーバー管理ツール]** を見つけて **[役割管理ツール]** と **[PowerShell 用 Hyper-V モジュール]** をオンにします。

![スクリーン ショットの役割と機能を示す、HYPER-V のリモート サーバー管理ツールが選択されています。](../media/prepare-environment/7ab0999602b7083733525bd0c1ba2747.png)

これで、Microsoft Hyper-V Server 2012 R2 は、Windows Admin Center で管理するための準備が整いました。

> [!Tip]
> Windows Admin Center をインストールする準備はできましたか。 [今すぐダウンロード](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/windows-admin-center#download-now)