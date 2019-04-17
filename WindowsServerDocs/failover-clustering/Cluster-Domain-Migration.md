---
title: クロス 2019/Windows Server 2016 でのドメインのクラスター移行
ms.prod: windows-server-threshold
ms.manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.date: 01/18/2019
description: この記事では、Windows Server 2019 クラスターの 1 つのドメインの移動について説明します。
ms.localizationpriority: medium
ms.openlocfilehash: bcfd458c94d33820f434cde3313dc069fc42ffd9
ms.sourcegitcommit: 21677706eb85cb1396c1f40bf443146c09ef1b0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "9042036"
---
# フェールオーバー クラスター ドメインへの移行

> 適用対象: Windows Server 2019、Windows Server 2016

このトピックでは、移動中の Windows Server フェールオーバーの概要を説明が別の 1 つのドメインからクラスターを提供します。

## ドメイン間で移行する理由

クラスターを 1 つの doamin から別に移行する必要があるいくつかのシナリオがあります。

- 人物については、CompanyB と結合し、人物についてドメインのすべてのクラスターに移動する必要があります。
- クラスターがメインのデータ センターに組み込まれているし、リモートの場所に出荷
- クラスターは、ワークグループ クラスターとしてビルドされ、ドメインの一部にする必要があります。
- クラスターは、ドメイン クラスターとしてビルドされ、ワークグループの一部にする必要があります。
- クラスターを別の会社の 1 つの領域に移動し、別のサブドメイン

Microsoft では、アプリケーションの基になる操作がサポートされていない場合に、1 つのドメインからリソースを別に移動しようとしています。 管理者のためのサポートを提供されていません。 たとえば、Microsoft では、Microsoft Exchange サーバーを 1 つのドメイン間で移動しようとしています。 管理者のためのサポートを提供されていません。

   > [!WARNING]
   > クラスターを移動する前に、クラスター内のすべての共有記憶域の完全なバックアップを実行することをお勧めします。

## Windows Server 2016 以前のバージョン

Windows Server 2016 と以前では、クラスター サービスには 1 つのドメイン間を移動する機能がありませんでした。  これは、Active Directory ドメイン サービスで作成した仮想名が依存しているためです。   

## オプション

このような移動を行うためには、2 つのオプションがあります。

最初のオプションは、クラスターを破棄して、新しいドメインでそれを再構築する必要があります。

![破棄し、リビルド](media\Cross-Domain-Cluster-Migration\Cross-Cluster-Domain-Migration-1.gif)

アニメーションでは、このオプションは破棄を伴うの手順を実行します。

1. クラスターを破棄します。
2. 新しいドメインにノードのドメインのメンバーシップを変更します。
3. 更新されたドメインで、新しいクラスターを再作成します。  すべてのリソースを再作成しなくてもこの効果はします。

2 番目のオプションは、小さい破棄を伴うは、新しいクラスターを新しいドメインをビルドする必要がある追加のハードウェアが必要です。  クラスターが新しいドメイン内にある、リソースを移行するクラスター移行ウィザードを実行します。 このデータを移行しないこと、-[ストレージ移行サービス](../storage/storage-migration-service/overview.md)(したら、クラスターのサポートが追加されます) などのデータを移行する別のツールを使用する必要がありますに注意してください。

![ビルドし、移行](media\Cross-Domain-Cluster-Migration\Cross-Cluster-Domain-Migration-2.gif)

アニメーションを示すと、このオプションは破棄を伴うではありませんは、さまざまなハードウェアまたは既存のクラスターからノードが削除されたよりも必要があります。

1. ながら、古いクラスターが利用可能な新しい clusterin 新しいドメインを作成します。
2. [クラスター移行ウィザード](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754481(v=ws.10))を使用して、新しいクラスターにすべてのリソースを移行します。 アラーム、このデータはコピーされません、ので個別に実行する必要があります。
3. 使用停止または古いクラスターを破棄します。

両方のオプションでは、新しいクラスターが必要にすべての[クラスターに対応するアプリケーション](https://technet.microsoft.com/aa369082(v=vs.90))ドライバーはすべて最新の状態にし、可能性をすべてテストが適切に実行します。  これは、データも移動する必要がある場合の時間のかかるプロセスです。

## Windows Server 2019

Windows Server 2019 では、クロス クラスター ドメイン移行機能を導入しました。  これで、再構築する必要があるが不要になった、上に示したシナリオを行う簡単にできます。  

1 つのドメインからのクラスターの移動は、単純なプロセスです。 これを実現するには、2 つの新しい PowerShell コマンドレットがあります。

**新規 ClusterNameAccount** : Active Directory**削除 ClusterNameAccount**でクラスター名アカウントが作成されます: Active Directory からのクラスター名のアカウントの削除します。

これを実現するプロセスでは、ワークグループにし、新しいドメインには、1 つのドメインからクラスターを変更します。  破棄クラスター、クラスターを再構築、アプリケーションなどをインストールする必要は必須ではありません。 たとえば、次のようになります。

![移行](media\Cross-Domain-Cluster-Migration\Cross-Cluster-Domain-Migration-3.gif)

## 新しいドメインへのクラスターの移行

次の手順でクラスターを Contoso.com ドメインから新しい Fabrikam.com ドメインに移動されているが。  クラスター名が*CLUSCLUS*と*FS CLUSCLUS*と呼ばれるファイル サーバーの役割を使用しています。

1. 同じ名とパスワード、クラスター内のすべてのサーバーでローカル管理者アカウントを作成します。  これは、サーバーのドメイン間で移動中にログインする必要がありますです。
2. Active Directory アクセス許可をクラスター名オブジェクト (CNO)、仮想コンピューター オブジェクト (VCO) を持つドメイン ユーザーまたは管理者アカウントを持つ最初のサーバーにサインインでは、クラスター、および開いている PowerShell へのアクセスがあります。
3. クラスター ネットワーク名のすべてのリソースは、オフライン状態と実行を確認する、以下のコマンド。  このコマンド可能性のあるクラスター Active Directory オブジェクトが削除されます。

   ```PowerShell
   Remove-ClusterNameAccount -Cluster CLUSCLUS -DeleteComputerObjects
   ```
4. すべてのクラスター名に関連付けられているオブジェクトが削除された CNO と VCO コンピューターを確認するのにには、Active Directory ユーザーとコンピューターを使用します。

   > [!NOTE]
   > クラスター内のすべてのサーバーでクラスター サービスを停止し、サーバーがドメインを変更するときに再起動する場合、クラスター サービスの開始しないように、手動にサービスのスタートアップの種類を設定することをお勧めします。

   ```PowerShell
   Stop-Service -Name ClusSvc

   Set-Service -Name ClusSvc -StartupType Manual
   ```

5. ワークグループ サーバーのドメインのメンバーシップを変更、サーバーを再起動する、サーバーは、ドメインに参加させ、新しい、およびをもう一度再起動します。
6. サーバーは、新しいドメインでは後で、ドメイン ユーザーまたは管理者アカウントを Active Directory のアクセス許可オブジェクトを作成するには、クラスターへのアクセスには、サーバーにサインインし、PowerShell を開きます。 クラスター サービスを開始し、自動バックアップに設定します。

   ```PowerShell
   Start-Service -Name ClusSvc

   Set-Service -Name ClusSvc -StartupType Automatic
   ```
7. オンライン状態に、クラスター名とその他のすべてのクラスター リソースのネットワーク名を表示します。

   ```PowerShell
   Start-ClusterResource -Name "Cluster Name"

   Start-ClusterResource -Name FS-CLUSCLUS
   ```

8. クラスターが関連付けられている active directory オブジェクトを使用して新しいドメインの一部を変更します。 これを行うには、次に示しますコマンドとネットワーク名のリソースは、オンライン状態である必要があります。  このコマンドが実行されますが、Active Directory 内の名前のオブジェクトを再作成します。

   ```PowerShell
   New-ClusterNameAccount -Name CLUSTERNAME -Domain NEWDOMAINNAME.com -UpgradeVCOs
   ```

    注: ネットワーク名 (つまり、HYPER-V を使用したクラスター仮想マシンのみ) を持つその他のグループを用意していない場合、UpgradeVCOs パラメーター スイッチは必要ありません。

9. 新しいドメインを確認し、関連付けられたコンピューター オブジェクトが作成されたことを確認するには、Active Directory ユーザーとコンピューターを使用します。 、している場合は、グループをオンラインで残りのリソースを表示します。

   ```PowerShell
   Start-ClusterGroup -Name "Cluster Group"

   Start-ClusterGroup -Name FS-CLUSCLUS
   ```

## 既知の問題

新しい USB 監視機能を使用している場合、新しいドメインをクラスターに追加することはできません。  理由は、ファイル共有監視の種類が認証に Kerberos を利用する必要があります。  クラスターをドメインに追加する前に [なし] に監視を変更します。  完了すると、USB 監視を再作成します。  エラーが表示されますがします。

```
New-ClusternameAccount : Cluster name account cannot be created.  This cluster contains a file share witness with invalid permissions for a cluster of type AdministrativeAccesssPoint ActiveDirectoryAndDns. To proceed, delete the file share witness.  After this you can create the cluster name account and recreate the file share witness.  The new file share witness will be automatically created with valid permissions.
```

