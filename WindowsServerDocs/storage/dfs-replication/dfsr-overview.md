---
Title: DFS レプリケーションの概要
ms.date: 03/08/2019
ms.prod: windows-server-threshold
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 17fa97e28d099806c9280e42dd900e8d6c708641
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850243"
---
# <a name="dfs-replication-overview"></a>DFS レプリケーションの概要

> 適用対象:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008、Windows Server (半期チャネル)

DFS レプリケーションとは、複数のサーバーやサイト間で効率的にフォルダー (DFS 名前空間パスで参照されるを含む) をレプリケートすることができる Windows server の役割サービスです。 DFS レプリケーションは、フォルダーを限られた帯域幅のネットワーク接続サーバー間で同期するために使用できる、効率的なマルチ マスター レプリケーション エンジンです。 DFS 名前空間、および Windows Server 2008 またはそれ以降のドメイン機能レベルを使用するドメインの Active Directory Domain Services (AD DS) SYSVOL フォルダーをレプリケートするため、レプリケーション エンジンとしてファイル レプリケーション サービス (FRS) を置き換えます。

DFS レプリケーションは、RDC (Remote Differential Compression) と呼ばれる圧縮アルゴリズムを使用します。 RDC は、ファイルにデータへの変更を検出し、ファイル全体ではなく、変更されたファイル ブロックのみをレプリケートする DFS レプリケーションを有効にします。

DFS レプリケーションを使用して SYSVOL をレプリケートする方法の詳細については、次を参照してください。 [DFS レプリケーションに SYSVOL レプリケーション移行](migrate-sysvol-to-dfsr.md)します。

DFS レプリケーションを使用するには、は、レプリケーション グループを作成し、レプリケート フォルダーをグループに追加する必要があります。 レプリケーション グループ、レプリケート フォルダー、およびメンバーは、次の図に示します。

![2 つのメンバー間の接続を含むレプリケーション グループ、それぞれがいくつかレプリケート フォルダー](media\dfsr-overview.gif)

この図では、レプリケーション グループが 1 つまたは複数のレプリケート フォルダーのレプリケーションに参加している、メンバーと呼ばれるサーバーのセットを示します。 レプリケート フォルダーは、各メンバーの同期を維持するフォルダーです。 図では、2 つのレプリケートされたフォルダーがあります。Projects と Proposals します。 データは、各レプリケート フォルダーの変更、変更は、レプリケーション グループのメンバー間の接続間でレプリケートされます。 すべてのメンバー間の接続は、レプリケーション トポロジを形成します。
1 つのレプリケーション グループ内の複数のレプリケート フォルダーを作成するには、トポロジ、スケジュール、および帯域幅調整をレプリケーション グループは、レプリケート フォルダーごとに適用されるため、レプリケート フォルダーを展開するプロセスが簡略化します。 追加のレプリケート フォルダーを展開するには、命令を使用する Dfsradmin.exe またはフォロー、ウィザードでローカル パスと、新しいレプリケート フォルダーのアクセス許可を定義します。

各レプリケート フォルダーはファイルとサブフォルダーのフィルターなど、一意の設定を持つ別のファイルと各レプリケート フォルダーのサブフォルダーを除外できるようにします。

各メンバーに保存されたレプリケート フォルダーは、メンバーで別々 のボリューム上に配置でき、レプリケート フォルダーは、共有フォルダーや名前空間の一部にする必要はありません。 ただし、DFS の管理スナップインで簡単にレプリケート フォルダーを共有し、必要に応じて既存の名前空間で公開します。

DFS レプリケーションを管理するには、DFS の管理、DfsrAdmin と Dfsrdiag コマンド、または WMI を呼び出すスクリプトを使用します。

## <a name="requirements"></a>要件

DFS レプリケーションを展開する前に、サーバーを次のように構成する必要があります。

- Windows Server 2003 R2 またはそれ以降のスキーマの追加機能を含める Active Directory Domain Services (AD DS) スキーマを更新します。 読み取り専用のレプリケート フォルダーは、Windows Server 2003 R2 または古いスキーマを追加で使用できません。
- レプリケーション グループに含まれるすべてのサーバーが、同じフォレストに存在することを確認します。 異なるフォレスト内にある複数のサーバーにまたがってレプリケーションを有効にすることはできません。
- レプリケーション グループのメンバーとして機能するすべてのサーバー上では、DFS レプリケーションをインストールします。
- ウイルス対策ソフトウェア ベンダーに問い合わせて、使用するウイルス対策ソフトウェアが DFS レプリケーションと互換性があることを確認します。
- NTFS ファイル システムでフォーマットされているボリュームで、レプリケートするフォルダーを探します。 DFS レプリケーションでは Resilient File System (ReFS) または FAT ファイル システムはサポートされていません。 また、DFS レプリケーションではクラスターの共有ボリュームに保存されているコンテンツはレプリケートできません。

## <a name="interoperability-with-azure-virtual-machines"></a>Azure Virtual Machines との相互運用性

Windows Server; は、DFS レプリケーションを使用して、Azure の仮想マシンのテストします。ただしがいくつかの制限事項と要件に従う必要があります。

- DFS レプリケーションによって SYSVOL フォルダー以外のデータをレプリケートしているサーバーを、スナップショットや保存された状態を使用して復元すると、DFS レプリケーションが失敗します。この場合、特別なデータベース回復手順が必要になります。 また、仮想マシンをエクスポート、複製、またはコピーすることも避けてください。 詳細については、Microsoft サポート技術情報の記事 [2517913](http://support.microsoft.com/kb/2517913) と、「 [Safely Virtualizing DFSR (DFSR を安全に仮想化する)](https://blogs.technet.microsoft.com/filecab/2013/04/05/safely-virtualizing-dfsr/)」を参照してください。
- 仮想マシンでホストされているレプリケート フォルダー内のデータをバックアップする場合は、ゲスト仮想マシン内からバックアップ ソフトウェアを使用する必要があります。
- DFS レプリケーションには、物理または仮想化ドメイン コント ローラーへのアクセスが必要です: Azure AD と直接通信できません。
- DFS レプリケーションを行うには、オンプレミスのレプリケーション グループ メンバーと、Azure VM でホストされているメンバーとの間の VPN 接続が必要です。 また、オンプレミスのルーター (Forefront Threat Management Gateway など) を構成して、RPC エンドポイント マッパー (ポート 135) と、49152 ～ 65535 の範囲にランダムに割り当てられたポートが、VPN 接続を経由できるようにする必要があります。 Set-dfsrmachineconfiguration コマンドレットまたは Dfsrdiag コマンド ライン ツールを使用すると、ランダムなポートではなく静的ポートを指定します。 DFS レプリケーション用に静的ポートを指定する方法の詳細については、「 [Set-DfsrServiceConfiguration](https://docs.microsoft.com/powershell/module/dfsr/set-dfsrserviceconfiguration)」を参照してください。 Windows Server の管理用に開く関連ポートについては、Microsoft サポート技術情報の記事 [832017](http://support.microsoft.com/kb/832017) を参照してください。

Azure 仮想マシンを使い始める方法については、 [Microsoft Azure の Web サイト](https://docs.microsoft.com/azure/virtual-machines/)を参照してください。

## <a name="installing-dfs-replication"></a>DFS レプリケーションのインストール

DFS レプリケーションは、ファイル サービスおよび記憶域サービスの役割の一部です。 (DFS の管理、DFS レプリケーション モジュールは、Windows PowerShell とコマンド ライン ツール) の dfs 管理ツールは、リモート サーバー管理ツールの一部として個別にインストールされます。

DFS レプリケーションを使用して、インストール[Windows Admin Center](../../manage/windows-admin-center/understand/windows-admin-center.md)、サーバー マネージャー、または PowerShell で次のセクションで説明します。

### <a name="to-install-dfs-by-using-server-manager"></a>サーバー マネージャーを使用して DFS をインストールするには

1. サーバー マネージャーを開き、**[管理]** をクリックし、**[役割と機能の追加]** をクリックします。 役割と機能の追加ウィザードが表示されます。

2. **[サーバーの選択]** ページで、DFS をインストールするオフライン仮想マシンのサーバーまたは仮想ハード ディスク (VHD) を選択します。

3. インストールする役割サービスおよび機能を選択します。

    - DFS レプリケーション サービスをインストールする、**サーバーの役割**] ページで、[ **DFS レプリケーション**します。

    - DFS 管理ツールのみをインストールするには、**[機能]** ページで、**[リモート サーバー管理ツール]**、**[役割管理ツール]**、**[ファイル サービス ツール]** の順に展開し、**[DFS 管理ツール]** をクリックします。

         **DFS 管理ツール**DFS の管理スナップインで、DFS レプリケーションとは、Windows PowerShell とコマンド ライン ツールは、DFS 名前空間モジュールがインストールされますが、サーバーで、DFS サービスをインストールできません。

### <a name="to-install-dfs-replication-by-using-windows-powershell"></a>Windows PowerShell を使用して、DFS レプリケーションをインストールするには

管理者特権で Windows PowerShell セッションを開くし、次のコマンドでは、入力場所 < 名前\>は役割サービスまたはインストールする機能 (関連する役割サービスまたは機能名の一覧については、次の表を参照してください)。

```PowerShell
Install-WindowsFeature <name>
```

|役割サービスまたは機能|名前|
|---|---|
|DFS レプリケーション|`FS-DFS-Replication`|
|DFS 管理ツール|`RSAT-DFS-Mgmt-Con`|

たとえば、リモート サーバー管理ツール機能の分散ファイル システム ツール部分をインストールするには、次のように入力します。

```PowerShell
Install-WindowsFeature "RSAT-DFS-Mgmt-Con"
```

DFS レプリケーション、およびリモート サーバー管理ツール機能の分散ファイル システム ツール部分をインストールするには、次のように入力します。

```PowerShell
Install-WindowsFeature "FS-DFS-Replication", "RSAT-DFS-Mgmt-Con"
```

## <a name="see-also"></a>関連項目

- [DFS 名前空間と DFS レプリケーションの概要](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj127250(v%3dws.11))
- [チェックリスト:DFS レプリケーションをデプロイします。](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772201(v%3dws.11))
- [チェックリスト:DFS レプリケーションを管理します。](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc755035(v%3dws.11))
- [DFS レプリケーションを展開します。](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770925(v%3dws.11))
- [DFS レプリケーションを管理します。](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770925(v%3dws.11))
- [DFS レプリケーションのトラブルシューティング](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732802(v%3dws.11))
