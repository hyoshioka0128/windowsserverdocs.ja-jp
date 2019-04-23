---
title: デスクトップ ホスティング環境を理解します。
description: Azure IaaS を使用して、RDS deployhment の概要です。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 08/01/2016
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: 880fc8f9fa2db5ec56d2117e02c069650c61584a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877923"
---
# <a name="understanding-the-desktop-hosting-environment"></a>デスクトップ ホスティング環境を理解します。

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

次の情報には、サービスをホストしているデスクトップのコンポーネントについて説明します。  
  
## <a name="tenant-environment"></a>テナント環境  
プロバイダーのデスクトップ ホスティング サービスは、分離されたテナント環境のセットとして実装されます。 各テナントの環境は、ストレージ コンテナーを一連の仮想マシン、および分離された virtual network 上のすべての通信、Azure サービスの組み合わせで構成されます。 各仮想マシンには、1 つまたは複数のテナントのホストされたデスクトップ環境を構成するコンポーネントが含まれています。 次のサブセクションでは、各テナントのホストされたデスクトップ環境を構成するコンポーネントについて説明します。

## <a name="remote-desktop-services"></a>リモート デスクトップ サービス
デスクトップ ホスティング環境では、次のリモート デスクトップ サービスの役割はさまざまな仮想マシン間でインストールされます。

  - リモート デスクトップ接続ブローカー
  - リモート デスクトップ ゲートウェイ
  - リモート デスクトップ ライセンス
  - リモート デスクトップ セッション ホスト
  - リモート デスクトップ Web アクセス

これらのロールと相互にやり取りする方法のそれぞれの詳細についてを参照してください、[理解 RDS 役割](Understanding-RDS-roles.md)ドキュメント。
  
##  <a name="azure-active-directory-domain-services"></a>(Azure)Active Directory Domain Services  
接続し、azure デスクトップ ホスティング環境の Active Directory Domain Services (AD DS) を管理する複数の方法はあります。

1. AD DS 役割を実行して、テナントの環境での仮想マシンの作成します。
2. 既存の AD DS を使用するテナントのオンプレミス環境とサイト対サイト VPN 接続を作成します。
3. テナントの Azure Active Directory ベースのテナントの仮想ネットワークでドメインを作成する Azure AD Domain Services PaaS ロールを使用して、

リモート デスクトップ サービスでは、テナントの Active Directory 環境、ユーザー プロファイルの記憶域にアクセスを管理する必要がありますと、配置内で監視します。 標準の (Azure 以外の) AD DS を使用する場合、テナントのフォレストには、プロバイダーの管理フォレストと信頼関係は不要です。 ドメイン管理者アカウントを設定したりできますでテナントのドメインを利用する (システム状態を監視し、ソフトウェア更新プログラムの適用) など、テナントの環境で管理タスクを実行して、プロバイダーの技術担当者を許可するにはトラブルシューティングと構成。  
    
追加情報:  
[Azure Active Directory Domain Services のドキュメント](https://azure.microsoft.com/documentation/services/active-directory-ds/)  
[Azure の仮想ネットワークに新しい Active Directory フォレストをインストールします。](https://azure.microsoft.com/documentation/articles/active-directory-new-forest-virtual-machine/)  
[Azure Portal を使用してサイト対サイト VPN 接続を持つリソース マネージャー VNet を作成します。](https://azure.microsoft.com/documentation/articles/vpn-gateway-howto-site-to-site-resource-manager-portal/)  
  
## <a name="azure-sql-database"></a>Azure SQL データベース  
Azure SQL Database では、展開および完全な SQL Server Always-On クラスターを管理することがなく、リモート デスクトップ サービス展開を拡張するホスト。 Azure SQL Database は、エンド ホスト サーバーへの現在のユーザーの接続のマッピングなどの展開情報を格納するリモート デスクトップ接続ブローカーによって使用されます。 他の Azure サービスのように Azure SQL DB に依存して、消費モデルは、あらゆるサイズの展開に最適です。   
  
追加情報:  
[SQL Database とは何ですか。](https://azure.microsoft.com/documentation/articles/sql-database-technical-overview/)  
  
## <a name="azure-active-directory-application-proxy"></a>Azure Active Directory アプリケーション プロキシ  
Azure Active Directory アプリケーション プロキシは、有料 Sku の Azure Active Directory のユーザーが Azure のリバース プロキシ サービス経由で内部アプリケーションに接続できるで提供されるサービスです。 これにより、パブリック IP アドレスを使用してインターネットに公開される必要がないため、仮想ネットワーク内で非表示にする RD Web と RD ゲートウェイ エンドポイントです。 これには、ホスト側は、完全なデプロイを維持しながら、テナントの環境で仮想マシンの数を要約をさらにによりできます。
  
追加情報:  
[Azure AD アプリケーション プロキシを有効にします。](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-enable/)  
    
## <a name="file-server"></a>ファイル サーバー  
ファイル サーバーは、サーバー メッセージ ブロック (SMB) 3.0 プロトコルを使用して、共有フォルダーを提供します。 作成してデータのバックアップをユーザー プロファイル ディスク ファイル (.vhdx) を格納して、テナントの仮想ネットワーク内の他のユーザーとデータを共有する場所をユーザーに許可するのには、共有フォルダーが使用されます。
  
ファイル サーバーを展開するために使用する VM を Azure データ ディスクが接続され、共有フォルダーで構成されている必要があります。 Azure データ ディスクを使用して、ライト スルー キャッシュをディスクに書き込むことが保証されますが、VM の再起動の間で保持します。  
  
小規模のテナントのテナントの環境で 1 つの仮想マシン上の RD 接続ブローカー、RD ライセンスの役割を実行する仮想マシンとファイル サーバーを組み合わせることによって、コストを削減できます。  
  
追加情報  
[ファイル サービスおよび記憶域サービスの概要](https://technet.microsoft.com/library/hh831487.aspx)  
[仮想マシンにデータ ディスクをアタッチする方法](http://www.windowsazure.com/manage/windows/how-to-guides/attach-a-disk/)  
  
### <a name="user-profile-disks"></a>ユーザー プロファイル ディスク  
ユーザー プロファイル ディスクのコレクションでは、RD セッション ホスト サーバー上のセッションにサインインしているときに、個人の設定とファイルの保存を許可し、同じ設定とファイルへのアクセス、コレクション内の別の RD セッション ホスト サーバーにサインインするときにします。 ユーザーが初めてサインインするときに、テナントのファイル サーバーでユーザー プロファイル ディスクが作成され、ユーザーが接続されている RD セッション ホスト サーバーにそのディスクがマウントされています。 各以降、サインイン、適切な RD セッション ホスト サーバーにユーザー プロファイル ディスクがマウントされてし、各にサインアウト、ことはできませんアンマウントします。 プロファイル ディスクの内容は、そのユーザーのみがアクセスできます。  
  


