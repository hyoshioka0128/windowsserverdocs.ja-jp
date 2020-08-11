---
title: デスクトップ ホスティング サービス
description: デスクトップ ホスティング サービスのコンポーネントについて説明します。
ms.author: helohr
ms.date: 07/06/2018
ms.topic: article
author: heidilohr
manager: lizross
ms.openlocfilehash: e1973bca8218f1ece287b03fee24486e95fe5492
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971639"
---
# <a name="desktop-hosting-service"></a>デスクトップ ホスティング サービス

>適用先:Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016

この記事では、デスクトップ ホスティング サービスのコンポーネントについて詳しく説明します。

## <a name="tenant-environment"></a>テナント環境

「[リモート デスクトップ サービス ロール](rds-roles.md)」で説明されているように、各ロールはテナント環境内で異なる役割を果たします。

プロバイダーのデスクトップ ホスティング サービスは、分離されたテナント環境のセットとして実装されます。 各テナントの環境は、ストレージ コンテナー、一連の仮想マシン、および Azure サービスの組み合わせで構成されます。これらはすべて、分離された仮想ネットワークを介して通信します。 各仮想マシンには、テナントのホストされたデスクトップ環境を構成する 1 つ以上のコンポーネントが含まれています。 次のサブセクションでは、各テナントのホストされたデスクトップ環境を構成するコンポーネントについて説明します。

## <a name="active-directory-domain-services"></a>[Active Directory Domain Services]

Active Directory Domain Services (AD DS) は、テナントのユーザーがデスクトップとアプリケーションにサインインしてワークロードを実行できるように、ドメインおよびフォレストの情報を提供します。 また、これにより、Windows アプリケーションに必要になる場合があるファイル共有とデータベースの設定や接続も行えます。

テナントのフォレストには、プロバイダーの管理フォレストとの信頼関係は不要です。 ドメイン管理者アカウントをテナントのドメインに設定して、プロバイダーの技術担当者がテナントの環境内で管理タスク (システム状態の監視、ソフトウェア更新プログラムの適用など) を実行したり、トラブルシューティングと構成を支援したりするようにすることが可能です。

AD DS の展開には複数の方法があります。

1. テナントの仮想ネットワーク環境で Azure Active Directory Domain Services を有効にします。 これにより、Azure AD に存在するユーザーとグループに基づいて、テナントの AD DS マネージド インスタンスが作成されます。
2. テナントの仮想ネットワーク環境でスタンドアロン AD DS サーバーを設定します。 これにより、仮想マシンで実行されている AD DS インスタンスを完全に制御できます。
3. テナントの構内にある AD DS サーバーへのサイト間 VPN 接続を作成します。 これにより、テナントがそれらの既存の AD DS インスタンスに接続できるので、ユーザー、グループ、組織単位などの重複を減らすことができます。

詳細については、以下の記事を参照してください。

* [Active Directory Domain Services のドキュメント](/azure/active-directory-domain-services/)
* [Windows Server 2012 R2 用のデスクトップ ホスティングの参照アーキテクチャ ガイド](/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)
* [Azure portal でサイト間接続を作成する](/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)

## <a name="sql-database"></a>SQL データベース

高可用性の SQL データベースは、展開情報 (ホスト サーバー対する現行ユーザーの接続のマッピングなど) を格納するために、リモート デスクトップ接続ブローカーによって使用されます。

SQL データベースの展開方法は複数あります。

1. テナントの環境で Azure SQL データベースを作成します。 これにより、自分でサーバー自体を管理しなくても、冗長 SQL データベースの機能を利用できます。 また、これにより、インフラストラクチャに投資する代わりに、消費した分だけ支払うことができます。
2. SQL Server AlwaysOn クラスターを作成します。 これにより、既存の SQL Server インフラストラクチャを利用し、SQL Server インスタンスを完全に制御できます。

高可用性の SQL データベースのインフラストラクチャを設定する方法の詳細については、次の記事をご覧ください。

* [Azure SQL Database サービスとは](/azure/sql-database/sql-database-technical-overview)
* [可用性グループの作成と構成 (SQL Server)](/sql/database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server?view=sql-server-2017)。
* [RD 接続ブローカー サーバーを展開に追加し、高可用性を構成する](rds-connection-broker-cluster.md)。

## <a name="file-server"></a>ファイル サーバー

ファイル サーバーは、サーバー メッセージ ブロック (SMB) 3.0 プロトコルを使用して共有フォルダーを提供します。 これらの共有フォルダーは、データをバックアップしたり、ユーザーがテナントのクラウド サービス内でデータを互いに共有できるようにしたりするためのユーザー プロファイル ディスク ファイル (.vhdx) の作成と格納に使用されます。

ファイル サーバーを展開する仮想マシンは、Azure データ ディスクがアタッチされ、共有フォルダーで構成されている必要があります。 Azure データ ディスクはライト スルー キャッシュを使用して、仮想マシンが再起動されてもディスクへの書き込みが消去されないことを保証します。

小規模テナントは、テナントの環境内の単一の仮想マシンでファイル サーバーと [RD ライセンスのロール](rds-roles.md#remote-desktop-licensing)を組み合わせることで、コストを削減できます。

詳細については、以下の記事を参照してください。

* [Windows Server の記憶域](../../storage/storage.yml)
* [Azure portal で Windows VM にマネージド データ ディスクをアタッチする方法](/azure/virtual-machines/windows/attach-managed-disk-portal?toc=/azure/virtual-machines/windows/classic/toc.json)

### <a name="user-profile-disks"></a>ユーザー プロファイル ディスク

ユーザー プロファイル ディスクを使用すると、ユーザーは、1 つのコレクション内の RD セッション ホスト サーバー上のセッションにサインインするときに個人用の設定とファイルを保存し、その後、そのコレクション内の別の [RD セッション ホスト](rds-roles.md#remote-desktop-session-host) サーバーにサインインするときに、同じ設定とファイルにアクセスできます。 ユーザーが初めてサインインすると、テナントのファイル サーバーによって、ユーザーが現在接続している RD セッション ホスト サーバーにマウントされるユーザー プロファイル ディスクが作成されます。 以降の各サインインでは、ユーザー プロファイル ディスクが適切な RD セッション ホスト サーバーにマウントされ、サインアウトのたびにマウント解除されます。そのユーザーのみがプロファイル ディスクの内容にアクセスできます。
