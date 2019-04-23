---
title: デスクトップ ホスティング サービス
description: デスクトップ ホスティング サービスのコンポーネントについて説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 07/06/2018
ms.tgt_pltfrm: na
ms.topic: article
author: heidilohr
manager: dougkim
ms.openlocfilehash: adbb9fd69bc61d2e877cadb0484a4e42093f262a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840473"
---
# <a name="desktop-hosting-service"></a>デスクトップ ホスティング サービス

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

この記事で示されますサービスのコンポーネントをホストしているデスクトップの詳細。

## <a name="tenant-environment"></a>テナント環境

」の説明に従って[リモート デスクトップ サービス ロール](rds-roles.md)、各ロールは、テナント環境で異なる役割を果たします。

プロバイダーのデスクトップ ホスティング サービスは、分離されたテナント環境のセットとして実装されます。 各テナントの環境は、ストレージ コンテナーを一連の仮想マシン、および分離された virtual network 上のすべての通信、Azure サービスの組み合わせで構成されます。 各仮想マシンには、1 つまたは複数のテナントのホストされたデスクトップ環境を構成するコンポーネントが含まれています。 次のサブセクションでは、各テナントのホストされたデスクトップ環境を構成するコンポーネントについて説明します。

## <a name="active-directory-domain-services"></a>Active Directory Domain Services

Active Directory Domain Services (AD DS) は、テナントのユーザーがデスクトップと、ワークロードを実行するアプリケーションにサインインできるように、ドメインおよびフォレストの情報を提供します。 これによりを設定するか、必要なファイル共有と Windows アプリケーションのために必要なデータベースに接続することもできます。

テナントのフォレストでは、プロバイダーの管理フォレストと信頼関係は必要ありません。 ドメイン管理者アカウントを設定したりできますでテナントのドメインを利用する (システム状態を監視し、ソフトウェア更新プログラムの適用) など、テナントの環境で管理タスクを実行して、プロバイダーの技術担当者を許可するにはトラブルシューティングと構成。

AD DS の展開に複数の方法はあります。

1. テナントの仮想ネットワーク環境で Azure Active Directory Domain Services を有効にします。 これにより、ユーザーと Azure AD 内に存在するグループに基づいて、テナントの AD DS のマネージ インスタンスが作成されます。
2. テナントの仮想ネットワーク環境でのスタンドアロンの AD DS サーバーを設定します。 これにより、すべての仮想マシンで実行されている AD DS インスタンスのフル コントロール。
3. テナントのオンプレミスの AD DS サーバーへのサイト対サイト VPN 接続を作成します。 これにより、その既存の AD DS インスタンスに接続し、ユーザー、グループ、組織単位、およびなどの重複を減らすには、テナントができます。

詳しくは、次の記事をご覧ください。

* [Azure Active Directory Domain Services のドキュメント](https://docs.microsoft.com/azure/active-directory-domain-services/)
* [デスクトップ ホスティング参照アーキテクチャのガイド Windows Server 2012 r2](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)
* [Azure portal でのサイト対サイト接続を作成します。](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)

## <a name="sql-database"></a>SQL データベース (SQL database)

高可用性の SQL database は、ホスト サーバーへの現在のユーザーの接続のマッピングなどの展開情報を格納するリモート デスクトップ接続ブローカーによって使用されます。

SQL データベースを展開する複数の方法はあります。

1. テナントの環境では、Azure SQL Database を作成します。 これを実行するサーバー自体を管理する必要がありません冗長 SQL database の機能を提供します。 これによりインフラストラクチャに投資する代わりに使用する何に対して課金することもできます。
2. SQL Server AlwaysOn クラスターを作成します。 これにより、既存の SQL Server インフラストラクチャを利用することができ、SQL Server インスタンスを完全に制御できます。

高可用性 SQL データベースのインフラストラクチャをセットアップする方法の詳細については、次の記事を参照してください。

* [Azure SQL Database サービスとは何ですか。](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview)
* [可用性グループ (SQL Server) の作成と構成](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server?view=sql-server-2017)します。
* [展開に RD 接続ブローカー サーバーを追加し、高可用性構成](rds-connection-broker-cluster.md)します。

## <a name="file-server"></a>ファイル サーバー

ファイル サーバーは、共有フォルダーを指定するのに、サーバー メッセージ ブロック (SMB) 3.0 プロトコルを使用します。 これらの共有フォルダーは、作成し、ユーザー プロファイル ディスク ファイル (.vhdx) にデータをバックアップし、ユーザーがテナントのクラウド サービス内で他のデータを共有できるように保存に使用されます。

ファイル サーバーをデプロイする仮想マシンを Azure データ ディスクが接続され、共有フォルダーで構成されている必要があります。 Azure データ ディスクを使用して、ライト スルー キャッシュで、仮想マシンが再起動されるたびに、ディスクへの書き込みが消去されるしないことを保証します。

小さなテナントは、ファイル サーバーを組み合わせることでコストを削減することができますと[RD ライセンスのロール](rds-roles.md#remote-desktop-licensing)テナントの環境で単一の仮想マシンにします。

詳しくは、次の記事をご覧ください。

* [Windows Server でのストレージ](../../storage/storage.md)
* [Azure portal で Windows VM を管理対象データ ディスクを接続する方法](https://docs.microsoft.com/azure/virtual-machines/windows/attach-managed-disk-portal?toc=%2Fazure%2Fvirtual-machines%2Fwindows%2Fclassic%2Ftoc.json)

### <a name="user-profile-disks"></a>ユーザー プロファイル ディスク

ユーザー プロファイル ディスクが 1 つのコレクションで、RD セッション ホスト サーバー上のセッションにサインインしているときに、個人の設定とファイルの保存を許可し、別にサインインするときに、同じ設定とファイルをアクセス[RD セッション ホスト](rds-roles.md#remote-desktop-session-host)コレクション内のサーバー。 ユーザーが初めてサインインすると、テナントのファイル サーバーは、ユーザーが現在接続している RD セッション ホスト サーバーにマウントするユーザー プロファイル ディスクを作成します。 各後続でサインイン、ユーザー プロファイル ディスクが、適切な RD セッション ホスト サーバーにマウントされており、各にマウントが解除サインアウトします。ユーザーは、プロファイル ディスクの内容にアクセスできます。