---
title: Hyper-v の第2世代仮想マシンのセキュリティ設定
description: 第2世代仮想マシンの Hyper-v マネージャーで使用できるセキュリティ設定について説明します。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 06ab4f5f-6b8e-4058-8108-76785aa93d4c
author: larsiwer
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 82544a58a8d46b3063605557be3c63cfa799e4fb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364243"
---
# <a name="generation-2-virtual-machine-security-settings-for-hyper-v"></a>Hyper-v の第2世代仮想マシンのセキュリティ設定

>適用先:Windows Server 2016、Microsoft Hyper-V Server 2016、Windows Server 2019、Microsoft Hyper-V Server 2019

Hyper-v マネージャーの仮想マシンのセキュリティ設定を使用して、仮想マシンのデータと状態を保護します。 バーチャルマシンは、ホスト上で実行される可能性のあるマルウェアとデータセンター管理者の両方で、検査、盗難、改ざんを防ぐことができます。 取得するセキュリティのレベルは、実行するホストハードウェア、バーチャルマシンの世代、およびホストガーディアンサービスと呼ばれるサービスを設定するかどうかによって決まります。このサービスは、ホストがシールドされたバーチャルマシンを起動するのを承認します。  

ホストガーディアンサービスは、Windows Server 2016 の新しい役割です。 正当な Hyper-v ホストを識別し、特定のバーチャルマシンを実行できるようにします。 最も一般的には、データセンターのホストガーディアンサービスを設定します。 ただし、ホストガーディアンサービスを設定せずに、シールドされた仮想マシンをローカルで実行するように作成することもできます。 後で、シールドされたバーチャルマシンをホストガーディアンファブリックに配布できます。  

ホストガーディアンサービスを設定していない場合、または Hyper-v ホストでローカルモードで実行していて、ホストにバーチャルマシン所有者のガーディアンキーがある場合は、このトピックで説明する設定を変更できます。   ガーディアンキーの所有者は、秘密キーまたは公開キーを作成して共有し、そのキーで作成されたすべての仮想マシンを所有する組織です。  

ホストガーディアンサービスを使用して仮想マシンのセキュリティを強化する方法については、次のリソースを参照してください。  

- [ファブリックの強化: Hyper-v でのテナントシークレットの保護 (Ignite ビデオ) ](https://go.microsoft.com/fwlink/?LinkId=746379)
- [保護されたファブリックとシールドされた Vm](https://go.microsoft.com/fwlink/?LinkId=746381)

## <a name="secure-boot-setting-in-hyper-v-manager"></a>Hyper-v マネージャーでのセキュアブート設定  

セキュアブートは、第2世代仮想マシンで使用可能な機能であり、許可されていないファームウェア、オペレーティングシステム、または Unified Extensible Firmware Interface (UEFI) ドライバー (オプション Rom とも呼ばれます) が起動時に実行されるのを防ぐのに役立ちます。 セキュアブートは既定で有効になっています。 Windows または Linux ディストリビューションのオペレーティングシステムを実行する第2世代仮想マシンでセキュアブートを使用できます。  

次の表に示すテンプレートは、ブートプロセスの整合性を確認するために必要な証明書を示しています。  

|テンプレート名|説明|  
|-----------------|---------------|  
|Microsoft Windows|Windows オペレーティングシステムの仮想マシンをセキュアブートする場合に選択します。|  
|Microsoft UEFI 証明機関|Linux ディストリビューションオペレーティングシステム用の仮想マシンをセキュアブートする場合に選択します。|  
|オープンソースのシールドされた VM|このテンプレートは[、Linux ベースのシールド](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-create-a-linux-shielded-vm-template)された vm のブートをセキュリティで保護するために活用されています。|

詳しくは、次のトピックをご覧ください。  

- [Windows 10 セキュリティの概要](https://docs.microsoft.com/windows/security/threat-protection/overview-of-threat-mitigations-in-windows-10)  
- [Hyper-v に第1世代または第2世代の仮想マシンを作成する必要がありますか。](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)  
- [Hyper-v 上の Linux および FreeBSD Virtual Machines](../Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)  

## <a name="encryption-support-settings-in-hyper-v-manager"></a>Hyper-v マネージャーでの暗号化サポートの設定

次の暗号化サポートオプションを選択することで、仮想マシンのデータと状態を保護することができます。  

- **トラステッドプラットフォームモジュールを有効に**する-仮想マシンで仮想化されたトラステッドプラットフォームモジュール (TPM) チップを使用できるようにします。 これにより、ゲストは BitLocker を使用して仮想マシンディスクを暗号化することができます。
  - Hyper-v ホストが Windows 10 1511 を実行している場合は、分離ユーザーモードを有効にする必要があります。 
- **状態と VM の移行トラフィックを暗号化**する-仮想マシンの保存された状態とライブマイグレーションのトラフィックを暗号化します。

### <a name="enable-isolated-user-mode"></a>分離ユーザーモードを有効にする

Windows 10 記念日更新より前のバージョンの Windows を実行している Hyper-v ホストで [**トラステッドプラットフォームモジュールを有効**にする] を選択した場合は、分離ユーザーモードを有効にする必要があります。 これは、Windows Server 2016 または Windows 10 周年更新プログラム以降を実行する Hyper-v ホストに対しては必要ありません。

分離ユーザーモードは、Hyper-v ホスト上の仮想保護モードでセキュリティアプリケーションをホストするランタイム環境です。 仮想保護モードは、仮想 TPM チップの状態を保護および保護するために使用されます。  

以前のバージョンの Windows 10 を実行する Hyper-v ホストで分離ユーザーモードを有効にするには、  

1.  管理者として Windows PowerShell を開きます。  

2.  次のコマンドを実行します。  

    ```  
    Enable-WindowsOptionalFeature -Feature IsolatedUserMode -Online  
    New-Item -Path HKLM:\SYSTEM\CurrentControlSet\Control\DeviceGuard -Force  
    New-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Control\DeviceGuard -Name EnableVirtualizationBasedSecurity -Value 1 -PropertyType DWord -Force  

    ```  

仮想 TPM が有効になっている仮想マシンを、Windows Server 2016、Windows 10 ビルド10586以降のバージョンを実行している任意のホストに移行することができます。 ただし、別のホストに移行する場合は、起動できないことがあります。 バーチャルマシンを実行する新しいホストを承認するには、そのバーチャルマシンのキープロテクターを更新する必要があります。 詳細については、「保護された[ファブリックとシールド](https://go.microsoft.com/fwlink/?LinkId=746381)された vm」および「 [Windows Server 上の hyper-v のシステム要件](../System-requirements-for-Hyper-V-on-Windows.md)」を参照してください。  

## <a name="security-policy-in-hyper-v-manager"></a>Hyper-v マネージャーのセキュリティポリシー  
仮想マシンのセキュリティを強化するには、[**シールドを有効**にする] オプションを使用して、コンソール接続、PowerShell Direct、一部の統合コンポーネントなどの管理機能を無効にします。 このオプションを選択すると、 **[セキュアブート]** 、 **[トラステッドプラットフォームモジュールを有効に]** する、 **[暗号化の状態と VM の移行のトラフィック]** オプションが選択され、適用されます。   

ホストガーディアンサービスを設定せずに、シールドされた仮想マシンをローカルで実行することができます。 ただし、別のホストに移行する場合は、起動できないことがあります。 バーチャルマシンを実行する新しいホストを承認するには、そのバーチャルマシンのキープロテクターを更新する必要があります。 詳細については、「[保護されたファブリックとシールドされた VM](https://go.microsoft.com/fwlink/?LinkId=746381)」を参照してください。  

Windows Server のセキュリティの詳細については、「[セキュリティと保証](../../../security/Security-and-Assurance.md)」を参照してください。  
