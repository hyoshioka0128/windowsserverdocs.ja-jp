---
title: HYPER-V の第 2 世代仮想マシンのセキュリティ設定
description: 第 2 世代仮想マシンの HYPER-V マネージャーで使用できるセキュリティ設定について説明します
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 06ab4f5f-6b8e-4058-8108-76785aa93d4c
author: larsiwer
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 90a2b7234ee55d8469b6e02ba3de3a0efc080a3e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889503"
---
# <a name="generation-2-virtual-machine-security-settings-for-hyper-v"></a>HYPER-V の第 2 世代仮想マシンのセキュリティ設定

>適用先:Windows Server 2016、Microsoft HYPER-V Server 2016、Windows Server 2019、Microsoft HYPER-V Server 2019

データと仮想マシンの状態を保護するために、HYPER-V マネージャーで仮想マシンのセキュリティ設定を使用します。 仮想マシンは、検査、盗難、およびホスト、およびデータ センターの管理者で実行される可能性があるマルウェアの両方から改ざんから保護できます。 取得するセキュリティのレベルが、仮想マシンの世代を実行するホスト ハードウェアに依存し、シールドされた仮想マシンを開始するホストを承認する、ホスト ガーディアン サービスと呼ばれる、サービスを設定するかどうか。  

ホスト ガーディアン サービスは、Windows Server 2016 で新しいロールです。 正当な HYPER-V ホストを識別し、指定された仮想マシンを実行することができます。 データ センターのホスト ガーディアン サービスを設定すると最も一般的です。 ホスト ガーディアン サービスをセットアップすることがなくローカルで実行するシールドされた仮想マシンを作成することができます。 ホスト ガーディアンのファブリックにシールドされた仮想マシンを後で配布できます。  

ホスト ガーディアン サービスを設定していないか実行しているローカル モードでの HYPER-V ホストとホストにバーチャル マシンの所有者のガーディアン キー場合、は、このトピックで説明する設定を変更できます。   ガーディアン キーの所有者を作成する組織がそのキーを持つすべての仮想マシンを所有する、プライベートまたはパブリック キーが作成された共有します。  

作成する方法、仮想マシン、ホスト ガーディアン サービスのセキュリティを強化については、次のリソースを参照してください。  

- [ファブリックを強化します。HYPER-V (Ignite ビデオ) でテナントのシークレットを保護します。](https://go.microsoft.com/fwlink/?LinkId=746379)
- [保護されたファブリックとシールドされた Vm](https://go.microsoft.com/fwlink/?LinkId=746381)

## <a name="secure-boot-setting-in-hyper-v-manager"></a>HYPER-V マネージャーでのブート設定をセキュリティで保護します。  

セキュア ブートは、利用して、承認されていないファームウェア、オペレーティング システム、または Unified Extensible Firmware Interface (UEFI) ドライバー (オプション Rom とも呼ばれます) がブート時に実行されていることを防止する機能が第 2 世代仮想マシンで利用可能です。 セキュア ブートが既定で有効にします。 セキュア ブートは、Windows または Linux のディストリビューションのオペレーティング システムを実行する第 2 世代仮想マシンで使用できます。  

次の表で説明したテンプレートは、ブート プロセスの整合性を検証する必要のある証明書を参照してください。  

|テンプレート名|説明|  
|-----------------|---------------|  
|Microsoft Windows|セキュア ブートには、Windows オペレーティング システム用の仮想マシンを選択します。|  
|Microsoft UEFI 証明機関|セキュア ブートには、Linux ディストリビューションのオペレーティング システム用の仮想マシンを選択します。|  
|オープン ソースのシールドされた VM|このテンプレートを活用すると、セキュア ブートを[シールドされた Vm の Linux ベース](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-create-a-linux-shielded-vm-template)します。|

詳しくは、次のトピックをご覧ください。  

- [Windows 10 のセキュリティの概要](https://docs.microsoft.com/windows/security/threat-protection/overview-of-threat-mitigations-in-windows-10)  
- [HYPER-V にジェネレーション 1 または 2 仮想マシンを作成する必要があります。](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)  
- [Linux および FreeBSD Virtual Machines on Hyper-v の概要](../Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)  

## <a name="encryption-support-settings-in-hyper-v-manager"></a>HYPER-V マネージャーでの暗号化のサポートの設定

次の暗号化のサポート オプションを選択してデータと、仮想マシンの状態を保護に役立てることができます。  

- **トラステッド プラットフォーム モジュールを有効にする**-この設定により、仮想化されたトラステッド プラットフォーム モジュール (TPM) チップが、仮想マシンで使用可能です。 これにより、BitLocker を使用して仮想マシンのディスクを暗号化するゲストができます。
  - HYPER-V ホストが Windows 10 1511 を実行中の場合は、分離ユーザー モードを有効にする必要です。 
- **状態と VM の移行のトラフィックを暗号化する**- 仮想マシンの保存された状態を暗号化し、ライブ マイグレーション トラフィック。

### <a name="enable-isolated-user-mode"></a>分離ユーザー モードを有効にします。

選択した場合**トラステッド プラットフォーム モジュールを有効にする**、Windows 10 Anniversary Update より前のバージョンの Windows を実行する HYPER-V ホストで分離ユーザー モードを有効にする必要があります。 こうと、HYPER-V がその実行の Windows Server 2016 または Windows 10 Anniversary Update をホストする必要はありませんまたはそれ以降。

分離ユーザー モードは、仮想保護モード内で HYPER-V ホスト上のセキュリティ アプリケーションをホストするランタイム環境です。 仮想保護モードは、セキュリティで保護し、仮想 TPM チップの状態を保護するために使用されます。  

以前のバージョンの Windows 10 を実行する HYPER-V ホストを分離ユーザー モードを有効にするには  

1.  管理者として Windows PowerShell を開きます。  

2.  次のコマンドを実行します。  

    ```  
    Enable-WindowsOptionalFeature -Feature IsolatedUserMode -Online  
    New-Item -Path HKLM:\SYSTEM\CurrentControlSet\Control\DeviceGuard -Force  
    New-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Control\DeviceGuard -Name EnableVirtualizationBasedSecurity -Value 1 -PropertyType DWord -Force  

    ```  

仮想マシンを移行するには Windows Server 2016 を実行している任意のホストに有効になっている仮想 tpm を装備した、Windows 10 ビルド 10586 以降のバージョン。 開始することがありますできませんを別のホストに移行する場合。 仮想マシンを実行する新しいホストを承認するためにその仮想マシンのキー プロテクターを更新する必要があります。 詳細については、次を参照してください。[保護されたファブリックとシールドされた Vm](https://go.microsoft.com/fwlink/?LinkId=746381)と[Windows server、Hyper-v のシステム要件](../System-requirements-for-Hyper-V-on-Windows.md)します。  

## <a name="security-policy-in-hyper-v-manager"></a>HYPER-V マネージャーでのセキュリティ ポリシー  
複数の仮想マシンのセキュリティを使用して、**シールドを有効にする**コンソール接続や PowerShell ダイレクトでは、いくつかの統合コンポーネントなどの管理機能を無効にするオプション。 このオプションを選択した場合**セキュア ブート**、**トラステッド プラットフォーム モジュールを有効にする**、および**暗号化の状態と VM の移行のトラフィック**オプションが選択され、適用します。   

ホスト ガーディアン サービスをセットアップすることがなく、シールドされた仮想マシンをローカルに実行できます。 開始することがありますできませんを別のホストに移行する場合。 仮想マシンを実行する新しいホストを承認するためにその仮想マシンのキー プロテクターを更新する必要があります。 詳細については、「[保護されたファブリックとシールドされた VM](https://go.microsoft.com/fwlink/?LinkId=746381)」を参照してください。  

Windows Server のセキュリティの詳細については、次を参照してください。[セキュリティおよび保証](../../../security/Security-and-Assurance.md)します。  
