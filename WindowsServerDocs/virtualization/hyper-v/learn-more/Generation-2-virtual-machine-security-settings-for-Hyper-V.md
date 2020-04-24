---
title: Hyper-V の第 2 世代仮想マシンのセキュリティ設定
description: 第 2 世代仮想マシン向けに Hyper-V マネージャーで使用できるセキュリティ設定について説明します
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: 06ab4f5f-6b8e-4058-8108-76785aa93d4c
author: larsiwer
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 7eb867529d38ab21ee21c19f92c89ed4128b0ea4
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "80860805"
---
# <a name="generation-2-virtual-machine-security-settings-for-hyper-v"></a>Hyper-V の第 2 世代仮想マシンのセキュリティ設定

>適用先:Windows Server 2016、Microsoft Hyper-V Server 2016、Windows Server 2019、Microsoft Hyper-V Server 2019

仮想マシンのデータおよび状態の保護を促進するには、Hyper-V マネージャー内の仮想マシンのセキュリティ設定を使用します。 ホスト上で実行される可能性のあるマルウェアとデータセンター管理者の両方による閲覧、盗難、改ざんから仮想マシンを保護できます。 得られるセキュリティのレベルは、実行するホスト ハードウェア、仮想マシンの世代、およびホスト ガーディアン サービス (シールドされた仮想マシンの起動することをホストの承認により許可するサービス) を設定するかどうかによって決まります。  

ホスト ガーディアン サービスは、Windows Server 2016 の新しい役割です。 これは、正当な Hyper-V ホストを識別し、それらが特定の仮想マシンを実行することを許可します。 ホスト ガーディアン サービスを設定する例として最も一般的なのはデータセンターです。 ただし、ホスト ガーディアン サービスを設定せずに、シールドされた仮想マシンを作成してローカルで実行することができます。 シールドされた仮想マシンは、後でホスト ガーディアン ファブリックに割り振ることができます。  

ホスト ガーディアン サービスが、未設定の場合、または仮想マシン所有者のガーディアン キーが存在する Hyper-V ホスト上でローカル モードで実行されている場合は、このトピックで説明する設定を変更できます。   ガーディアン キーの所有者は、秘密キーまたは公開キーを作成して共有し、そのキーを使用して作成されたすべての仮想マシンを所有する組織です。  

ホスト ガーディアン サービスを使用して仮想マシンのセキュリティを強化する方法については、次のリソースを参照してください。  

- [ファブリックの強化: Hyper-V のテナントの機密情報を保護する (Ignite ビデオ)](https://go.microsoft.com/fwlink/?LinkId=746379)
- [保護されたファブリックとシールドされた VM](https://go.microsoft.com/fwlink/?LinkId=746381)

## <a name="secure-boot-setting-in-hyper-v-manager"></a>Hyper-V マネージャーでのセキュア ブートの設定  

セキュア ブートは、第 2 世代仮想マシンで使用できる機能です。これにより、無許可のファームウェア、オペレーティング システム、または Unified Extensible Firmware Interface (UEFI) ドライバー (オプション ROM とも呼ばれます) が起動時に実行されないようにします。 セキュア ブートは既定で有効になっています。 Windows または Linux ディストリビューションのオペレーティング システムが実行されている第 2 世代仮想マシンでセキュア ブートを使用できます。  

次の表に記載されているテンプレートは、ブート プロセスの整合性を検証するために必要な証明書を示しています。  

|テンプレート名|説明|  
|-----------------|---------------|  
|Microsoft Windows|Windows オペレーティング システムの仮想マシンのセキュア ブートを有効にする場合に選択します。|  
|Microsoft UEFI 証明機関|Linux ディストリビューションのオペレーティング システムの仮想マシンのセキュア ブートを有効にする場合に選択します。|  
|オープン ソースのシールドされた VM|このテンプレートは、[Linux ベースのシールドされた VM](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-create-a-linux-shielded-vm-template) のセキュア ブートを有効にする場合に利用します。|

詳しくは、次のトピックをご覧ください。  

- [Windows 10 のセキュリティの概要](https://docs.microsoft.com/windows/security/threat-protection/overview-of-threat-mitigations-in-windows-10)  
- [Hyper-V で第 1 世代または第 2 世代の仮想マシンを作成する必要がありますか](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)  
- [Hyper-V での Linux および FreeBSD の仮想マシン](../Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)  

## <a name="encryption-support-settings-in-hyper-v-manager"></a>Hyper-V マネージャーでの暗号化のサポートの設定

次の暗号化サポート オプションを選択することで、仮想マシンのデータと状態を保護できます。  

- **トラステッド プラットフォーム モジュールを有効にする** - この設定によって、仮想マシンで仮想化されたトラステッド プラットフォーム モジュール (TPM) チップを使用できるようになります。 これにより、ゲストは BitLocker を使用して仮想マシン ディスクを暗号化できます。
  - Hyper-V ホストで Windows 10 1511 が実行されている場合は、分離ユーザー モードを有効にする必要があります。 
- **状態と仮想マシンのマイグレーション トラフィックの暗号化** - 仮想マシンの保存された状態とライブ マイグレーション トラフィックを暗号化します。

### <a name="enable-isolated-user-mode"></a>分離ユーザー モードを有効にする

Windows 10 Anniversary Update より前のバージョンの Windows を実行している Hyper-V ホストで **[トラステッド プラットフォーム モジュールを有効にする]** を選択した場合は、分離ユーザー モードを有効にする必要があります。 Windows Server 2016 または Windows 10 Anniversary Update 以降を実行している Hyper-V ホストの場合は、これを行う必要はありません。

分離ユーザー モードは、Hyper-V ホスト上の仮想保護モード内でセキュリティ アプリケーションをホストするランタイム環境です。 仮想保護モードは、仮想 TPM チップの状態を保護するために使用されます。  

以前のバージョンの Windows 10 を実行している Hyper-V ホストで分離ユーザー モードを有効にするには、  

1.  管理者として Windows PowerShell を開きます。  

2.  次のコマンドを実行します。  

    ```  
    Enable-WindowsOptionalFeature -Feature IsolatedUserMode -Online  
    New-Item -Path HKLM:\SYSTEM\CurrentControlSet\Control\DeviceGuard -Force  
    New-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Control\DeviceGuard -Name EnableVirtualizationBasedSecurity -Value 1 -PropertyType DWord -Force  

    ```  

仮想 TPM が有効になっている仮想マシンは、Windows Server 2016 または Windows 10 ビルド 10586 以降のバージョンを実行しているホストに移行できます。 ただし、別のホストに移行すると、起動できないことがあります。 新しいホストで仮想マシンを実行することを承認するために、その仮想マシンのキーの保護機能を更新する必要があります。 詳細については、「[保護されたファブリックとシールドされた VM](https://go.microsoft.com/fwlink/?LinkId=746381)」および「[Windows Server 上の Hyper-V のシステム要件](../System-requirements-for-Hyper-V-on-Windows.md)」 を参照してください。  

## <a name="security-policy-in-hyper-v-manager"></a>Hyper-V マネージャーのセキュリティ ポリシー  
仮想マシンのセキュリティを向上させるには、 **[Enable Shielding]\(シールドを有効にする\)** オプションを使用して、コンソール接続、PowerShell Direct、一部の統合コンポーネントなどの管理機能を無効にしてください。 このオプションを選択すると、 **[セキュア ブート]** 、 **[トラステッド プラットフォーム モジュールを有効にする]** 、 **[状態と仮想マシンのマイグレーション トラフィックの暗号化]** の各オプションが選択および適用されます。   

ホスト ガーディアン サービスを設定せずに、シールドされた仮想マシンをローカルで実行できます。 ただし、別のホストに移行すると、起動できないことがあります。 新しいホストで仮想マシンを実行することを承認するために、その仮想マシンのキーの保護機能を更新する必要があります。 詳細については、「[保護されたファブリックとシールドされた VM](https://go.microsoft.com/fwlink/?LinkId=746381)」を参照してください。  

Windows Server のセキュリティの詳細については、「[セキュリティおよび保証](../../../security/Security-and-Assurance.md)」を参照してください。  
