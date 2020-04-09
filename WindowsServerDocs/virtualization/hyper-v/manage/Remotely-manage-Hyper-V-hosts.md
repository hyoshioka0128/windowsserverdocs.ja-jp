---
title: Hyper-v ホストのリモート管理
description: Hyper-v ホストと Hyper-v マネージャーの間のバージョンの互換性について説明します。また、クロスドメインやスタンドアロンを含むさまざまな環境でリモートホストに接続する方法についても説明します。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: 2d34e98c-6134-479b-8000-3eb360b8b8a3
author: kbdazure
ms.author: kathydav
ms.date: 12/06/2016
ms.openlocfilehash: 592bb6352c4ca56770e1a3051ecbc88d9d378467
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859415"
---
# <a name="remotely-manage-hyper-v-hosts-with-hyper-v-manager"></a>Hyper-v マネージャーを使用して Hyper-v ホストをリモートで管理する

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows 10、Windows 8.1

この記事では、Hyper-v ホストと Hyper-v マネージャーバージョンのサポートされる組み合わせの一覧を示し、リモートおよびローカルの Hyper-v ホストに接続して管理できるようにする方法について説明します。 

Hyper-v マネージャーでは、リモートとローカルの両方で、少数の Hyper-v ホストを管理できます。 Hyper-v 管理ツールをインストールするとインストールされます。 hyper-v 管理ツールは、hyper-v の完全インストールまたはツールのみのインストールのいずれかを使用して実行できます。 ツールのみのインストールを実行すると、ハードウェア要件を満たしていないコンピューターのツールを使用して Hyper-v をホストできます。 Hyper-v ホストのハードウェアの詳細については、「[システム要件](../System-requirements-for-Hyper-V-on-Windows.md)」を参照してください。

Hyper-v マネージャーがインストールされていない場合は、以下の[手順](#install-hyper-v-manager)を参照してください。

## <a name="supported-combinations-of-hyper-v-manager-and-hyper-v-host-versions"></a>Hyper-v マネージャーと Hyper-v ホストのバージョンのサポートされる組み合わせ

場合によっては、表に示すように、ホスト上の Hyper-v のバージョンとは異なるバージョンの Hyper-v マネージャーを使用できます。 この操作を行うと、管理しているホスト上の hyper-v のバージョンで使用できる機能が Hyper-v マネージャーによって提供されます。 たとえば、windows server 2012 R2 で hyper-v マネージャーのバージョンを使用して、Windows Server 2012 で Hyper-v を実行しているホストをリモートで管理している場合、その Hyper-v ホスト上の Windows Server 2012 R2 で利用可能な機能を使用することはできません。

次の表に、特定のバージョンの Hyper-v マネージャーから管理できる Hyper-v ホストのバージョンを示します。 サポートされているオペレーティングシステムのバージョンのみが一覧表示されます。 特定のオペレーティングシステムバージョンのサポート状態の詳細については、 [Microsoft ライフサイクルポリシー](https://support.microsoft.com/lifecycle)ページの **[Product ライフサイクルの検索]** ボタンを使用してください。 一般に、以前のバージョンの Hyper-v マネージャーでは、同じバージョンまたは同等の Windows Server バージョンを実行している Hyper-v ホストのみを管理できます。

|Hyper-v マネージャーのバージョン | Hyper-v ホストのバージョン|
|---|---|
|Windows 2016、Windows 10|-Windows Server 2016-Nano Server を含むすべてのエディションとインストールオプション、および対応するバージョンの Hyper-v Server <br>-Windows Server 2012 R2-すべてのエディションとインストールオプション、および対応するバージョンの Hyper-v Server <br>-Windows Server 2012-すべてのエディションとインストールオプション、および対応するバージョンの Hyper-v Server <br> -Windows 10 <br> -Windows 8.1  |
| Windows Server 2012 R2、Windows 8.1 | -Windows Server 2012 R2-すべてのエディションとインストールオプション、および対応するバージョンの Hyper-v Server <br>-Windows Server 2012-すべてのエディションとインストールオプション、および対応するバージョンの Hyper-v Server <br>-Windows 8.1
| Windows Server 2012 | -Windows Server 2012-すべてのエディションとインストールオプション、および対応するバージョンの Hyper-v Server
| Windows Server 2008 R2 Service Pack 1、Windows 7 Service Pack 1 | -Windows Server 2008 R2-すべてのエディションとインストールオプション、および対応するバージョンの Hyper-v Server
| Windows Server 2008、Windows Vista Service Pack 2 | -Windows Server 2008-すべてのエディションとインストールオプション、および対応するバージョンの Hyper-v Server

>[!NOTE]
>Service pack のサポートは、2016年1月12日の Windows 8 で終了しました。 詳細については、 [Windows 8.1](https://support.microsoft.com/help/18581)に関する FAQ を参照してください。

## <a name="connect-to-a-hyper-v-host"></a>Hyper-v ホストに接続する

Hyper-v マネージャーから hyper-v ホストに接続するには、左側のウィンドウで **[Hyper-v マネージャー]** を右クリックし、 **[サーバーへの接続]** をクリックします。

## <a name="manage-hyper-v-on-a-local-computer"></a>ローカルコンピューターで Hyper-v を管理する

Hyper-v マネージャーには、ローカルコンピューターを含むコンピューターを追加するまで、Hyper-v をホストしているコンピューターは表示されません。 これを行うには :

1. 左側のウィンドウで、 **[Hyper-v マネージャー]** を右クリックします。
2. [**サーバーへの接続] を**クリックします。
3. **[コンピューターの選択]** で、 **[ローカルコンピューター]** をクリックし、 **[OK]** をクリックします。

接続できない場合:

* Hyper-v ツールのみがインストールされている可能性があります。 Hyper-v プラットフォームがインストールされていることを確認するには、仮想マシン管理サービスを探します。 または、サービスデスクトップアプリを開きます。 **[スタート]** ボタンをクリックし、 **[検索の開始]** ボックスをクリックして「 **services.msc**」と入力し、 **enter キーを**押します。 バーチャルマシン管理サービスが一覧に表示されない場合は、「 [hyper-v のインストール](../get-started/Install-the-Hyper-V-role-on-Windows-Server.md)」の手順に従って、hyper-v プラットフォームをインストールします。
* ハードウェアが要件を満たしていることを確認します。 「[システム要件](../System-requirements-for-Hyper-V-on-Windows.md)」を参照してください。
* ユーザーアカウントが Administrators グループまたは Hyper-v Administrators グループに属していることを確認します。

## <a name="manage-hyper-v-hosts-remotely"></a>Hyper-v ホストをリモートで管理する  

リモートの Hyper-v ホストを管理するには、ローカルコンピューターとリモートホストの両方でリモート管理を有効にします。

Windows Server でサーバーマネージャー \>**ローカルサーバー** \>**リモート管理** を開き、**このコンピューターへのリモート接続を許可する** をクリックします。 

または、いずれかのオペレーティングシステムで、管理者として Windows PowerShell を開き、次を実行します。 

```
Enable-PSRemoting
```

### <a name="connect-to-hosts-in-the-same-domain"></a>同じドメイン内のホストに接続する

Windows 8.1 以前では、リモート管理は、ホストが同じドメイン内にあり、ローカルユーザーアカウントがリモートホスト上にもある場合にのみ機能します。

リモート Hyper-v ホストを Hyper-v マネージャーに追加するには、 **[コンピューターの選択**] ダイアログボックスで **[別のコンピューター]** を選択し、リモートホストのホスト名、NetBIOS 名、または完全修飾ドメイン名 \(FQDN\)を入力します。

Windows Server 2016 と Windows 10 の hyper-v マネージャーでは、以前のバージョンよりも多くの種類のリモート接続が提供されます。詳細については、次のセクションで説明します。  

### <a name="connect-to-a-windows-2016-or-windows-10-remote-host-as-a-different-user"></a>別のユーザーとして Windows 2016 または Windows 10 リモートホストに接続する

これにより、hyper-v ホスト上の Hyper-v Administrators グループまたは Administrators グループのメンバーであるユーザーとしてローカルコンピューター上で実行されていない場合に、Hyper-v ホストに接続できます。 これを行うには :

1. 左側のウィンドウで、 **[Hyper-v マネージャー]** を右クリックします。
1. [**サーバーへの接続] を**クリックします。
1. **[コンピューターの選択]** ダイアログボックスで **[別のユーザーとして接続]** する を選択します。
1. **[ユーザーの設定]** を選択します。

>[!NOTE]
> これは、Windows Server 2016 または Windows 10**リモート**ホストに対してのみ機能します。

### <a name="connect-to-a-windows-2016-or-windows-10-remote-host-using-ip-address"></a>IP アドレスを使用して Windows 2016 または Windows 10 リモートホストに接続する

これを行うには :

1. 左側のウィンドウで、 **[Hyper-v マネージャー]** を右クリックします。
1. [**サーバーへの接続] を**クリックします。
1. **[別のコンピューター]** テキストフィールドに IP アドレスを入力します。

>[!NOTE]
> これは、Windows Server 2016 または Windows 10**リモート**ホストに対してのみ機能します。

### <a name="connect-to-a-windows-2016-or-windows-10-remote-host-outside-your-domain-or-with-no-domain"></a>ドメインの外部またはドメインなしで Windows 2016 または Windows 10 リモートホストに接続する

これを行うには :

1. 管理対象の Hyper-v ホストで、管理者として Windows PowerShell セッションを開きます。

1. プライベートネットワークゾーンに必要なファイアウォール規則を作成します。   
   
   ```
   Enable-PSRemoting
   ```

2. パブリックゾーンでのリモートアクセスを許可するには、CredSSP および WinRM のファイアウォール規則を有効にします。
  
   ```
   Enable-WSManCredSSP -Role server
   ```

    詳細については、 [enable-psremoting](https://technet.microsoft.com/library/hh849694.aspx)と[enable-wsmancredssp](https://technet.microsoft.com/library/hh849872.aspx)を参照してください。

次に、Hyper-v ホストの管理に使用するコンピューターを構成します。

1. 管理者として Windows PowerShell セッションを開きます。
1. 次のコマンドを実行します。

     ```
     Set-Item WSMan:\localhost\Client\TrustedHosts -Value "fqdn-of-hyper-v-host"
     ```
     ```
     Enable-WSManCredSSP -Role client -DelegateComputer "fqdn-of-hyper-v-host"
     ```
1. また、次のグループポリシーを構成する必要がある場合もあります。 
    * **コンピューターの構成**\>**管理用テンプレート**\>**システム**\>**資格情報の委任**\> **NTLM のみのサーバー認証で新しい資格情報を委任でき**ます
    * **[有効化]** をクリックし、 *wsman/fqdn*を追加します。
1. **Hyper-v マネージャー**を開きます。
1. 左側のウィンドウで、 **[Hyper-v マネージャー]** を右クリックします。
1. [**サーバーへの接続] を**クリックします。

>[!NOTE]
> これは、Windows Server 2016 または Windows 10**リモート**ホストに対してのみ機能します。

コマンドレットの詳細については、「 [Set-Item](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/set-item) and [enable-wsmancredssp](https://technet.microsoft.com/library/hh849872.aspx)」を参照してください。

## <a name="install-hyper-v-manager"></a>Hyper-v マネージャーをインストールする

UI ツールを使用するには、Hyper-v マネージャーを実行するコンピューターのオペレーティングシステムに適したものを選択します。

Windows Server でサーバーマネージャーを開き、**役割と機能の追加**\> \>**管理**します。 **[機能]** ページに移動し、 **[リモートサーバー管理ツール]** \> [**役割管理 \> ツール**]、 **[hyper-v 管理ツール]** の順に展開します。 

Windows では、hyper-v マネージャーは、 [hyper-v を含むすべての windows オペレーティングシステム](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_compatibility)で使用できます。

1. Windows デスクトップで スタート ボタンをクリックし、**プログラムと機能** の入力を開始します。 
1. 検索結果 で、**プログラムと機能** をクリックします。
1. 左側のウィンドウで、 **[Windows の機能の有効化または無効化]** をクリックします。
1. Hyper-v フォルダーを展開し、 **[Hyper-v 管理ツール] をクリック**します。
1. Hyper-v マネージャーをインストールするには、 **[Hyper-v 管理ツール]** をクリックします。 Hyper-v モジュールもインストールする場合は、このオプションをクリックします。

Windows PowerShell を使用するには、管理者として次のコマンドを実行します。

```
add-windowsfeature rsat-hyper-v-tools
```

## <a name="see-also"></a>参照  
 
[Hyper-V をインストールする](../get-started/Install-the-Hyper-V-role-on-Windows-Server.md) 

