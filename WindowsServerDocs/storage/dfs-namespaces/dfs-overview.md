---
title: "DFS 名前空間の概要"
ms.prod: windows-server-threshold
ms.author: jgerend
ms.manager: brianlic
ms.technology: storage
ms.topic: article
author: jasongerend
ms.date: 07/10/2017
description: "このトピックでは、DFS 名前空間について説明します。DFS 名前空間は、複数のサーバー上に配置されている共有フォルダーを、論理的に構造化された 1 つ以上の名前空間にグループ化できる Windows Server の役割サービスです。"
ms.openlocfilehash: f3a76208fa1d6e1207edd699f830fc05a360bee5
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="dfs-namespaces-overview"></a>DFS 名前空間の概要

> 適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

DFS 名前空間は、複数のサーバー上に配置されている共有フォルダーを、論理的に構造化された 1 つ以上の名前空間にグループ化できる Windows Server の役割サービスです。 これにより、ユーザーに対して共有フォルダーを仮想的に表示し、複数のサーバー上にあるファイルを 1 つのパスで表すことができます (次の図を参照)。

![DFS 名前空間のテクノロジ要素](media/dfs-overview.png)

次では、DFS 名前空間を構成する要素について説明します。

- **名前空間サーバー**: 名前空間サーバーは、名前空間をホストします。 名前空間サーバーには、メンバー サーバーやドメイン コントローラーを使用できます。
- **名前空間のルート**: 名前空間のルートは、名前空間の開始ポイントです。 上の図では、ルートの名前は Public、名前空間のパスは \\\\Contoso\\Public です。 この種類の名前空間は、ドメイン名 (Contoso など) で始まり、メタデータを Active Directory Domain Services (AD DS) に格納しているため、ドメインベースの名前空間です。 上の図では、名前空間サーバーが 1 つだけ示されていますが、ドメインベースの名前空間を複数の名前空間サーバーでホストして、名前空間の可用性を向上させることもできます。
- **フォルダー**:  フォルダー ターゲットを持たないフォルダーは名前空間に階層構造を追加し、フォルダー ターゲットを持つフォルダーはユーザーに対して実際の内容を提供します。 ユーザーが名前空間内のフォルダー ターゲットを持つフォルダーを参照すると、クライアント コンピューターは、そのフォルダー ターゲットの 1 つにクライアント コンピューターを透過的にリダイレクトする紹介を受け取ります。
- **フォルダー ターゲット**: フォルダー ターゲットは、共有フォルダー、または名前空間内のフォルダーに関連付けられた別の名前空間の UNC パスです。 フォルダー ターゲットは、データおよび内容が保存される場所です。 上の図で、Tools という名前のフォルダーには、2 つのフォルダー ターゲット (ロンドンに 1 つ、ニューヨークに 1 つ) があります。また、Training Guides という名前のフォルダーには、フォルダー ターゲットがニューヨークに 1 つだけあります。 \\Contoso\Public\Software\Tools を参照したユーザーは、そのユーザーが現在所属しているサイトに応じて、共有フォルダー \\LDN-SVR-01\Tools または \\NYC-SVR-01\Tools に透過的にリダイレクトされます。

このトピックでは、DFS のインストール方法、新機能、評価と展開に関する情報の参照先について説明します。

名前空間の管理には、DFS 管理、[Windows PowerShell の DFS 名前空間 (DFSN) コマンドレット](https://technet.microsoft.com/library/jj884270.aspx)、**DfsUtil** コマンド、WMI を呼び出すスクリプトのいずれかを使用できます。

## <a name="server-requirements-and-limits"></a>サーバーの要件と制限

DFS の管理の実行または DFS 名前空間の使用には、その他のハードウェアまたはソフトウェアの要件はありません。

名前空間サーバーとは、名前空間をホストするドメイン コントローラーまたはメンバー サーバーです。 1 つのサーバーでホストできる名前空間の数は、名前空間サーバーで実行されているオペレーティング システムによって決まります。

次のオペレーティング システムを実行するサーバーは、複数のドメインベースの名前空間と、単一のスタンドアロンの名前空間をホストできます。 

- Windows Server (半期チャネル)
- Windows Server 2016 
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 Datacenter/Enterprise

次のオペレーティング システムを実行するサーバーは、単一のスタンドアロンの名前空間をホストできます。

- Windows Server 2008 R2 Standard


次の表では、名前空間をホストするサーバーを選択する場合に考慮すべきその他の事項について説明します。

|スタンドアロンの名前空間をホストするサーバー|ドメインベースの名前空間をホストするサーバー|
|---|---|
|名前空間をホストするための NTFS ボリュームを含める必要があります。|名前空間をホストするための NTFS ボリュームを含める必要があります。|
|メンバー サーバーまたはドメイン コントローラーを指定できます。|名前空間が構成されているドメインのメンバー サーバーまたはドメイン コントローラーである必要があります。 この要件は、特定のドメインベースの名前空間をホストしているすべての名前空間サーバーに適用されます。|
|フェールオーバー クラスターでホストして、名前空間の可用性を高めることができます。|名前空間には、フェールオーバー クラスター内のクラスター化されたリソースを指定することはできません。 ただし、名前空間をそのサーバーのローカルのリソースとしてのみ構成する場合は、フェールオーバー クラスター内のノードとしても機能するサーバー上に名前空間を置くことができます。|

## <a name="installing-dfs-namespaces"></a>DFS 名前空間をインストールする

DFS 名前空間および DFS レプリケーションは、ファイル サービスおよび記憶域サービスの役割の一部です。 DFS 用の管理ツール (DFS の管理、Windows PowerShell 用の DFS 名前空間モジュール、およびコマンド ライン ツール) がリモート サーバー管理ツールの一部として個別にインストールされています。

DFS 名前空間は、次のセクションの手順に従って、サーバー マネージャーまたは PowerShell を使用してインストールします。

### <a name="to-install-dfs-by-using-server-manager"></a>サーバー マネージャーを使用して DFS をインストールするには

1. サーバー マネージャーを開き、**[管理]**をクリックし、**[役割と機能の追加]**をクリックします。 役割と機能の追加ウィザードが表示されます。

2. **[サーバーの選択]** ページで、DFS をインストールするオフライン仮想マシンのサーバーまたは仮想ハード ディスク (VHD) を選択します。

3. インストールする役割サービスおよび機能を選択します。

    - DFS 名前空間サービスをインストールするには、**[サーバーの役割]** ページで、**[DFS 名前空間]** をクリックします。

    - DFS 管理ツールのみをインストールするには、**[機能]** ページで、**[リモート サーバー管理ツール]**、**[役割管理ツール]**、**[ファイル サービス ツール]** の順に展開し、**[DFS 管理ツール]** をクリックします。

         **[DFS 管理ツール]** では DFS 管理スナップイン、Windows PowerShell 用の DFS 名前空間モジュール、およびコマンド ライン ツールがインストールされますが、DFS サービスはサーバーにインストールされません。

### <a name="to-install-dfs-by-using-windows-powershell"></a>Windows PowerShell を使用して DFS をインストールするには

管理者特権を使用して Windows PowerShell セッションを開き、次のコマンドを入力します。<name\> にはインストールする役割サービスまたは機能を入力します。関連する役割サービスまたは機能の名前の一覧については、下の表を参照してください。

```PowerShell
Install-WindowsFeature <name>
```

|役割サービスまたは機能|名前|
|---|---|
|DFS 名前空間|`FS-DFS-Namespace`|
|DFS 管理ツール|`RSAT-DFS-Mgmt-Con`|

たとえば、リモート サーバー管理ツール機能の分散ファイル システム ツール部分をインストールするには、次のように入力します。

```PowerShell
Install-WindowsFeature RSAT-DFS-Mgmt-Con
```

リモート サーバー管理ツール機能の DFS 名前空間および分散ファイル システム ツール部分をインストールするには、次のように入力します。

```PowerShell
Install-WindowsFeature FS-DFS-Namespace, RSAT-DFS-Mgmt-Con
```

## <a name="interoperability-with-azure-virtual-machines"></a>Azure Virtual Machines との相互運用性

Microsoft Azure 内の仮想マシンにおける DFS 名前空間の使用はテスト済みです。ただし、いくつかの制限事項と要件があります。

- Azure の仮想マシンでは、スタンドアロンの名前空間をクラスター化することはできません。

- Azure の仮想マシン (Azure Active Directory を使用した環境を含む) では、ドメイン ベースの名前空間をホストすることはできますが、オンプレミスの名前空間サーバーと、Azure VM でホストされている名前空間サーバーの両方を単一の名前空間に含めることは (Active Directory フェデレーション サービス (AD FS) を使用している場合でも) できません。

Azure 仮想マシンを使い始める方法については、[Azure 仮想マシンのドキュメント](https://docs.microsoft.com/azure/virtual-machines/)を参照してください。

## <a name="see-also"></a>関連項目

その他の関連情報については、次の情報を参照してください。

|コンテンツの種類|参考資料|
|------------------|----------------|
|**製品評価**|[Windows Server での DFS 名前空間と DFS レプリケーションの新機能](https://technet.microsoft.com/library/dn281957(v=ws.11).aspx)|
|**展開**|[DFS 名前空間のスケーラビリティに関する考慮事項](http://blogs.technet.com/b/filecab/archive/2012/08/26/dfs-namespace-scalability-considerations.aspx)|
|**運用**|[DFS 名前空間: よく寄せられる質問](http://technet.microsoft.com/library/ee404780.aspx)|
|**コミュニティ リソース**|[ファイル サービスとストレージに関する TechNet フォーラム](http://social.technet.microsoft.com/forums/winserverfiles/threads/)|
|**プロトコル**|[ファイル サービス Windows Server プロトコル](http://msdn.microsoft.com/library/cc239875.aspx)|
|**関連テクノロジ**| [フェールオーバー クラスタリング](../../failover-clustering/failover-clustering-overview.md)|