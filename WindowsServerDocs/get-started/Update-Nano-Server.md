---
title: Nano Server の更新
description: " "
ms.prod: windows-server-threshold
ms.service: na
manager: DonGill
ms.technology: server-nano
ms.date: 09/06/2017
ms.tgt_pltfrm: na
ms.topic: get-started-article
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: 7f74b35e93d4ddbe39b955daf7f78c4ef693aa9a
ms.sourcegitcommit: 07ac08dea2b8f2763c2614a999dc7967018aa0b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2018
ms.locfileid: "6121471"
---
# Nano Server の更新

> [!IMPORTANT]
> Windows Server バージョン 1709 以降、Nano Server は[コンテナー基本 OS イメージ](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image)としてのみ提供されます。 その意味については、「[Nano Server に加えられる変更](nano-in-semi-annual-channel.md)」をご覧ください。 

Nano Server を最新の状態に保つには、さまざまな方法が用意されています。 Windows Server の他のインストール オプションに比べて、Nano Server では、Windows 10 に近いアクティブなサービス モデルが採用されています。 このような定期的なリリースは、**Current Branch for Business (CBB)** リリースと呼ばれます。 このアプローチは、もっとすばやく改革を取り入れ、クラウド上での短期間の開発ライフサイクルに対応する必要のあるお客様をサポートするものです。 CBB について詳しくは、[Windows Server ブログの記事](https://blogs.technet.microsoft.com/windowsserver/2016/07/12/windows-server-2016-new-current-branch-for-business-servicing-option/)をご覧ください。

**これらの CBB リリースの合間**には、Nano Server は一連の*累積的な更新プログラム*によって最新の状態に維持されます。 たとえば、Nano Server の最初の累積的な更新プログラムは、2016 年 9 月 26 日、 [KB4093120](https://support.microsoft.com/help/4093120/windows-10-update-kb4093120)にリリースされました。 これ以降の累積的な更新プログラムでは、これらの更新プログラムを Nano Server にインストールするためのさまざまな方法が提供されています。 この記事では、KB3192366 の更新プログラムを例として使い、Nano Server の累積的な更新プログラムを取得して適用する方法を説明します。 累積的な更新プログラムのモデルについて詳しくは、[Microsoft Update ブログの記事](https://blogs.technet.microsoft.com/mu/2016/10/25/patching-with-windows-server-2016/) (英語) をご覧ください。

> [!NOTE]
> オプションの Nano Server パッケージをメディアやオンライン リポジトリからインストールする場合、そのパッケージには最近のセキュリティ修正プログラムが含まれていません。 オプションのパッケージとベースのオペレーティング システムの間のバージョンの不一致を避けるためには、オプションのパッケージをインストールした直後に必ず、サーバーを再起動する**前に**、最新の累積的な更新をインストールする必要があります。

Windows Server 2016 の累積的な更新プログラム: September 26, 2016 年 9 月 26 日 ([KB3192366](https://support.microsoft.com/en-us/kb/3192366)) の場合は、必要条件として、まず最新の Windows 10 Version 1607 のサービス スタック更新プログラム: 2016 年 8 月 23 日 ([KB3176936](https://support.microsoft.com/en-us/kb/3176936)) をインストールする必要があります。 以下で説明する方法のほとんどでは、.cab 更新プログラム パッケージを収録した .msu ファイルが必要になります。 それぞれの更新プログラム パッケージをダウンロードするには、Microsoft Update カタログの以下のページにアクセスしてください。
- [https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB3192366](https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB3192366)
- [https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB3176936](https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB3176936)

Microsoft Update カタログから .msu ファイルをダウンロードしたら、それらをネットワーク共有または C:\ServicingPackages などのローカル ディレクトリに保存します。 各ファイルを見分けやすくするために、以下のように KB 番号に従って .msu ファイルの名前を変更してもかまいません。 次に、EXPAND ユーティリティを使って .msu ファイルから .cab ファイルを別々のディレクトリに展開し、それらの .cab ファイルを 1 つのフォルダーにコピーします。

```code
    mkdir C:\ServicingPackages_expanded
    mkdir C:\ServicingPackages_expanded\KB3176936
    mkdir C:\ServicingPackages_expanded\KB3192366
    Expand C:\ServicingPackages\KB3176936.msu -F:* C:\ServicingPackages_expanded\KB3176936
    Expand C:\ServicingPackages\KB3192366.msu -F:* C:\ServicingPackages_expanded\KB3192366
    mkdir C:\ServicingPackages_cabs
    copy C:\ServicingPackages_expanded\KB3176936\Windows10.0-KB3176936-x64.cab C:\ServicingPackages_cabs
    copy C:\ServicingPackages_expanded\KB3192366\Windows10.0-KB3192366-x64.cab C:\ServicingPackages_cabs
```

その後、展開した .cab ファイルを使って、いくつかの異なる方法からニーズに合った方法で Nano Server イメージに更新プログラムを適用できます。 以降では、使用できる方法を順不同で紹介します。お使いの環境に最も適した方法を選んでください。

> [!NOTE]
> DISM ツールを使って Nano Server をサービスする場合は、サービスの対象となる Nano Server のバージョンと同じかそれよりも新しいバージョンの DISM を使う必要があります。 そのためには、一致するバージョンの Windows から DISM を実行するか、一致するバージョンの [Windows アセスメント & デプロイメント キット (ADK)](https://developer.microsoft.com/en-us/windows/hardware/windows-assessment-deployment-kit) をインストールするか、または Nano Server 上で DISM を実行します。

## 方法 1: 新しいイメージに累積的な更新プログラムを統合する
新しい Nano Server イメージを作成する場合は、最新の累積的な更新プログラムをイメージに直接統合して、初回起動時に更新プログラムが完全に適用されるようにすることができます。

```powershell
New-NanoServerImage -ServicingPackagePath 'C:\ServicingPackages_cabs\Windows10.0-KB3176936-x64.cab', 'C:\ServicingPackages_cabs\Windows10.0-KB3192366-x64.cab' -<other parameters>
```

## 方法 2: 既存のイメージに累積的な更新プログラムを統合する
Nano Server の特定のインスタンスを作成するために既存の Nano Server イメージをベースラインとして使う場合は、最新の累積的な更新プログラムを既存のベースライン イメージに直接統合して、そのイメージから作成されたマシンの初回起動時に更新プログラムが完全に適用されるようにすることができます。

```powershell
Edit-NanoServerImage -ServicingPackagePath 'C:\ServicingPackages_cabs\Windows10.0-KB3176936-x64.cab', 'C:\ServicingPackages_cabs\Windows10.0-KB3192366-x64.cab' -TargetPath .\NanoServer.wim
```

## 方法 3: 既存のオフライン VHD または VHDX に累積的な更新プログラムを適用する
既に仮想ハード ディスク (VHD または VHDX) がある場合は、DISM ツールを使って仮想ハード ディスクに更新プログラムを適用できます。 ディスクが使用中にならないように、そのディスクを使っているすべての VM をシャットダウンするか、仮想ハード ディスク ファイルのマウントを解除する必要があります。

- PowerShell を使用する

   ```powershell
   Mount-WindowsImage -ImagePath .\NanoServer.vhdx -Path .\MountDir -Index 1
   Add-WindowsPackage -Path .\MountDir -PackagePath  C:\ServicingPackages_cabs
   Dismount-WindowsImage -Path .\MountDir -Save
   ```

- dism.exe を使用する

   ```code
   dism.exe /Mount-Image /ImageFile:C:\NanoServer.vhdx /Index:1 /MountDir:C:\MountDir
   dism.exe /Image:C:\MountDir /Add-Package /PackagePath:C:\ServicingPackages_cabs
   dism.exe /Unmount-Image /MountDir:C:\MountDir /Commit
   ```

## 方法 4: 実行中の Nano Server に累積的な更新プログラムを適用する
実行中の Nano Server VM または物理ホストがあり、更新プログラムの .cab ファイルをダウンロードした場合は、DISM ツールを使って、オペレーティング システムがオンラインの間に更新プログラムを適用できます。 .cab ファイルは、Nano Server 上にローカルにコピーするか、アクセス可能なネットワーク上の場所にコピーする必要があります。 サービス スタック更新プログラムを適用する場合は、サービス スタック更新プログラムの適用後、他の更新プログラムを適用する前に、必ずサーバーを再起動してください。

> [!NOTE]
> New-NanoServerImage コマンドレットを使って Nano Server の VHD または VHDX イメージを作成した場合、仮想ハード ディスク ファイルの MaxSize を指定しないと既定のサイズの 4 GB になりますが、このサイズでは小さすぎて累積的な更新プログラムを適用できません。 更新プログラムをインストールする前に、Hyper-V マネージャー、ディスクの管理、PowerShell、その他のツールを使って、仮想ハード_ディスクとシステム ボリュームのサイズを 10 GB 以上に拡張するか、または DISM ツールの ScratchDir パラメーターを使って、スクラッチ ディレクトリを 10 GB 以上の空き領域のあるボリュームに設定してください。

```powershell
$s = New-PSSession -ComputerName (Read-Host "Enter Nano Server IP address") -Credential (Get-Credential)
Copy-Item -ToSession $s -Path C:\ServicingPackages_cabs -Destination C:\ServicingPackages_cabs -Recurse
Enter-PSSession $s
```

- PowerShell を使用する

   ```powershell
   # Apply the servicing stack update first and then restart
   Add-WindowsPackage -Online -PackagePath C:\ServicingPackages_cabs\Windows10.0-KB3176936-x64.cab
   Restart-Computer; exit

   # After restarting, apply the cumulative update and then restart
   Enter-PSSession -ComputerName (Read-Host "Enter Nano Server IP address") -Credential (Get-Credential)
   Add-WindowsPackage -Online -PackagePath C:\ServicingPackages_cabs\Windows10.0-KB3192366-x64.cab
   Restart-Computer; exit
   ```

- dism.exe を使用する
   ```powershell
   # Apply the servicing stack update first and then restart
   dism.exe /Online /Add-Package /PackagePath:C:\ServicingPackages_cabs\Windows10.0-KB3176936-x64.cab
   
   # After the operation completes successfully and you are prompted to restart, it's safe to
   # press Ctrl+C to cancel the pipeline and return to the prompt
   Restart-Computer; exit

   # After restarting, apply the cumulative update and then restart
   Enter-PSSession -ComputerName (Read-Host "Enter Nano Server IP address") -Credential (Get-Credential)
   dism.exe /Online /Add-Package /PackagePath:C:\ServicingPackages_cabs\Windows10.0-KB3192366-x64.cab
   Restart-Computer; exit
   ```

## 方法 5: 累積的な更新プログラムをダウンロードして実行中の Nano Server にインストールする

実行中の Nano Server VM または物理ホストがある場合は、Windows Update WMI プロバイダーを使って、オペレーティング システムがオンラインの間に更新プログラムをダウンロードしてインストールできます。 この方法では、Microsoft Update カタログから .msu ファイルを個別にダウンロードする必要はありません。 WMI プロバイダーにより、利用可能なすべての更新プログラムの検出、ダウンロード、インストールが一度に行われます。

```powershell
Enter-PSSession -ComputerName (Read-Host "Enter Nano Server IP address") -Credential (Get-Credential)
```

- 利用可能な更新プログラムをスキャンする
   ```powershell
   $ci = New-CimInstance -Namespace root/Microsoft/Windows/WindowsUpdate -ClassName MSFT_WUOperationsSession  
   $result = $ci | Invoke-CimMethod -MethodName ScanForUpdates -Arguments @{SearchCriteria="IsInstalled=0";OnlineScan=$true}
   $result.Updates
   ```

- 利用可能なすべての更新プログラムをインストールする
   ```powershell
   $ci = New-CimInstance -Namespace root/Microsoft/Windows/WindowsUpdate -ClassName MSFT_WUOperationsSession
   Invoke-CimMethod -InputObject $ci -MethodName ApplyApplicableUpdates
   Restart-Computer; exit
   ```

- インストールされた更新プログラムの一覧を取得する
   ```powershell
   $ci = New-CimInstance -Namespace root/Microsoft/Windows/WindowsUpdate -ClassName MSFT_WUOperationsSession
   $result = $ci | Invoke-CimMethod -MethodName ScanForUpdates -Arguments @{SearchCriteria="IsInstalled=1";OnlineScan=$true}
   $result.Updates
   ```
   
## 追加オプション
Nano Server のその他の更新方法には、上記の方法と一部が共通していたり、上記の方法を補完したりするものがあります。 このようなオプションとして、Windows Server Update Services (WSUS)、System Center Virtual Machine Manager (VMM)、タスク スケジューラー、または Microsoft 以外のソリューションを使う方法があります。
- 次のレジストリ キーを設定して、[WSUS 用に Windows Update を構成](https://msdn.microsoft.com/en-us/library/dd939844(v=ws.10).aspx)します。
  - WUServer
  - WUStatusServer (通常は WUServer と同じ値を使います)
  - UseWUServer
  - AUOptions
- [VMM でファブリックの更新を管理する](https://technet.microsoft.com/library/gg675084(v=sc.12).aspx)
- [スケジュールされたタスクを登録する](https://technet.microsoft.com/library/jj649811.aspx)