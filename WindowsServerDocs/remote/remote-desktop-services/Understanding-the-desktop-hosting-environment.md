---
title: デスクトップ ホスティング環境の概要
description: Azure IaaS を使用した RDS 展開の概要。
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 08/01/2016
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: 8fdebcad1370e06c19752944e85363c714f1fbcd
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "80854695"
---
# <a name="understanding-the-desktop-hosting-environment"></a>デスクトップ ホスティング環境の概要

>適用先:Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016

ここでは、デスクトップ ホスティング サービスのコンポーネントについて説明します。  
  
## <a name="tenant-environment"></a>テナント環境  
プロバイダーのデスクトップ ホスティング サービスは、分離された一連のテナント環境として実装されます。 各テナントの環境は、ストレージ コンテナー、一連の仮想マシン、および Azure サービスの組み合わせで構成されます。これらはすべて、分離された仮想ネットワークを介して通信します。 各仮想マシンには、テナントのホストされたデスクトップ環境を構成する 1 つ以上のコンポーネントが含まれています。 以降のサブセクションでは、各テナントのホストされたデスクトップ環境を構成するコンポーネントについて説明します。

## <a name="remote-desktop-services"></a>リモート デスクトップ サービス
デスクトップ ホスティング環境では、さまざまな仮想マシン間で次のリモート デスクトップ サービス ロールがインストールされます。

  - リモート デスクトップ接続ブローカー
  - リモート デスクトップ ゲートウェイ
  - リモート デスクトップ ライセンス
  - リモート デスクトップ セッション ホスト
  - リモート デスクトップ Web アクセス

これらの各ロールの詳しい説明と、それらがどのように連携するかについては、[RDS ロールの概要](Understanding-RDS-roles.md)に関するドキュメントをご覧ください。
  
##  <a name="azure-active-directory-domain-services"></a>(Azure) Active Directory Domain Services  
Azure のデスクトップ ホスティング環境の Active Directory Domain Services (AD DS) に接続し、管理する方法は複数あります。

1. AD DS ロールを実行するテナントの環境に仮想マシンを作成する。
2. テナントのオンプレミス環境とのサイト間 VPN 接続を作成し、既存の AD DS を使用する。
3. Azure AD Domain Services PaaS ロールを使用する。これにより、テナントの Azure Active Directory に基づいてテナントの仮想ネットワークにドメインが作成されます。

リモート デスクトップ サービスを使用する場合、テナントには、環境へのアクセス、ユーザー プロファイルの保管、および展開内の監視を管理する Active Directory が必要です。 標準の (Azure 以外の) AD DS を使用する場合、テナントのフォレストには、プロバイダーの管理フォレストとの信頼関係は不要です。 プロバイダーの技術担当者がテナントの環境内で管理タスク (システム状態の監視、ソフトウェア更新プログラムの適用など) を実行できるようにしたり、トラブルシューティングと構成を支援したりするために、ドメイン管理者アカウントがテナントのドメインに設定されることがあります。  
    
追加情報:  
[Active Directory Domain Services のドキュメント](https://azure.microsoft.com/documentation/services/active-directory-ds/)  
[Azure 仮想ネットワークに新しい Active Directory フォレストをインストールする](https://azure.microsoft.com/documentation/articles/active-directory-new-forest-virtual-machine/)  
[Azure Portal を使用してリソース マネージャー VNet とサイト間 VPN 接続を作成する](https://azure.microsoft.com/documentation/articles/vpn-gateway-howto-site-to-site-resource-manager-portal/)  
  
## <a name="azure-sql-database"></a>Azure SQL Database  
Azure SQL Database では、完全な SQL Server Always-On クラスターを展開および管理することなく、ホスト側でリモート デスクトップ サービスの展開を拡張することができます。 Azure SQL Database は、エンド ホスト サーバーへの現在のユーザーの接続のマッピングなどの展開情報を格納するために、リモート デスクトップ接続ブローカーによって使用されます。 Azure SQL DB は、他の Azure サービスと同じように従量課金モデルを採用しているため、どのサイズの展開にも適しています。   
  
追加情報:  
[SQL Database とは](https://azure.microsoft.com/documentation/articles/sql-database-technical-overview/)  
  
## <a name="azure-active-directory-application-proxy"></a>Azure Active Directory アプリケーション プロキシ  
Azure Active Directory アプリケーション プロキシは、ユーザーが Azure 独自のリバース プロキシ サービス経由で内部アプリケーションに接続できるようにする、Azure Active Directory の有料 SKU で提供されるサービスです。 これにより、RD Web と RD ゲートウェイ エンドポイントを仮想ネットワーク内に隠し、パブリック IP アドレスによってインターネットに公開する必要性をなくすことができます。 さらにホスト側は、完全な展開を維持しながら、テナントの環境内の仮想マシンの数を減らすことができます。
  
追加情報:  
[Azure AD アプリケーション プロキシの有効化](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-enable/)  
    
## <a name="file-server"></a>ファイル サーバー  
ファイル サーバーは、サーバー メッセージ ブロック (SMB) 3.0 プロトコルを使用して共有フォルダーを提供します。 この共有フォルダーは、ユーザー プロファイル ディスク ファイル (.vhdx) を作成して格納するため、データをバックアップするため、およびテナントの仮想ネットワーク内のユーザー同士でデータを共有できるようにするために使用されます。
  
ファイル サーバーの展開に使用する VM は、Azure データ ディスクがアタッチされ、共有フォルダーで構成されている必要があります。 Azure データ ディスクではライトスルー キャッシュが使用されており、VM を再起動してもディスクへの書き込みが保持されます。  
  
小規模テナントの場合、テナントの環境内の 1 つの仮想マシン上で RD 接続ブローカーと RD ライセンスのロールを実行する仮想マシンとファイル サーバーを組み合わせることによって、コストを削減できます。  
  
追加情報  
[ファイル サービスおよび記憶域サービスの概要](https://technet.microsoft.com/library/hh831487.aspx)  
[仮想マシンにデータ ディスクをアタッチする方法](http://www.windowsazure.com/manage/windows/how-to-guides/attach-a-disk/)  
  
### <a name="user-profile-disks"></a>ユーザー プロファイル ディスク  
ユーザー プロファイル ディスクにより、ユーザーはコレクション内の RD セッション ホスト サーバー上のセッションにサインインしたときに個人用の設定とファイルを保存して、その後、そのコレクション内の別の RD セッション ホスト サーバーにサインインしたときにも同じ設定とファイルにアクセスできます。 ユーザーが初めてサインインすると、テナントのファイル サーバーにユーザー プロファイル ディスクが作成されて、ユーザーが接続している RD セッション ホスト サーバーにそのディスクがマウントされます。 それ以降のサインインのたびに、ユーザー プロファイル ディスクは適切な RD セッション ホスト サーバーにマウントされ、サインアウトのたびにマウント解除されます。 プロファイル ディスクの内容には、そのユーザーのみがアクセスできます。  
  


