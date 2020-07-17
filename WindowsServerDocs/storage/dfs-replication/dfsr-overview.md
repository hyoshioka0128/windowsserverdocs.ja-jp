---
title: DFS レプリケーションの概要
ms.date: 03/08/2019
ms.prod: windows-server
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 8164032ff4071facb33c1df0edf44dcc86a6d918
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475419"
---
# <a name="dfs-replication-overview"></a>DFS レプリケーションの概要

> 適用先:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008、Windows Server (半期チャネル)

DFS レプリケーションは、複数のサーバーやサイト間で効率的にフォルダー (DFS 名前空間パスで参照されるフォルダーなど) をレプリケートできる Windows Server の役割サービスです。 DFS レプリケーションは、限られた帯域幅のネットワーク上で、複数のサーバー間のフォルダーを同期するために使用する、効率的なマルチ マスター レプリケーション エンジンです。 これは、DFS 名前空間のレプリケーション エンジンとして、また Windows Server 2008 以降のドメイン機能レベルを使用するドメインで Active Directory Domain Services (AD DS) SYSVOL フォルダーをレプリケートするためのレプリケーション エンジンとして、ファイル レプリケーション サービス (FRS) に置き換わります。

DFS レプリケーションは、RDC (Remote Differential Compression) と呼ばれる圧縮アルゴリズムを使用します。 RDC はファイル内のデータに対する変更を検出し、DFS レプリケーションにより、ファイル全体ではなく、変更されたファイル ブロックのみをレプリケートします。

DFS レプリケーションを使用して SYSVOL をレプリケートする方法の詳細については、「[SYSVOL のレプリケーションを DFS レプリケーションに移行する](migrate-sysvol-to-dfsr.md)」を参照してください。

DFS レプリケーションを使用するには、レプリケーション グループを作成し、そのグループにレプリケート フォルダーを追加する必要があります。 次の図に、レプリケーション グループ、レプリケート フォルダー、およびメンバーを示します。

![それぞれがいくつかのレプリケートフォルダーを持つ、2 つのメンバー間の接続を含むレプリケーション グループ](media/dfsr-overview.gif)

この図に示すとおり、 レプリケーション グループは、1 つまたは複数のレプリケート フォルダーのレプリケーションに参加している一連のサーバー (メンバーと呼ばれます) で構成されます。 レプリケート フォルダーとは、各メンバー間で常に同期がとられているフォルダーです。 この図では、Projects と Proposals という 2 つのレプリケート フォルダーがあります。 各レプリケート フォルダー内のデータが変更されるたびに、これらの変更内容は、接続を介してレプリケーション グループのメンバー間でレプリケートされます。 すべてのメンバー間の接続によって、レプリケーション トポロジが形成されます。
1 つのレプリケーション グループに複数のレプリケート フォルダーを作成すると、そのレプリケーション グループのトポロジ、スケジュール、および帯域幅調整が各レプリケート フォルダーに適用されるため、レプリケート フォルダーの展開プロセスが簡略化されます。 追加のレプリケート フォルダーを展開するには、Dfsradmin.exe を使用するか、またはウィザードの指示に従って、新しいレプリケート フォルダーのローカル パスとアクセス許可を定義します。

各レプリケート フォルダーには固有の設定 (ファイルとサブフォルダーのフィルターなど) があるため、レプリケート フォルダーごとに異なるファイルとサブフォルダーをフィルターで除外できます。

各メンバー上に保管されているレプリケート フォルダーは、メンバー上の異なるボリュームに配置可能であり、レプリケート フォルダーは名前空間の一部や共有フォルダーである必要はありません。 ただし、DFS の管理スナップインを使用すると、簡単にレプリケート フォルダーを共有し、必要に応じて既存の名前空間で公開できます。

DFS レプリケーションは、DFS の管理、DfsrAdmin および Dfsrdiag コマンド、または WMI を呼び出すスクリプトを使用して管理できます。

## <a name="requirements"></a>要件

DFS レプリケーションを展開する前に、サーバーを次のように構成する必要があります。

- Windows Server 2003 R2 以降のスキーマを追加できるように、Active Directory Domain Services (AD DS) スキーマを更新します。 Windows Server 2003 R2 以前のスキーマでは、読み取り専用のレプリケート フォルダーを使用することができません。
- レプリケーション グループに含まれるすべてのサーバーが、同じフォレストに存在することを確認します。 異なるフォレスト内にある複数のサーバーにまたがってレプリケーションを有効にすることはできません。
- レプリケーション グループのメンバーとして動作するすべてのサーバーに DFS レプリケーションをインストールします。
- ウイルス対策ソフトウェア ベンダーに問い合わせて、使用するウイルス対策ソフトウェアが DFS レプリケーションと互換性があることを確認します。
- NTFS ファイル システムでフォーマットされているボリュームで、レプリケートするフォルダーを探します。 DFS レプリケーションでは Resilient File System (ReFS) または FAT ファイル システムはサポートされていません。 また、DFS レプリケーションではクラスターの共有ボリュームに保存されているコンテンツはレプリケートできません。

## <a name="interoperability-with-azure-virtual-machines"></a>Azure 仮想マシンとの相互運用性

Azure 内の仮想マシンにおける DFS レプリケーションの使用は Windows Server でテスト済みです。だだし、従わなければならない制限事項と要件がいくつかあります。

- DFS レプリケーションによって SYSVOL フォルダー以外のデータをレプリケートしているサーバーを、スナップショットや保存された状態を使用して復元すると、DFS レプリケーションが失敗します。この場合、特別なデータベース回復手順が必要になります。 また、仮想マシンをエクスポート、複製、またはコピーすることも避けてください。 詳細については、Microsoft サポート技術情報の記事 [2517913](https://support.microsoft.com/kb/2517913) と、「 [Safely Virtualizing DFSR (DFSR を安全に仮想化する)](https://blogs.technet.microsoft.com/filecab/2013/04/05/safely-virtualizing-dfsr/)」を参照してください。
- 仮想マシンに格納されているレプリケート フォルダー内のデータをバックアップする場合は、ゲスト仮想マシン内からバックアップ ソフトウェアを使用する必要があります。
- DFS レプリケーションを行うには、物理または仮想化ドメイン コント ローラーへのアクセスが必要です。Azure AD と直接通信することはできません。
- DFS レプリケーションを行うには、オンプレミスのレプリケーション グループ メンバーと、Azure VM でホストされているメンバーとの間の VPN 接続が必要です。 また、オンプレミスのルーター (Forefront Threat Management Gateway など) を構成して、RPC エンドポイント マッパー (ポート 135) と、49152 ～ 65535 の範囲にランダムに割り当てられたポートが、VPN 接続を経由できるようにする必要があります。 ランダム ポートではなく静的ポートを指定するには、Set-DfsrMachineConfiguration コマンドレットか、Dfsrdiag コマンド ライン ツールを使用できます。 DFS レプリケーション用に静的ポートを指定する方法の詳細については、「 [Set-DfsrServiceConfiguration](https://docs.microsoft.com/powershell/module/dfsr/set-dfsrserviceconfiguration)」を参照してください。 Windows Server の管理用に開く関連ポートについては、Microsoft サポート技術情報の記事 [832017](https://support.microsoft.com/kb/832017) を参照してください。

Azure 仮想マシンを使い始める方法については、 [Microsoft Azure の Web サイト](https://docs.microsoft.com/azure/virtual-machines/)を参照してください。

## <a name="installing-dfs-replication"></a>DFS レプリケーションのインストール

DFS レプリケーションは、ファイル サービスおよび記憶域サービスの役割の一部です。 DFS 用の管理ツール (DFS の管理、Windows PowerShell 用の DFS レプリケーション モジュール、およびコマンド ライン ツール) がリモート サーバー管理ツールの一部として個別にインストールされています。

DFS レプリケーションは、以降のセクションの手順に従って、[Windows Admin Center](../../manage/windows-admin-center/understand/windows-admin-center.md)、サーバー マネージャーまたは PowerShell を使用してインストールします。

### <a name="to-install-dfs-by-using-server-manager"></a>サーバー マネージャーを使用して DFS をインストールするには

1. サーバー マネージャーを開き、 **[管理]** をクリックし、 **[役割と機能の追加]** をクリックします。 役割と機能の追加ウィザードが表示されます。

2. **[サーバーの選択]** ページで、DFS をインストールするオフライン仮想マシンのサーバーまたは仮想ハード ディスク (VHD) を選択します。

3. インストールする役割サービスおよび機能を選択します。

    - DFS レプリケーション サービスをインストールするには、 **[サーバーの役割]** ページで、 **[DFS レプリケーション]** をクリックします。

    - DFS 管理ツールのみをインストールするには、 **[機能]** ページで、 **[リモート サーバー管理ツール]** 、 **[役割管理ツール]** 、 **[ファイル サービス ツール]** の順に展開し、 **[DFS 管理ツール]** をクリックします。

         **[DFS 管理ツール]** では DFS 管理スナップイン、Windows PowerShell 用の DFS レプリケーション モジュールと DFS 名前空間モジュール、およびコマンド ライン ツールがインストールされますが、DFS サービスはサーバーにインストールされません。

### <a name="to-install-dfs-replication-by-using-windows-powershell"></a>Windows PowerShell を使用して DFS レプリケーションをインストールするには

管理者特権を使用して Windows PowerShell セッションを開き、次のコマンドを入力します。<name\> にはインストールする役割サービスまたは機能を入力します (関連する役割サービスまたは機能の名前の一覧については、下の表を参照してください)。

```PowerShell
Install-WindowsFeature <name>
```

|役割サービスまたは機能|名前|
|---|---|
|DFS レプリケーション|`FS-DFS-Replication`|
|[DFS 管理ツール]|`RSAT-DFS-Mgmt-Con`|

たとえば、リモート サーバー管理ツール機能の分散ファイル システム ツール部分をインストールするには、次のように入力します。

```PowerShell
Install-WindowsFeature "RSAT-DFS-Mgmt-Con"
```

リモート サーバー管理ツール機能の DFS レプリケーション、および分散ファイル システム ツール部分をインストールするには、次のように入力します。

```PowerShell
Install-WindowsFeature "FS-DFS-Replication", "RSAT-DFS-Mgmt-Con"
```

## <a name="additional-references"></a>その他の参照情報

- [DFS 名前空間と DFS レプリケーションの概要](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj127250(v%3dws.11))
- [チェックリスト:DFS レプリケーションを展開する](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772201(v%3dws.11))
- [チェックリスト:DFS レプリケーションを管理する](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc755035(v%3dws.11))
- [DFS レプリケーションの展開](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770925(v%3dws.11))
- [DFS レプリケーションの管理](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770925(v%3dws.11))
- [DFS レプリケーションのトラブルシューティング](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732802(v%3dws.11))
