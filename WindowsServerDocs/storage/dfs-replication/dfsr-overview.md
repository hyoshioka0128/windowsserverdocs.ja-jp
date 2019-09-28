---
title: DFS レプリケーションの概要
ms.date: 03/08/2019
ms.prod: windows-server
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: eebce26eef6eceddc064e3bb179f268ccf47c93d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386062"
---
# <a name="dfs-replication-overview"></a>DFS レプリケーションの概要

> 適用対象:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008、Windows Server (半期チャネル)

DFS レプリケーションは、Windows Server の役割サービスです。これを使用すると、複数のサーバーやサイト間でフォルダー (DFS 名前空間パスによって参照されるフォルダーを含む) を効率的にレプリケートできます。 DFS レプリケーションは、帯域幅が制限されたネットワーク接続を介してサーバー間でフォルダーの同期を維持するために使用できる、効率的なマルチマスターレプリケーションエンジンです。 これにより、ファイルレプリケーションサービス (FRS) が DFS 名前空間のレプリケーションエンジンとして置き換えられます。また、Windows Server 2008 以降のドメイン機能レベルを使用するドメインで Active Directory Domain Services (AD DS) SYSVOL フォルダーをレプリケートすることもできます。

DFS レプリケーションは、RDC (Remote Differential Compression) と呼ばれる圧縮アルゴリズムを使用します。 RDC は、ファイル内のデータに対する変更を検出し、ファイル全体ではなく、変更されたファイルブロックのみをレプリケート DFS レプリケーションできるようにします。

DFS レプリケーションを使用した SYSVOL のレプリケートの詳細については、「 [DFS レプリケーションへの sysvol レプリケーションの移行](migrate-sysvol-to-dfsr.md)」を参照してください。

DFS レプリケーションを使用するには、レプリケーショングループを作成し、そのグループにレプリケートフォルダーを追加する必要があります。 次の図は、レプリケーショングループ、レプリケートフォルダー、およびメンバーを示しています。

![2つのメンバー間の接続を含むレプリケーショングループ。それぞれにレプリケートフォルダーがいくつかあります。](media/dfsr-overview.gif)

この図は、レプリケーショングループが、1つまたは複数のレプリケートフォルダーのレプリケーションに参加する、メンバーと呼ばれる一連のサーバーであることを示しています。 レプリケートフォルダーは、各メンバーの同期状態を維持するフォルダーです。 図には、次の2つのレプリケートフォルダーがあります。プロジェクトと提案。 各レプリケートフォルダー内のデータが変更されると、レプリケーショングループのメンバー間の接続間で変更がレプリケートされます。 すべてのメンバー間の接続は、レプリケーショントポロジを形成します。
1つのレプリケーショングループに複数のレプリケートフォルダーを作成すると、レプリケーショングループのトポロジ、スケジュール、および帯域幅の調整が各レプリケートフォルダーに適用されるため、レプリケートフォルダーの展開プロセスが簡単になります。 追加のレプリケートフォルダーを展開するには、Dfsradmin.exe またはを使用して、ウィザードの指示に従って、新しいレプリケートフォルダーのローカルパスとアクセス許可を定義します。

各レプリケートフォルダーには、ファイルとサブフォルダーのフィルターなどの固有の設定があるため、レプリケートフォルダーごとに異なるファイルとサブフォルダーを除外できます。

各メンバーに格納されているレプリケートフォルダーは、メンバー内のさまざまなボリュームに配置できます。また、レプリケートフォルダーは、共有フォルダーまたは名前空間の一部である必要はありません。 ただし、DFS 管理スナップインを使用すると、レプリケートされたフォルダーを簡単に共有し、必要に応じて既存の名前空間に発行することができます。

DFS レプリケーションを管理するには、DFS の管理、Dfsradmin.exe と Dfsrdiag.exe のコマンド、または WMI を呼び出すスクリプトを使用します。

## <a name="requirements"></a>要件

DFS レプリケーションを展開する前に、サーバーを次のように構成する必要があります。

- Active Directory Domain Services (AD DS) スキーマを更新して、Windows Server 2003 R2 以降のスキーマが追加されるようにします。 Windows Server 2003 R2 以前のスキーマ追加では、読み取り専用のレプリケートフォルダーを使用することはできません。
- レプリケーション グループに含まれるすべてのサーバーが、同じフォレストに存在することを確認します。 異なるフォレスト内にある複数のサーバーにまたがってレプリケーションを有効にすることはできません。
- レプリケーショングループのメンバとして機能するすべてのサーバーに DFS レプリケーションをインストールします。
- ウイルス対策ソフトウェア ベンダーに問い合わせて、使用するウイルス対策ソフトウェアが DFS レプリケーションと互換性があることを確認します。
- NTFS ファイル システムでフォーマットされているボリュームで、レプリケートするフォルダーを探します。 DFS レプリケーションでは Resilient File System (ReFS) または FAT ファイル システムはサポートされていません。 また、DFS レプリケーションではクラスターの共有ボリュームに保存されているコンテンツはレプリケートできません。

## <a name="interoperability-with-azure-virtual-machines"></a>Azure Virtual Machines との相互運用性

Azure の仮想マシンでの DFS レプリケーションの使用は、Windows Server でテストされています。ただし、いくつかの制限事項と要件に従う必要があります。

- DFS レプリケーションによって SYSVOL フォルダー以外のデータをレプリケートしているサーバーを、スナップショットや保存された状態を使用して復元すると、DFS レプリケーションが失敗します。この場合、特別なデータベース回復手順が必要になります。 同様に、仮想マシンをエクスポート、複製、またはコピーしないでください。 詳細については、Microsoft サポート技術情報の記事 [2517913](http://support.microsoft.com/kb/2517913) と、「 [Safely Virtualizing DFSR (DFSR を安全に仮想化する)](https://blogs.technet.microsoft.com/filecab/2013/04/05/safely-virtualizing-dfsr/)」を参照してください。
- 仮想マシンでホストされているレプリケート フォルダー内のデータをバックアップする場合は、ゲスト仮想マシン内からバックアップ ソフトウェアを使用する必要があります。
- DFS レプリケーションは、物理または仮想化されたドメインコントローラーにアクセスする必要があります。 Azure AD と直接通信することはできません。
- DFS レプリケーションを行うには、オンプレミスのレプリケーション グループ メンバーと、Azure VM でホストされているメンバーとの間の VPN 接続が必要です。 また、オンプレミスのルーター (Forefront Threat Management Gateway など) を構成して、RPC エンドポイント マッパー (ポート 135) と、49152 ～ 65535 の範囲にランダムに割り当てられたポートが、VPN 接続を経由できるようにする必要があります。 Set-dfsrmachineconfiguration コマンドレットまたは Dfsrdiag.exe コマンドラインツールを使用して、ランダムポートではなく静的ポートを指定できます。 DFS レプリケーション用に静的ポートを指定する方法の詳細については、「 [Set-DfsrServiceConfiguration](https://docs.microsoft.com/powershell/module/dfsr/set-dfsrserviceconfiguration)」を参照してください。 Windows Server の管理用に開く関連ポートについては、Microsoft サポート技術情報の記事 [832017](http://support.microsoft.com/kb/832017) を参照してください。

Azure 仮想マシンを使い始める方法については、 [Microsoft Azure の Web サイト](https://docs.microsoft.com/azure/virtual-machines/)を参照してください。

## <a name="installing-dfs-replication"></a>DFS レプリケーションのインストール

DFS レプリケーションは、ファイルサービスおよび記憶域サービスの役割の一部です。 DFS 用の管理ツール (DFS の管理、Windows PowerShell 用の DFS レプリケーションモジュール、およびコマンドラインツール) は、リモートサーバー管理ツールの一部として個別にインストールされます。

次のセクションで説明するように、 [Windows 管理センター](../../manage/windows-admin-center/understand/windows-admin-center.md)、サーバーマネージャー、または PowerShell を使用して DFS レプリケーションをインストールします。

### <a name="to-install-dfs-by-using-server-manager"></a>サーバー マネージャーを使用して DFS をインストールするには

1. サーバー マネージャーを開き、 **[管理]** をクリックし、 **[役割と機能の追加]** をクリックします。 役割と機能の追加ウィザードが表示されます。

2. **[サーバーの選択]** ページで、DFS をインストールするオフライン仮想マシンのサーバーまたは仮想ハード ディスク (VHD) を選択します。

3. インストールする役割サービスおよび機能を選択します。

    - DFS レプリケーションサービスをインストールするには、 **[サーバーの役割]** ページで **[DFS レプリケーション]** を選択します。

    - DFS 管理ツールのみをインストールするには、 **[機能]** ページで、 **[リモート サーバー管理ツール]** 、 **[役割管理ツール]** 、 **[ファイル サービス ツール]** の順に展開し、 **[DFS 管理ツール]** をクリックします。

         Dfs**管理ツール**は、dfs 管理スナップイン、Windows PowerShell 用の DFS レプリケーションと Dfs 名前空間モジュール、およびコマンドラインツールをインストールしますが、dfs サービスはサーバーにインストールしません。

### <a name="to-install-dfs-replication-by-using-windows-powershell"></a>Windows PowerShell を使用して DFS レプリケーションをインストールするには

管理者特権で Windows PowerShell セッションを開き、次のコマンドを入力します。ここで\> < name は、インストールする役割サービスまたは機能です (関連する役割サービスまたは機能名の一覧については、次の表を参照してください)。

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

DFS レプリケーションと、リモートサーバー管理ツール機能の分散ファイルシステムツール部分をインストールするには、次のように入力します。

```PowerShell
Install-WindowsFeature "FS-DFS-Replication", "RSAT-DFS-Mgmt-Con"
```

## <a name="see-also"></a>関連項目

- [DFS 名前空間と DFS レプリケーションの概要](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj127250(v%3dws.11))
- [チェックリスト:DFS レプリケーションのデプロイ](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772201(v%3dws.11))
- [チェックリスト:DFS レプリケーションの管理](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc755035(v%3dws.11))
- [DFS レプリケーションの展開](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770925(v%3dws.11))
- [DFS レプリケーションの管理](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770925(v%3dws.11))
- [DFS レプリケーションのトラブルシューティング](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732802(v%3dws.11))
