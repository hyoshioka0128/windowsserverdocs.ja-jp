---
title: クロス ドメイン 2019/Windows Server 2016 でのクラスターの移行
ms.prod: windows-server-threshold
ms.manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.date: 01/18/2019
description: この記事では、1 つのドメインから別の Windows Server 2019 クラスターの移動について説明します
ms.localizationpriority: medium
ms.openlocfilehash: bcfd458c94d33820f434cde3313dc069fc42ffd9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875943"
---
# <a name="failover-cluster-domain-migration"></a>フェールオーバー クラスターのドメインの移行

> 適用先:Windows Server 2019、Windows Server 2016

このトピックでは、別に 1 つのドメインからクラスターの移動の Windows Server フェールオーバーの概要を説明します。

## <a name="why-migrate-between-domains"></a>ドメイン間で移行する理由

いくつかのシナリオ別に 1 つ doamin からクラスターの移行が必要な場合があります。

- 人物については、CompanyB をマージし、人物についてのドメインのすべてのクラスターに移動する必要があります。
- クラスターが、メイン データ センターに組み込まれているし、リモートの場所への発送
- クラスターがワークグループ クラスターとして作成されており、ドメインの一部である必要があります。
- クラスターは、ドメインのクラスターとしてが作成されており、ワークグループの一部である必要があります。
- クラスターを別の会社の 1 つの領域に移動し、別のサブドメイン

Microsoft では、基になるアプリケーションの操作がサポートされていない場合は、別に 1 つのドメインからリソースを移動しようとする管理者にサポートを提供しません。 たとえば、Microsoft では、1 つのドメイン間で、Microsoft Exchange server を移動しようとする管理者にサポートを提供しません。

   > [!WARNING]
   > クラスターを移行する前に、クラスター内のすべての共有記憶域の完全バックアップを実行することをお勧めします。

## <a name="windows-server-2016-and-earlier"></a>Windows Server 2016 以前のバージョン

Windows Server 2016 以降では、クラスター サービスには、1 つのドメイン間を移動するの機能がありませんでした。  これは、Active Directory Domain Services で作成した仮想名への増加が原因でした。   

## <a name="options"></a>オプション

このような移動を行うには 2 つのオプションがあります。

最初のオプションは、クラスターを破棄して、新しいドメインでそれを再構築する必要があります。

![破棄および再構築](media\Cross-Domain-Cluster-Migration\Cross-Cluster-Domain-Migration-1.gif)

このオプションは、手順に破壊的なアニメーションが示すようにします。

1. クラスターを破棄します。
2. 新しいドメインに、ノードのドメイン メンバーシップを変更します。
3. 更新されたドメインで、新しいクラスターを再作成します。  すべてのリソースを再作成することが必要になるこれは。

2 番目のオプションは、小さい破壊的なは、新しいクラスターを新しいドメインをビルドする必要がある追加のハードウェアが必要です。  クラスターを新しいドメインには、リソースを移行するクラスターの移行ウィザードを実行します。 このデータを移行しないこと、-など、データを移行する別のツールを使用する必要がありますに注意してください[記憶域の移行サービス](../storage/storage-migration-service/overview.md)(したら、クラスターのサポートが追加されます)。

![ビルドおよび移行](media\Cross-Domain-Cluster-Migration\Cross-Cluster-Domain-Migration-2.gif)

アニメーションが示すように、このオプションは破壊的なではありませんは、別のハードウェアまたは既存のクラスターからノードのいずれかが削除されているよりも必要があります。

1. 以前のクラスターを利用しながら新しい clusterin、新しいドメインを作成します。
2. 使用して、[クラスターの移行ウィザード](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754481(v=ws.10))すべてのリソースを新しいクラスターに移行します。 アラームは、このデータはコピーされません、ため、個別に実行する必要があります。
3. 使用を停止または以前のクラスターを破棄します。

どちらのオプションで、新しいクラスターが必要にすべて[クラスター対応アプリケーション](https://technet.microsoft.com/aa369082(v=vs.90))、すべて最新のドライバーをインストールし、可能性があるテストを行うすべてが適切に実行します。  これは、データも移動する必要がある場合、時間のかかるプロセスです。

## <a name="windows-server-2019"></a>Windows Server 2019

Windows Server 2019、クラスターのクロス ドメインの移行機能を導入しました。  これで前に、示したシナリオを簡単に実施でき、再構築する必要があるが不要になった。  

1 つのドメインからのクラスターの移動は、単純なプロセスです。 これを行うには、2 つの新しい PowerShell コマンドレットがあります。

**新しい ClusterNameAccount** : Active Directory でクラスター名アカウントを作成します**削除 ClusterNameAccount** – クラスター名アカウントを Active Directory から削除します。

これを実現するプロセスでは、ワークグループには、新しいドメインには、1 つのドメインからクラスターを変更します。  クラスターの破棄、クラスターを再構築、アプリケーションなどをインストールする必要がある要件ではありません。 たとえば、このようなことになります。

![移行](media\Cross-Domain-Cluster-Migration\Cross-Cluster-Domain-Migration-3.gif)

## <a name="migrating-a-cluster-to-a-new-domain"></a>新しいドメインにクラスターの移行

次の手順でクラスターを Contoso.com ドメインから新しい Fabrikam.com ドメインに移動されるは。  クラスター名が*CLUSCLUS*と呼ばれるファイル サーバーの役割を使用して*FS CLUSCLUS*します。

1. 同じ名前と、クラスター内のすべてのサーバー上でパスワードを持つローカル管理者アカウントを作成します。  これは、サーバーはドメイン間で移動するときにログインする必要あります。
2. Active Directory のアクセス許可をクラスター名オブジェクト (CNO)、仮想コンピューター オブジェクト (VCO) を持つドメイン ユーザーまたは管理者アカウントを使用して最初のサーバーへのサインインには、PowerShell を開き、クラスターへのアクセスがあります。
3. すべてのクラスター ネットワーク名リソースが状態と実行をオフラインにしていることを確認、次のコマンド。  このコマンドは、クラスターがいる可能性のある Active Directory オブジェクトに削除されます。

   ```PowerShell
   Remove-ClusterNameAccount -Cluster CLUSCLUS -DeleteComputerObjects
   ```
4. Active Directory ユーザーとコンピューターを使用して、すべてのクラスター化された名前に関連付けられたオブジェクトが削除された CNO と VCO のコンピューターを確認します。

   > [!NOTE]
   > クラスター内のすべてのサーバー上でクラスター サービスを停止し、サーバーがドメインの変更中に再起動する場合、クラスター サービスが起動しないように、サービスのスタートアップの種類を手動に設定することをお勧めします。

   ```PowerShell
   Stop-Service -Name ClusSvc

   Set-Service -Name ClusSvc -StartupType Manual
   ```

5. ワークグループにサーバーのドメイン メンバーシップを変更、サーバーを再起動、サーバーを新しいドメインに参加およびをもう一度再起動します。
6. 新しいドメインのサーバーが表示されたら、Active Directory のアクセス許可オブジェクトを作成するには、クラスターにアクセスするドメイン ユーザーまたは管理者アカウントでサーバーにサインインし、PowerShell を開きます。 クラスター サービスを開始し、それを自動に設定します。

   ```PowerShell
   Start-Service -Name ClusSvc

   Set-Service -Name ClusSvc -StartupType Automatic
   ```
7. オンライン状態にクラスター名とその他のすべてのクラスター ネットワーク名リソースにもたらします。

   ```PowerShell
   Start-ClusterResource -Name "Cluster Name"

   Start-ClusterResource -Name FS-CLUSCLUS
   ```

8. 関連付けられている active directory オブジェクトを使用して新しいドメインの一部としてクラスターを変更します。 これを行うには、コマンドは以下は、ネットワーク名リソースがオンライン状態である必要があります。  このコマンドは、Active Directory で名前のオブジェクトを再作成します。

   ```PowerShell
   New-ClusterNameAccount -Name CLUSTERNAME -Domain NEWDOMAINNAME.com -UpgradeVCOs
   ```

    注: ネットワーク名 (つまり仮想マシンのみで、HYPER-V クラスター) とその他のグループがない - UpgradeVCOs パラメーター スイッチは不要です。

9. 新しいドメインを確認し、関連付けられたコンピューター オブジェクトが作成されたことを確認するには、Active Directory ユーザーとコンピューターを使用します。 場合は、グループをオンラインで残りのリソースを表示します。

   ```PowerShell
   Start-ClusterGroup -Name "Cluster Group"

   Start-ClusterGroup -Name FS-CLUSCLUS
   ```

## <a name="known-issues"></a>既知の問題

新しい USB ミラーリング監視サーバーの機能を使用している場合、新しいドメインにクラスターを追加することはできません。  推論としては、ファイル共有のミラーリング監視サーバーの種類が認証に Kerberos を利用する必要があります。  クラスターをドメインに追加する前に [なし] に、ミラーリング監視サーバーを変更します。  完了すると、USB のミラーリング監視サーバーを再作成します。  「エラーです。

```
New-ClusternameAccount : Cluster name account cannot be created.  This cluster contains a file share witness with invalid permissions for a cluster of type AdministrativeAccesssPoint ActiveDirectoryAndDns. To proceed, delete the file share witness.  After this you can create the cluster name account and recreate the file share witness.  The new file share witness will be automatically created with valid permissions.
```

