---
title: Windows Admin Center を使用して Azure Virtual Machines をデプロイする
description: Windows Admin Center を使用した Azure 仮想マシンのデプロイ。 Windows Admin Center で管理されているシナリオの一部としての Azure 仮想マシンの構成。
ms.technology: manage
ms.topic: article
author: nedpyle
ms.author: nedpyle
manager: jgerend
ms.date: 01/28/2020
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 2249a69f60fe87758c74a58aa13b47124da41361
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80319372"
---
# <a name="deploy-azure-virtual-machines-from-within-windows-admin-center"></a>Windows Admin Center 内から Azure 仮想マシンをデプロイする

>適用対象:Windows Admin Center、Windows Admin Center プレビュー

Windows Admin Center バージョン1910では、Azure 仮想マシンをデプロイできます。 これにより、VM の展開は、Windows Admin Center の管理されたワークロード ([記憶域の移行サービス](../../../storage/storage-migration-service/overview.md)や[記憶域レプリカ](../../../storage/storage-replica/storage-replica-overview.md)など) に統合されます。 ワークロードをデプロイする前に手動で Azure Portal で新しいサーバーと Vm を作成するのではなく、必要な手順と構成がない場合もあります。 Windows Admin Center では、Azure VM のデプロイ、ストレージの構成、ドメインへの参加、役割のインストールを行うことができます。次に、分散システムを設定します。 Windows Admin Center の [接続] ページからワークロードを使用せずに、新しい Azure Vm をデプロイすることもできます。

Windows Admin Center では、さまざまな Azure サービスも管理します。 [Windows Admin Center で利用できる Azure 統合オプションの詳細については、こちらを参照して](../plan/azure-integration-options.md)ください。

## <a name="scenarios"></a>シナリオ

Windows Admin Center バージョン 1910 Azure VM の展開では、次のシナリオがサポートされています。

- [記憶域移行サービス](../../../storage/storage-migration-service/overview.md)
- [記憶域レプリカ](../../../storage/storage-replica/storage-replica-overview.md)
- [新しいスタンドアロンサーバー (ロールなし)](index.md#extend-on-premises-capacity-with-azure)

## <a name="requirements"></a>要件

Windows Admin Center 内から新しい Azure VM を作成するには、次のものが必要です。

- [Azure サブスクリプション](https://azure.microsoft.com)。
- [Azure に登録されている Windows Admin Center ゲートウェイ](azure-integration.md)
- 作成アクセス許可がある既存の[Azure リソースグループ](https://docs.microsoft.com/azure/azure-resource-manager/management/overview)。
- 既存の[Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview)とサブネット。
- 仮想ネットワークとサブネットに関連付けられた[Azure Express Route](https://azure.microsoft.com/services/expressroute/)または[azure VPN ソリューション](https://azure.microsoft.com/services/vpn-gateway/)。 Azure VM からオンプレミスのクライアント、ドメインコントローラー、Windows Admin Center コンピューター、およびワークロードデプロイの一部としてこの VM と通信する必要があるすべてのサーバーへの接続を可能にします。 たとえば、Storage Migration Service を使用してストレージを Azure VM に移行するには、orchestrator コンピューターとソースコンピューターが、移行先の Azure VM に接続できる必要があります。

## <a name="usage"></a>使用法

Azure VM のデプロイの手順とウィザードは、シナリオによって異なります。 全体的なシナリオの詳細については、ワークロードのドキュメントを確認してください。

### <a name="deploying-azure-vms-as-part-of-storage-migration-service"></a>Storage Migration Service の一部としての Azure Vm のデプロイ

1. Windows Admin Center 内の*記憶域移行サービス*ツールから、1つまたは複数の移行元サーバーのインベントリを実行します。
2. *データ転送*フェーズが完了したら、[*変換先の指定*] ページで **[新しい Azure VM の作成]** を選択し、 **[VM の作成]** をクリックします。<br><br>
これにより、移行先として Windows Server 2012 R2、Windows Server 2016、または Windows Server 2019 の Azure VM を選択するステップバイステップの作成ツールが開始されます。 Storage Migration Service は、ソースに合わせて推奨される VM サイズを提供しますが、 **[すべてのサイズを表示]** をクリックして上書きすることができます。
<br><br>ソースサーバーのデータは、管理ディスクとそのファイルシステムを自動的に構成するため、および新しい Azure VM を Active Directory ドメインに参加させるためにも使用されます。 VM が Windows Server 2019 (推奨) の場合、Windows Admin Center では、Storage Migration Service プロキシ機能がインストールされます。 Azure VM を作成すると、Windows Admin Center は通常のストレージ移行サービスの転送ワークフローに戻ります。  

Storage Migration Service を使用して Azure Vm に移行する方法を示すビデオを次に示します。

> [!VIDEO https://www.youtube-nocookie.com/embed/k8Z9LuVL0xQ] 

### <a name="deploying-azure-vms-as-part-of-storage-replica"></a>ストレージレプリカの一部としての Azure Vm のデプロイ

1. Windows Admin Center 内の*記憶域レプリカ*ツールの [*パートナーシップ*] タブで、 **[新規作成]** を選択し、[*別のサーバーとのレプリケート*] で **[新しい Azure VM を使用]** する を選択し、 **[次へ]** を選択します。
2. 移行元サーバーの情報とレプリケーショングループ名を指定し、 **[次へ]** を選択します。<br><br>
これにより、移行元のターゲットとして Windows Server 2016 または Windows Server 2019 Azure VM が自動的に選択されるプロセスが開始されます。 Storage Migration Service では、ソースに一致する VM サイズが推奨されますが、 **[すべてのサイズを表示]** を選択してこれを上書きできます。 インベントリデータは、管理ディスクとそのファイルシステムを自動的に構成するため、および新しい Azure VM を Active Directory ドメインに参加させるために使用されます。 
3. Windows Admin Center で Azure VM を作成した後、レプリケーショングループ名を入力し、 **[作成]** を選択します。 その後、Windows Admin Center は、データの保護を開始するための通常の記憶域レプリカ初期同期プロセスを開始します。

ストレージレプリカを使用して Azure Vm にレプリケートする方法を示すビデオを次に示します。

> [!VIDEO https://www.youtube-nocookie.com/embed/_VqD7HjTewQ] 

### <a name="deploying-a-new-standalone-azure-vm"></a>新しいスタンドアロン Azure VM のデプロイ

1. Windows Admin Center 内の [*すべての接続*] ページで、 **[追加]** を選択します。
2. [ *AZURE VM* ] セクションで、 **[新規作成]** を選択します。<br><br> これにより、Windows Server 2012 R2、Windows Server 2016、または Windows Server 2019 の Azure VM を選択し、サイズを選択し、管理ディスクを追加し、必要に応じて Active Directory ドメインに参加するためのステップバイステップ作成ツールが開始されます。

Windows Admin Center を使用して Azure Vm を作成する方法を示すビデオを次に示します。

> [!VIDEO https://www.youtube-nocookie.com/embed/__A8J9aC_Jk] 
