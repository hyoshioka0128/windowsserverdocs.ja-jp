---
title: Windows Server での Hyper-v セキュリティの計画
description: Hyper-v ホストと仮想マシンのセキュリティに関する考慮事項の一覧を示します。
ms.prod: windows-server
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: 115db481-b57e-41c3-8354-504f4bc6113a
manager: dongill
author: larsiwer
ms.author: kathydav
ms.date: 08/03/2018
ms.openlocfilehash: 794f36b688c4c65da8b3925a98c91aea8cf74bde
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852885"
---
# <a name="plan-for-hyper-v-security-in-windows-server"></a>Windows Server での Hyper-v セキュリティの計画

>適用対象: Windows Server 2016、Microsoft Hyper-V Server 2016、Windows Server 2019、Microsoft Hyper-V Server 2019

HYPER-V ホストのオペレーティング システム、仮想マシン、構成ファイル、および仮想マシンのデータをセキュリティで保護します。 HYPER-V 環境を保護するためにチェックリストとして次の推奨されるベスト プラクティスの一覧を使用します。

## <a name="secure-the-hyper-v-host"></a>HYPER-V ホストのセキュリティ保護します。
- **ホスト OS のセキュリティを維持します。**
    - 管理オペレーティング システムに必要な最低限の Windows Server インストール オプションを使用して、攻撃対象領域を最小限に抑えます。 詳細については、Windows Server テクニカルコンテンツライブラリの[インストールオプション](/windows-server/windows-server#installation-options)に関するセクションを参照してください。 Windows 10 では、HYPER-V では、実稼働ワークロードを実行することは推奨されません。
    - HYPER-V ホストのオペレーティング システム、ファームウェア、およびデバイス ドライバーは最新のセキュリティ更新プログラムを最新のしてください。 ファームウェアとドライバーを更新する、ベンダーの推奨事項を確認してください。
    - HYPER-V ホストをワークステーションとして使用したり、不要なソフトウェアをインストールしないでください。
    - HYPER-V ホストをリモートで管理します。 ローカル HYPER-V ホストを管理する必要があります、資格情報の保護を使用します。 詳細については、次を参照してください。 [派生した資格情報 Guard でのドメイン資格情報を保護する](https://docs.microsoft.com/windows/access-protection/credential-guard/credential-guard)です。
    - コード整合性ポリシーを有効にします。 仮想化ベースのセキュリティを使用するには、サービスのコードの整合性が保護されています。 詳細については、次を参照してください。 [デバイス ガード展開ガイド](https://docs.microsoft.com/windows/device-security/device-guard/device-guard-deployment-guide)します。
- **セキュリティで保護されたネットワークを使用します。**
    - 物理的な HYPER-V コンピューターの専用のネットワーク アダプターで別のネットワークを使用します。
    - VM のアクセスの構成および仮想ハード ディスク ファイルへのプライベートまたはセキュリティで保護されたネットワークを使用します。
    - ライブ マイグレーション トラフィック/専用のプライベート ネットワークを使用します。 暗号化を使用し、移行中にネットワーク経由で仮想マシンのデータをセキュリティで保護するには、このネットワーク上の IPSec を有効にしてください。 詳細については、次を参照してください。 [フェールオーバー クラスタ リングのないライブ マイグレーションのためのホスト設定](../deploy/set-up-hosts-for-live-migration-without-failover-clustering.md)します。
- **ストレージ移行のトラフィックをセキュリティで保護します。** 

    SMB データとデータ保護の改ざんまたは信頼されていないネットワークの盗聴のエンド ツー エンドの暗号化の SMB 3.0 を使用します。 中間の攻撃を防ぐための SMB 共有の内容にアクセスするのにには、プライベート ネットワークを使用します。 詳細については、次を参照してください。 [SMB のセキュリティの強化](https://technet.microsoft.com/library/dn551363.aspx)します。 
- **保護されたファブリックの一部となるようにホストを構成します。** 

    詳細については、次を参照してください。 [保護され、fabric](../../../security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms-top-node.md)します。
- **デバイスをセキュリティで保護する。** 

    仮想マシンのリソース ファイルを保存する記憶装置をセキュリティで保護します。
    
- **ハードドライブをセキュリティで保護します。** 

    リソースを保護するのにには、BitLocker ドライブ暗号化を使用します。
    
- **Hyper-v ホストのオペレーティングシステムを強化します。** 

    ベースライン セキュリティ設定の推奨事項を使用して、 [Windows サーバーのセキュリティ ベースライン](https://docs.microsoft.com/windows/device-security/windows-security-baselines)します。
    
- **適切なアクセス許可を付与します。**
    - HYPER-V administrators グループに HYPER-V ホストを管理する必要があるユーザーを追加します。
    - Hyper-V ホスト オペレーティング システムでは、仮想マシン管理者のアクセス許可を付与しないでください。

- **Hyper-v のウイルス対策の除外とオプションを構成します。**  

    Windows Defender は既に [自動除外](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/configure-server-exclusions-windows-defender-antivirus) ように構成します。 除外リストの詳細については、次を参照してください。 [Hyper-v ホストでのウイルス対策の除外をお勧め](https://support.microsoft.com/kb/3105657)します。 

- **不明な Vhd をマウントしないでください。** これは、ファイル システム レベルの攻撃にホストを公開できます。

- **必要な場合を除き、運用環境での入れ子を有効にしないでください。**

    入れ子を有効にした場合は、仮想マシンでサポートされていないハイパーバイザーを実行しないでください。  

安全な環境向け。

- **トラステッドプラットフォームモジュール (TPM) 2.0 チップを搭載したハードウェアを使用して、保護されたファブリックを設定します。** 

    詳細については、次を参照してください。 [Windows Server 2016 にインストールされた Hyper-v のシステム要件](../system-requirements-for-hyper-v-on-windows.md)します。

## <a name="secure-virtual-machines"></a>セキュリティで保護された仮想マシン
- **サポートされているゲストオペレーティングシステムに対して第2世代仮想マシンを作成します。** 

    詳細については、次を参照してください。 [第 2 世代のセキュリティ設定](../learn-more/Generation-2-virtual-machine-security-settings-for-Hyper-V.md)します。
    
- **セキュアブートを有効にします。** 

    詳細については、次を参照してください。 [第 2 世代のセキュリティ設定](../learn-more/Generation-2-virtual-machine-security-settings-for-Hyper-V.md)します。
    
- **ゲスト OS のセキュリティを維持します。**

    - 運用環境で仮想マシンを有効にする前に、最新のセキュリティ更新プログラムをインストールします。
    - 統合サービスを必要とすることに保ちますサポートされるゲスト オペレーティング システムをインストールします。 サポートされているバージョンの Windows を実行しているゲストの統合サービスの更新プログラムは、Windows Update を通して利用できます。
    - 実行する役割に基づく各仮想マシンで実行されているオペレーティング システムを強化します。 説明されているベースライン セキュリティ設定の推奨事項を使用して、 [Windows セキュリティ ベースライン](https://docs.microsoft.com/windows/device-security/windows-security-baselines)します。
    
- **セキュリティで保護されたネットワークを使用します。** 

    仮想ネットワーク アダプターが正しい仮想スイッチに接続し、適切なセキュリティ設定と制限を適用することを確認してください。
    
- **仮想ハードディスクとスナップショットファイルを安全な場所に保管します。**

- **デバイスをセキュリティで保護する。** 

    仮想マシンにのみ必要なデバイスを構成します。 特定のシナリオに必要な場合を除き、実稼働環境内で個別のデバイスの割り当てを有効にしません。 これを有効にして場合は、信頼できるベンダーからのデバイスのみを公開することを確認してください。 
    
- **ウイルス対策ソフトウェア、構成、ファイアウォールおよび侵入検知ソフトウェア** 仮想マシン ロールに基いて、必要に応じて仮想マシン内で。

- **Windows 10 または Windows Server 2016 以降を実行しているゲストの仮想化ベースのセキュリティを有効にします。** 

    詳細については、次を参照してください。、 [デバイス ガード展開ガイド](https://docs.microsoft.com/windows/device-security/device-guard/device-guard-deployment-guide)します。
    
- **特定のワークロードに必要な場合のみ個別のデバイスの割り当てを有効にする**です。 

    物理デバイスを通過の性質上、セキュリティで保護された環境で使用するかどうかを理解するデバイスの製造元と協力します。

安全な環境向け。

- **シールドが有効になっているバーチャルマシンを展開し、保護されたファブリックに展開します。** 

    詳細については、次を参照してください。 [第 2 世代のセキュリティ設定](../learn-more/Generation-2-virtual-machine-security-settings-for-Hyper-V.md) と [保護され、fabric](../../../security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms-top-node.md)します。
