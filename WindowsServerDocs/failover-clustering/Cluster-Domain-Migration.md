---
title: Windows Server 2016/2019 でのクロスドメインクラスター移行
description: この記事では、Windows Server 2019 クラスターをあるドメインから別のドメインに移動する方法について説明します。
manager: eldenc
ms.topic: article
author: johnmarlin-msft
ms.author: johnmar
ms.date: 01/18/2019
ms.localizationpriority: medium
ms.openlocfilehash: 32f7e62fd08080f8b56c9c495f374d5c927454bb
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87990967"
---
# <a name="failover-cluster-domain-migration"></a>フェールオーバークラスタードメインの移行

> 適用先:Windows Server 2019、Windows Server 2016

このトピックでは、Windows Server フェールオーバークラスターをあるドメインから別のドメインに移動する方法の概要について説明します。

## <a name="why-migrate-between-domains"></a>ドメイン間で移行する理由

クラスターをある doamin から別のクラスターに移行する場合、いくつかのシナリオが必要です。

- 会社 b と合併し、すべてのクラスターを会社 a のドメインに移行する必要がある
- クラスターはメインデータセンターに構築され、リモートの場所に配布されます。
- クラスターはワークグループクラスターとして構築されており、現在はドメインに属している必要があります
- クラスターはドメインクラスターとして構築されており、ワークグループの一部である必要があります
- クラスターは別の場所に移動されており、別のサブドメインになっています

基になるアプリケーションの操作がサポートされていない場合は、ドメイン間でリソースを移動しようとする管理者に対して、Microsoft はサポートを提供しません。 たとえば、microsoft では、Microsoft Exchange server をあるドメインから別のドメインに移動しようとする管理者に対してサポートを提供していません。

   > [!WARNING]
   > クラスターを移動する前に、クラスター内のすべての共有記憶域の完全バックアップを実行することをお勧めします。

## <a name="windows-server-2016-and-earlier"></a>Windows Server 2016 以前

Windows Server 2016 以前では、クラスターサービスにドメイン間を移動する機能はありませんでした。  これは、Active Directory Domain Services と作成された仮想名への依存関係が増加したためです。

## <a name="options"></a>オプション

このような移動を行うために、2つのオプションがあります。

最初のオプションでは、クラスターを破棄し、新しいドメインで再構築します。

![破棄と再構築](media/Cross-Domain-Cluster-Migration/Cross-Cluster-Domain-Migration-1.gif)

アニメーションに示されているように、このオプションは、次の手順で破壊的です。

1. クラスターを破棄します。
2. ノードのドメインメンバーシップを新しいドメインに変更します。
3. 更新されたドメインの新規としてクラスターを再作成します。  これにより、すべてのリソースを再作成する必要があります。

2番目のオプションは破壊的ではありませんが、新しいクラスターを新しいドメインに構築する必要があるため、追加のハードウェアが必要になります。  クラスターが新しいドメインに追加されたら、クラスターの移行ウィザードを実行してリソースを移行します。 これはデータを移行しないことに注意してください。記憶域の移行[サービス](../storage/storage-migration-service/overview.md)(クラスターのサポートが追加された後) などの別のツールを使用してデータを移行する必要があります。

![ビルドと移行](media/Cross-Domain-Cluster-Migration/Cross-Cluster-Domain-Migration-2.gif)

アニメーションに示されているように、このオプションは破壊的ではありませんが、別のハードウェアまたは既存のクラスターのノードが削除されている必要があります。

1. 新しいドメインに新しい clusterin 作成し、以前のクラスターを使用できるようにします。
2. クラスターの[移行ウィザード](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754481(v=ws.10))を使用して、すべてのリソースを新しいクラスターに移行します。 リマインダーはデータをコピーしないため、別途行う必要があります。
3. 以前のクラスターを使用停止または破棄します。

どちらのオプションでも、新しいクラスターはすべての[クラスター対応アプリケーション](/previous-versions/windows/desktop/mscs/cluster-aware-applications)をインストールし、ドライバーをすべて最新の状態にして、すべてが正常に動作することを確認するためにテストすることが必要になる場合があります。  データも移動する必要がある場合は、この処理に時間がかかります。

## <a name="windows-server-2019"></a>Windows Server 2019

Windows Server 2019 では、クロスクラスタードメイン移行機能が導入されました。  ここで、上記のシナリオは簡単に実行でき、再構築の必要性は不要になりました。

1つのドメインからのクラスターの移動は、単純なプロセスです。 これを実現するには、2つの新しい PowerShell コマンドレットを使用します。

**新しい-ClusterNameAccount** –クラスター名アカウントを Active Directory 削除する **-clusternameaccount** –からクラスター名アカウントを削除し Active Directory

これを実現するには、クラスターを1つのドメインからワークグループに変更し、新しいドメインに戻します。  クラスターを破棄し、クラスターを再構築し、アプリケーションをインストールする必要はありません。 たとえば、次のようになります。

![移行](media/Cross-Domain-Cluster-Migration/Cross-Cluster-Domain-Migration-3.gif)

## <a name="migrating-a-cluster-to-a-new-domain"></a>クラスターを新しいドメインに移行する

次の手順では、クラスターを Contoso.com ドメインから新しい Fabrikam.com ドメインに移動します。  クラスター名は*CLUSCLUS* 、 *CLUSCLUS*というファイルサーバーの役割を持ちます。

1. クラスター内のすべてのサーバーに同じ名前とパスワードを持つローカル管理者アカウントを作成します。  これは、サーバーがドメイン間を移動している間にログインするために必要になる場合があります。
2. クラスター名オブジェクト (CNO) に対する Active Directory アクセス許可を持つドメインユーザーまたは管理者アカウントを使用して最初のサーバーにサインインし、仮想コンピューターオブジェクト (VCO) にクラスターへのアクセス権があり、PowerShell を開きます。
3. すべてのクラスターネットワーク名リソースがオフライン状態であることを確認してから、次のコマンドを実行してください。  このコマンドを実行すると、クラスターに存在する Active Directory オブジェクトが削除されます。

   ```PowerShell
   Remove-ClusterNameAccount -Cluster CLUSCLUS -DeleteComputerObjects
   ```
4. Active Directory ユーザーとコンピューター] を使用して、すべてのクラスター化された名前に関連付けられている CNO および VCO コンピューターオブジェクトが削除されていることを確認します。

   > [!NOTE]
   > クラスター内のすべてのサーバーでクラスターサービスを停止し、サービスのスタートアップの種類を手動に設定することをお勧めします。これにより、ドメインの変更中にサーバーを再起動してもクラスターサービスが開始されないようにすることができます。

   ```PowerShell
   Stop-Service -Name ClusSvc

   Set-Service -Name ClusSvc -StartupType Manual
   ```

5. サーバーのドメインメンバーシップをワークグループに変更し、サーバーを再起動して、サーバーを新しいドメインに参加させ、再起動します。
6. サーバーが新しいドメインに追加されたら、オブジェクトを作成するためのアクセス許可を持つドメインユーザーまたは管理者 Active Directory アカウントを使用してサーバーにサインインし、クラスターへのアクセス権を持ち、PowerShell を開きます。 クラスターサービスを開始し、[自動] に設定します。

   ```PowerShell
   Start-Service -Name ClusSvc

   Set-Service -Name ClusSvc -StartupType Automatic
   ```
7. クラスター名とその他のすべてのクラスターネットワーク名リソースをオンライン状態にします。

   ```PowerShell
   Start-ClusterResource -Name "Cluster Name"

   Start-ClusterResource -Name FS-CLUSCLUS
   ```

8. クラスターを、active directory オブジェクトに関連付けられた新しいドメインの一部になるように変更します。 これを行うには、次のコマンドを実行し、ネットワーク名リソースがオンライン状態である必要があります。  このコマンドでは、Active Directory で name オブジェクトを再作成します。

   ```PowerShell
   New-ClusterNameAccount -Name CLUSTERNAME -Domain NEWDOMAINNAME.com -UpgradeVCOs
   ```

    注: ネットワーク名を持つ追加のグループ (つまり、仮想マシンのみを持つ Hyper-v クラスター) がない場合は、-UpgradeVCOs パラメータースイッチは必要ありません。

9. Active Directory ユーザーとコンピューター] を使用して新しいドメインを確認し、関連付けられているコンピューターオブジェクトが作成されたことを確認します。 存在する場合は、グループ内の残りのリソースをオンラインにします。

   ```PowerShell
   Start-ClusterGroup -Name "Cluster Group"

   Start-ClusterGroup -Name FS-CLUSCLUS
   ```

## <a name="known-issues"></a>既知の問題

新しい USB 監視機能を使用している場合、クラスターを新しいドメインに追加することはできません。  理由は、ファイル共有監視の種類で認証に Kerberos を利用する必要があるということです。  クラスターをドメインに追加する前に、ミラーリング監視サーバーを [なし] に変更します。  完了したら、USB 監視を再作成します。  次のエラーが表示されます。

```
New-ClusternameAccount : Cluster name account cannot be created.  This cluster contains a file share witness with invalid permissions for a cluster of type AdministrativeAccesssPoint ActiveDirectoryAndDns. To proceed, delete the file share witness.  After this you can create the cluster name account and recreate the file share witness.  The new file share witness will be automatically created with valid permissions.
```