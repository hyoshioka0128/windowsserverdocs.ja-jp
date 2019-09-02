---
title: Windows Server 2016 で削除された機能または推奨されなくなった機能
description: Windows Server 2016 の機能のうち、現在のリリースで製品から削除された機能および今後のリリースで削除が検討されている機能 (非推奨の機能) の一覧。 商用環境でオペレーティング システムを更新する IT 担当者を対象としています。
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
ms.date: 08/22/2019
ms.assetid: 5d10c5f9-ebac-49a0-b808-c0b1702e0437
author: jasongerend
ms.author: jgerend
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: a35da3fda1736139290a2503a5c06317cf322ccc
ms.sourcegitcommit: 6f8993e2180c4d3c177e3e1934d378959396b935
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000610"
---
# <a name="features-removed-or-deprecated-in--windows-server-2016"></a>Windows Server 2016 で削除された機能または推奨されなくなった機能

>適用対象:Windows Server 2016

次の一覧に、Windows Server 2016 の機能のうち、現在のリリースで製品から削除された機能および今後のリリースで削除が検討されている機能 (推奨されなくなった機能) を示します。 商用環境でオペレーティング システムを更新する IT 担当者を対象としています。 この一覧は、今後のリリースで変更される可能性があります。また、使用が推奨されなくなった機能でこの一覧に含まれていないものもあります。 特定の機能とそれに置き換わる機能の詳細については、該当する機能のドキュメントを参照してください。

> [!TIP]
> 新しいバージョンで削除された機能や非推奨となった機能については、「[Windows Server で削除された機能と置換が計画されている機能](../get-started-19/removed-features.md)」を参照してください。

## <a name="features-removed-from-windows-server-2016"></a>Windows Server 2016 から削除された機能

以下の機能は、このリリースの Windows Server 2016 で削除されました。 このリリースでは、別の方法を使用しない限り、これらの機能に依存するアプリケーション、コード、使用法は機能しません。  

> [!NOTE]  
> Windows Server 2016 を Windows Server 2012 R2 または Windows Server 2012 より前のサーバー リリースから移行する場合は、「[Windows Server 2012 R2 で削除された機能または推奨されなくなった機能](https://technet.microsoft.com/library/dn303411.aspx)」および「[Windows Server 2012 で削除された機能または推奨されなくなった機能](https://technet.microsoft.com/library/hh831568.aspx)」も確認してください。  

### <a name="share-and-storage-management"></a>共有と記憶域の管理

Microsoft 管理コンソール用の共有と記憶域の管理スナップインは削除されました。 代わりに、次のいずれかの方法を使用できます。  

-   管理するコンピューターで Windows Server 2016 よりも前のオペレーティング システムを実行している場合は、リモート デスクトップで対象のコンピューターに接続し、共有と記憶域の管理スナップインのローカル バージョンを使用できます。  

-   Windows 8.1 以前が実行されているコンピューターでは、共有と記憶域の管理スナップインを RSAT から使用して、管理するコンピューターを表示できます。  

-   クライアント コンピューターで Hyper-V を使用して、RSAT の共有と記憶域の管理スナップインが含まれる Windows 7、Windows 8、または Windows 8.1 を実行する仮想マシンを実行できます。  

### <a name="journaldll"></a>Journal.dll

Journal.dll は Windows Server 2016 から削除されました。 これに置き換わるものはありません。  

### <a name="security-configuration-wizard"></a>セキュリティの構成ウィザード

セキュリティの構成ウィザードは削除されました。 代わりに、機能は既定でセキュリティ保護されています。 特定のセキュリティ設定を制御する必要がある場合は、グループ ポリシーまたは [Microsoft Security Compliance Manager](https://technet.microsoft.com/solutionaccelerators/cc835245.aspx) を使用できます。  

### <a name="sqm"></a>SQM

カスタマー エクスペリエンス向上プログラムへの参加を管理するオプトイン コンポーネントは削除されました。 

### <a name="windows-update"></a>Windows Update

**Wuauclt.exe/detectnow** コマンドは廃止され、サポートが終了しました。 更新のスキャンをトリガーするには、次のいずれかの操作を行います。

- 以下の PowerShell コマンドを実行する。
    ````powershell
    $AutoUpdates = New-Object -ComObject "Microsoft.Update.AutoUpdate"
    $AutoUpdates.DetectNow()
    ````

- 代わりに、以下の VBScript を使用する。
    ````vb
    Set automaticUpdates = CreateObject("Microsoft.Update.AutoUpdate")
    automaticUpdates.DetectNow()
    ````

## <a name="features-deprecated-starting-with-windows-server-2016"></a>Windows Server 2016 から推奨されなくなった機能

以下の機能は、このリリースから非推奨とされます。 これらの機能は、最終的に製品から完全に削除される予定ですが、このリリースでは使用できます (一部の機能が削除されている場合もあります)。 これらの機能に依存するアプリケーション、コード、使用法については、別の方法の使用を今から計画する必要があります。  

### <a name="configuration-tools"></a>構成ツール  

-   **Scregedit.exe** は非推奨となりました。 Scregedit.exe に依存するスクリプトを使っている場合は、Reg.exe または Windows PowerShell のメソッドを使用するように調整してください。  

-   **Sconfig.exe** は非推奨となりました。 代わりに Windows PowerShell を使用してください。  

### <a name="netcfg-custom-apis"></a>NetCfg のカスタム API

NetCfg のカスタム API を使用した PrintProvider、NetClient、および ISDN のインストールは非推奨となりました。  

### <a name="remote-management"></a>リモート管理  

WinRM.vbs は非推奨となりました。 代わりに、Windows PowerShell の WinRM プロバイダーの機能を使用してください。  

### <a name="smb"></a>SMB

NetBT 経由の SMB 2+ は非推奨となりました。 代わりに TCP または RDMA 経由の SMB を実装してください。 
