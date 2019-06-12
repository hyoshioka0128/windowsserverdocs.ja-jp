---
Title: 記憶域の移行サービスの概要
description: 記憶域の移行サービスでは、Windows Server の新しいバージョンにサーバーを移行するやすくなります。 サーバー上のデータのインベントリを作成し、新しいサーバーにデータと構成を転送するためのグラフィカル ツールを提供します-アプリやユーザーが何も変更することがなく。
author: jasongerend
ms.author: jgerend
manager: elizapo
ms.date: 05/21/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage
ms.openlocfilehash: ce4cbdc291d98a180ee6f5b597d322620fa1b19f
ms.sourcegitcommit: 48bb3e5c179dc520fa879b16c9afe09e07c87629
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66453172"
---
# <a name="storage-migration-service-overview"></a>記憶域の移行サービスの概要

>適用対象:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server (半期チャネル)

記憶域の移行サービスでは、Windows Server の新しいバージョンにサーバーを移行するやすくなります。 サーバー上のデータのインベントリを作成し、新しいサーバーにデータと構成を転送するためのグラフィカル ツールを提供します-アプリやユーザーが何も変更することがなく。

このトピックでは、記憶域の移行サービスを使用する、移行プロセスのしくみ、およびはソースと移行先サーバー用の要件について説明します。

## <a name="why-use-storage-migration-service"></a>記憶域の移行サービスを使用する理由

新しいハードウェアまたは仮想マシンに移行するサーバー (または多数のサーバー) ができましたので、記憶域の移行サービスを使用します。 記憶域の移行サービスは、次の手順に従ってように設計されています。

- 複数のサーバーとそのデータをインベントリします。
- 移行元サーバーからファイル、ファイル共有、およびセキュリティの構成を迅速に転送します。
- 必要に応じてユーザーとアプリは、既存のデータへのアクセスに何も変更する必要があるないように、(経由で cutting とも呼ばれます)、ソース サーバーの id を引き継ぐ
- Windows Admin Center ユーザー インターフェイスから 1 つまたは複数の移行を管理します。

![移行元サーバーから移行先サーバー、Azure Vm、または Azure File Sync の構成 (&)、ファイルを移行する記憶域の移行サービスを示す図。](media/overview/storage-migration-service-diagram.png)

**図 1: 記憶域サービスの移行元および変換先**

## <a name="how-the-migration-process-works"></a>移行プロセスのしくみ

移行では、3 つの手順を示します。

1. **サーバーのインベントリ**ファイルと (図 2 に示されている) 構成に関する情報を収集します。
2. **(コピー) のデータを転送**移行先サーバーへの移行元サーバーからです。
3. **新しいサーバーへのカット オーバー** (省略可能)。<br>移行先サーバーは、アプリとユーザーが何も変更する必要があるないようにに、ソース サーバーの元の id を想定します。 <br>移行元サーバーがまだ含まれている、同じメンテナンス状態の入力が常にあるファイル (決してファイルを削除、移行元サーバーから) はユーザーとアプリを使用できません。 都合に合わせて、サーバーを解除できます。

![スキャンする準備ができて、サーバーを示すスクリーン ショット](media/migrate/inventory.png)
**図 2。記憶域の移行サービスがサーバーのインベントリ**

## <a name="requirements"></a>必要条件

記憶域の移行サービスを使用するには、次のものが必要。

- A**移行元サーバー**ファイルとデータを移行するには
- A**移行先サーバー**に移行する Windows Server 2019 を実行して、同様に機能が、約 50% が遅くなるは Windows Server 2016 および Windows Server 2012 R2
- **Orchestrator サーバー**移行を管理する Windows Server 2019 を実行しています。  <br>場合は、いくつかのサーバーのみを移行して、Windows Server 2019 が実行されているサーバーのいずれか、オーケストレーターとしてを使用できます。 多くのサーバーを移行する場合は、別の orchestrator サーバーの使用をお勧めします。
- A **PC またはを実行するサーバー [Windows Admin Center](../../manage/windows-admin-center/understand/windows-admin-center.md)** を PowerShell を使用して、移行を管理する場合を除き、記憶域の移行サービスのユーザー インターフェイスを実行します。 Windows Admin Center と Windows Server 2019 バージョン両方以上でなければなりませんバージョンは 1809 します。

強くお勧めする orchestrator および変換先のコンピューターは、少なくとも 2 つのコアまたは 2 つの Vcpu と少なくとも 2 GB のメモリがあります。 インベントリと転送の操作は、複数のプロセッサとメモリをはるかに高速です。

### <a name="security-requirements"></a>セキュリティ要件

- 移行元コンピューターと orchestrator コンピューターの管理者である移行アカウントを指定します。
- セットアップ先のコンピューターと orchestrator コンピューターの管理者である移行アカウントを指定します。
- Orchestrator コンピューターのファイルとプリンターの共有 (SMB で) ファイアウォール ルールを有効になっている必要があります*受信*します。
- ソースと変換先のコンピューターで次のファイアウォール規則を有効になっている必要があります*受信*(ただし、既に有効になっていることを必要があります)。
  - ファイルとプリンターの共有 (SMB 受信)
  - Netlogon サービス (NP で)
  - (DCOM で) Windows Management Instrumentation
  - Windows Management Instrumentation (WMI-In)
  
  > [!TIP]
  > Windows Server 2019 コンピューターに、記憶域の移行サービスのプロキシ サービスをインストールすると、自動的にコンピューターに必要なファイアウォール ポートを開きます。
- コンピューターは、Active Directory Domain Services ドメインに属している場合する必要がありますすべてフォレストに属している、同じです。 移行先サーバーも必要があります、移行元サーバーと同じドメイン内にカット オーバーする場合、先に送信元のドメイン名を転送する場合。 カット オーバー技術的には、ドメインにわたってが変換先の完全修飾ドメイン名は、ソースと異なるになります.

### <a name="requirements-for-source-servers"></a>移行元サーバーの要件

移行元サーバーには、次のオペレーティング システムのいずれかを実行する必要があります。

- Windows Server 半期チャネル
- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2
- Windows Server 2008
- Windows Server 2003 R2
- Windows Server 2003

オーケストレーターは、Windows Server バージョンが 1903 以降を実行している場合は、次の追加のソースの種類を移行できます。

- フェールオーバー クラスター
- Samba を使用して Linux サーバー。 次のテストしました。
    - 7.6 の red Hat Enterprise Linux、CentOS 7、8 Debian、Ubuntu 16.04 および 12.04.5、SUSE Linux Enterprise Server (SLES) 11 SP4
    - Samba 4.x, 3.6.x

### <a name="requirements-for-destination-servers"></a>移行先サーバーの要件

移行先サーバーには、次のオペレーティング システムのいずれかを実行する必要があります。

- Windows Server 半期チャネル
- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2

> [!TIP]
> Windows Server 2019 または Windows Server を実行している移行先サーバー、半期チャネルは 1809 またはそれ以降のバージョンでは、Windows Server の以前のバージョンの転送のパフォーマンス倍精度浮動小数点があります。 このパフォーマンスの向上では、ポートしていない場合は開くために必要なファイアウォールを開くことも、組み込みの記憶域の移行サービス プロキシ サービスを含めることが原因です。

## <a name="whats-new-in-storage-migration-service"></a>記憶域の移行サービスの新機能新機能

Windows Server、バージョンが 1903 が orchestrator サーバー上で実行すると、次の新機能を追加します。

- 新しいサーバーにローカル ユーザーとグループを移行します。
- フェールオーバー クラスターから記憶域を移行します。
- Samba を使用する Linux サーバーから記憶域を移行します。
- Azure File Sync を使用して Azure に移行された共有をより簡単に同期します。
- Azure などの新しいネットワークへの移行します。

## <a name="see-also"></a>関連項目

- [記憶域の移行サービスを使用してファイル サーバーを移行します。](migrate-data.md)
- [よく寄せられる質問 (FAQ) の記憶域の移行サービス](faq.md)
- [記憶域の移行サービスの既知の問題](known-issues.md)
