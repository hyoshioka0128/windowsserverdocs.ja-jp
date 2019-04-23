---
title: HYPER-V ホストをリモートで管理します。
description: HYPER-V ホストと HYPER-V マネージャー ドメイン間やスタンドアロンなどのさまざまな環境でのリモート ホストに接続する方法とバージョンの互換性について説明します。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2d34e98c-6134-479b-8000-3eb360b8b8a3
author: KBDAzure
ms.author: kathydav
ms.date: 12/06/2016
ms.openlocfilehash: df66f308ee7999f97fe7e57a8b52256f2561faa2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870233"
---
# <a name="remotely-manage-hyper-v-hosts-with-hyper-v-manager"></a>HYPER-V マネージャーと HYPER-V ホストをリモートで管理します。

>適用先:Windows Server 2016、Windows Server 2012 R2、Windows 10、Windows 8.1

この記事では、HYPER-V ホストと HYPER-V マネージャーのバージョンのサポートされる組み合わせの一覧を表示し、それらを管理できるように、リモートとローカルの HYPER-V ホストに接続する方法について説明します。 

HYPER-V マネージャーを使用して、リモートとローカルの両方の HYPER-V ホストの数が少ないを管理できます。 インストールされて、行うことができます、HYPER-V 管理ツールをインストールするときに完全な使用するか、HYPER-V をインストールまたはツールのみのインストール。 ツールのみのインストール方法を行うと、ホスト、HYPER-V のハードウェア要件を満たしていないコンピューターで、ツールを使用できます。 HYPER-V ホストのハードウェアに関する詳細については、次を参照してください。[システム要件](..\System-requirements-for-Hyper-V-on-Windows.md)します。

HYPER-V マネージャーがインストールされていない場合は、次を参照してください。、[指示](#install-hyper-v-manager)以下。

## <a name="supported-combinations-of-hyper-v-manager-and-hyper-v-host-versions"></a>HYPER-V マネージャーと HYPER-V ホストのバージョンのサポートされる組み合わせ

場合によっては、表に示すように、ホストでは、HYPER-V のバージョンよりも、HYPER-V マネージャーの別のバージョンを使用できます。 これを行うときに、HYPER-V マネージャーは、管理しているホストで HYPER-V のバージョンで使用できる機能を提供します。 たとえば、Windows Server 2012 で HYPER-V を実行するホストをリモートで管理する Windows Server 2012 R2 で HYPER-V マネージャーのバージョンを使用する場合、その HYPER-V ホスト上の Windows Server 2012 R2 で使用できる機能を使用できません。

次の表は、どのバージョンの HYPER-V ホスト、HYPER-V マネージャーの特定のバージョンから管理できます。 オペレーティング システムのバージョンの一覧についてのみサポートされます。 詳細については、特定のオペレーティング システムのバージョンのサポート状況を使用して、**検索製品のライフ サイクル**のボタンでは、 [Microsoft ライフ サイクル ポリシー](https://support.microsoft.com/lifecycle)ページ。 一般に、以前のバージョンの HYPER-V マネージャーは、同じバージョンまたは同等の Windows Server のバージョンを実行する HYPER-V ホストのみを管理できます。

|HYPER-V マネージャーのバージョン | HYPER-V ホストのバージョン|
|---|---|
|Windows 2016、Windows 10|Windows Server 2016-Nano Server、および対応するバージョンの HYPER-V サーバーを含む、すべてのエディションとインストールのオプション <br>-Windows Server 2012 R2-すべてのエディションとインストール オプション、および対応するバージョンの HYPER-V サーバー <br>Windows Server 2012-すべてのエディションとインストール オプション、および対応するバージョンの HYPER-V サーバー <br> - Windows 10 <br> - Windows 8.1  |
| Windows Server 2012 R2、Windows 8.1 | -Windows Server 2012 R2-すべてのエディションとインストール オプション、および対応するバージョンの HYPER-V サーバー <br>Windows Server 2012-すべてのエディションとインストール オプション、および対応するバージョンの HYPER-V サーバー <br>- Windows 8.1
| Windows Server 2012 | Windows Server 2012-すべてのエディションとインストール オプション、および対応するバージョンの HYPER-V サーバー
| Windows Server 2008 R2 Service Pack 1、Windows 7 Service Pack 1 | -Windows Server 2008 R2-すべてのエディションとインストール オプション、および対応するバージョンの HYPER-V サーバー
| Windows Server 2008、Windows Vista Service Pack 2 | Windows Server 2008-すべてのエディションとインストール オプション、および対応するバージョンの HYPER-V サーバー

>[!NOTE]
>2016 年 1 月 12 日に、Windows 8 用サービス パックのサポートが終了しました。 詳細については、次を参照してください。、 [Windows 8.1 の FAQ](https://support.microsoft.com/help/18581)します。

## <a name="connect-to-a-hyper-v-host"></a>HYPER-V ホストに接続します。

HYPER-V マネージャーから HYPER-V ホストに接続するには、右 **、HYPER-V マネージャー**で左側のウィンドウをクリック**サーバーへの接続**します。

## <a name="manage-hyper-v-on-a-local-computer"></a>ローカル コンピューター上の HYPER-V を管理します。

HYPER-V マネージャーには、ローカル コンピューターを含め、コンピューターを追加するまでに、HYPER-V をホストする任意のコンピューターがリスト表示されません。 これには、次の手順を実行します。

1. 左側のウィンドウで右クリック **、HYPER-V Manager**します。
2. クリックして**サーバーに接続する**します。
3. **コンピューターの選択**、 をクリックして**ローカル コンピューター**順にクリックします**OK**します。

接続することはできません。 場合、

* HYPER-V ツールのみがインストールされていることができます。 HYPER-V プラットフォームがインストールされていることを確認するには、仮想マシン管理サービスを探します。 \(サービスのデスクトップ アプリを開く: をクリックして**開始**、 をクリックして、**検索の開始**ボックスに「 **services.msc**、しキーを押します **」と入力**します。 仮想マシン管理サービスが表示されていない場合は、次の手順で、HYPER-V プラットフォームをインストール[インストール HYPER-V](..\get-started\Install-the-Hyper-V-role-on-Windows-Server.md)します。\)
* ご使用のハードウェア要件を満たしていることを確認します。 参照してください[システム要件](..\System-requirements-for-Hyper-V-on-Windows.md)します。
* ユーザー アカウントが Administrators グループまたは HYPER-V Administrators グループに属していることを確認します。

## <a name="manage-hyper-v-hosts-remotely"></a>HYPER-V ホストをリモート管理します。  

リモート HYPER-V ホストを管理するには、ローカル コンピューターとリモート ホストの両方でリモート管理が有効にします。

Windows Server で、サーバー マネージャーを開き\>**ローカル サーバー** \>**リモート管理**し**このコンピューターにリモート接続を許可する**. 

または、どちらのオペレーティング システムから管理者として Windows PowerShell を開いてし、実行します。 

```
Enable-PSRemoting
```

### <a name="connect-to-hosts-in-the-same-domain"></a>同じドメイン内のホストに接続します。

Windows 8.1 以前では、リモート管理は、同じドメインにホストがあり、ローカル ユーザー アカウントがリモート ホスト上にも場合にのみ動作します。

リモート HYPER-V ホストを HYPER-V マネージャーを追加するには、選択**別のコンピューター**で、**コンピューターの選択** ダイアログ ボックスと、リモート ホストのホスト名、NetBIOS 名、または完全修飾ドメイン名入力\(FQDN\)します。

Windows Server 2016 および Windows 10 で HYPER-V マネージャーでは、次のセクションで説明されている、以前のバージョンよりもリモート接続の種類を提供します。  

### <a name="connect-to-a-windows-2016-or-windows-10-remote-host-as-a-different-user"></a>別のユーザーとして Windows 2016 または Windows 10 のリモート ホストに接続します。

これにより、ローカル コンピューター上の HYPER-V Administrators グループまたは HYPER-V ホストの Administrators グループのいずれかのメンバーであるユーザーとして実行していないときに、HYPER-V ホストに接続できます。 これには、次の手順を実行します。

1. 左側のウィンドウで右クリック **、HYPER-V Manager**します。
1. クリックして**サーバーに接続する**します。
1. 選択**別のユーザーとして接続**で、**コンピューターの選択** ダイアログ ボックス。
1. 選択**ユーザー設定**します。

>[!NOTE]
> これは、Windows Server 2016 または Windows 10 の機能のみ**リモート**ホスト。

### <a name="connect-to-a-windows-2016-or-windows-10-remote-host-using-ip-address"></a>IP アドレスを使用して Windows 2016 または Windows 10 リモート ホストに接続します。

これには、次の手順を実行します。

1. 左側のウィンドウで右クリック **、HYPER-V Manager**します。
1. クリックして**サーバーに接続する**します。
1. IP アドレスを入力、**別のコンピューター**テキスト フィールド。

>[!NOTE]
> これは、Windows Server 2016 または Windows 10 の機能のみ**リモート**ホスト。

### <a name="connect-to-a-windows-2016-or-windows-10-remote-host-outside-your-domain-or-with-no-domain"></a>Windows 2016 または Windows 10 リモート ホストまたはドメインなしで、ドメインの外部に接続します。

これには、次の手順を実行します。

1. 管理対象 HYPER-V ホストで、管理者として Windows PowerShell セッションを開きます。

1. プライベート ネットワーク ゾーンに必要なファイアウォール規則を作成します。   
   
   ```
   Enable-PSRemoting
   ```

2. パブリック ゾーンでのリモート アクセスを許可するのには、CredSSP および WinRM のファイアウォール規則を有効にします。
  
   ```
   Enable-WSManCredSSP -Role server
   ```

    詳細については、次を参照してください。 [Enable-psremoting](https://technet.microsoft.com/library/hh849694.aspx)と[Enable-wsmancredssp](https://technet.microsoft.com/library/hh849872.aspx)します。

次に、HYPER-V ホストの管理を使用するコンピューターを構成します。

1. 管理者として Windows PowerShell セッションを開きます。
1. これらのコマンドを実行します。

     ```
     Set-Item WSMan:\localhost\Client\TrustedHosts -Value "fqdn-of-hyper-v-host"
     ```
     ```
     Enable-WSManCredSSP -Role client -DelegateComputer "fqdn-of-hyper-v-host"
     ```
1. また、次のグループ ポリシーを構成する必要があります。 
    * **コンピューターの構成** \> **管理用テンプレート** \> **システム** \> **資格情報の委任** \> **NTLM のみのサーバー認証で新しい資格情報の委任を許可します。**
    * をクリックして**を有効にする**追加*wsman/fqdn からのハイパー-v-ホスト*します。
1. 開いている**Hyper V マネージャー**します。
1. 左側のウィンドウで右クリック **、HYPER-V Manager**します。
1. クリックして**サーバーに接続する**します。

>[!NOTE]
> これは、Windows Server 2016 または Windows 10 の機能のみ**リモート**ホスト。

コマンドレットの詳細は、次を参照してください。 [Set-item](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/set-item)と[Enable-wsmancredssp](https://technet.microsoft.com/library/hh849872.aspx)します。

## <a name="install-hyper-v-manager"></a>Hyper V マネージャーをインストールします。

UI ツールを使用するには、HYPER-V マネージャーを実行するコンピューターのオペレーティング システムに適したものを選択します。

Windows Server で、サーバー マネージャーを開き\>**管理** \> **役割と機能の追加**します。 移動、**機能**ページし、展開**リモート サーバー管理ツール** \> **役割管理ツール** \> **HYPER-V 管理ツール**します。 

Windows、HYPER-V マネージャーがで使用できる[任意の Windows オペレーティング システム、HYPER-V を含む](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_compatibility)します。

1. Windows デスクトップで [スタート] ボタンをクリックして入力を開始**プログラムと機能**します。 
1. 検索結果でクリックして**プログラムと機能**します。
1. 左側のウィンドウで次のようにクリックします。**オンまたはオフにする Windows 機能**します。
1. HYPER-V のフォルダーを展開し、 **HYPER-V 管理ツール をクリックして**。
1. HYPER-V Manager をインストールする をクリックして**HYPER-V 管理ツール**します。 また、HYPER-V モジュールをインストールする場合は、そのオプションをクリックします。

Windows PowerShell を使用するには、管理者として、次のコマンドを実行します。

```
add-windowsfeature rsat-hyper-v-tools
```

## <a name="see-also"></a>関連項目  
 
[HYPER-V をインストールします。](..\get-started\Install-the-Hyper-V-role-on-Windows-Server.md) 

