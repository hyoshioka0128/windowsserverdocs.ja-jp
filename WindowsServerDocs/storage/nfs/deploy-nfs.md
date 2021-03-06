---
title: ネットワーク ファイル システムの展開
description: ネットワーク ファイル システムを展開する方法について説明します。
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: ab80b6d73a40256d5935635c9afc55b7c53727d3
ms.sourcegitcommit: 2977c707a299929c6ab0d1e0adab2e1c644b8306
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "63737821"
---
# <a name="deploy-network-file-system"></a>ネットワーク ファイル システムの展開

>適用対象:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

Network File System (NFS) は、ファイル共有の Windows サーバーと NFS プロトコルを使用して UNIX オペレーティング システムを実行しているコンピューターの間でファイルを転送できるソリューションを提供します。 このトピックでは、NFS のデプロイ時に従わなければならない手順を説明します。

## <a name="whats-new-in-network-file-system"></a>Network File System の新機能新機能

Windows Server 2012 での nfs の変更点を次に示します。

- **NFS version 4.1 のサポート**します。 このプロトコルのバージョンには、次の機能強化が含まれています。
  - ファイアウォールを移動するが簡単では、アクセシビリティを向上します。
  - サポート、RPCSEC\_GSS プロトコルより強力なセキュリティを提供して、クライアントとサーバーのセキュリティをネゴシエートすることができます。
  - UNIX と Windows のファイル セマンティクスをサポートしています。
  - クラスター化されたファイル サーバーの展開を利用します。
  - WAN に適した複合プロシージャをサポートしています。

- **Windows PowerShell の NFS モジュール**します。 組み込みの NFS コマンドレットの可用性では、さまざまな操作を自動化するやすくなります。 コマンドレット名は、適合して他の Windows PowerShell コマンドレット ("Get"と"Set"などの動詞を使用)、簡単になりますユーザーの新しいコマンドレットを使用する方法を説明する Windows PowerShell に慣れています。
- **NFS 管理の機能強化**します。 新しい UI ベースの管理を一元化されたコンソールには、SMB および NFS の共有、クォータ、ファイル スクリーンおよびクラスター化されたファイル サーバーを管理するだけでなく、分類の構成と管理が簡略化します。
- **Identity マッピングの機能強化**します。 新しい UI サポート、および、id マッピング ソースをすばやく構成し、個々 のマップされたユーザー id を作成することもできる id マッピングを構成するための Windows PowerShell コマンドレットのタスク ベースです。 機能強化を簡単に NFS と SMB の両方で、マルチ プロトコルへのアクセスの共有を設定する管理者。
- **クラスターのリソース モデルの再構築**します。 この機能強化、Windows nfs クラスターのリソース モデルと SMB プロトコル サーバー間の一貫性と管理を簡略化します。 持つ多くの共有 NFS サーバーでは、リソースのネットワークと必要な WMI 呼び出しの数が、NFS 共有の大きな数が削減格納されているボリューム フェールオーバーします。
- **再開キー マネージャーとの統合**します。 再開のキー マネージャーは、ファイル サーバーとファイル システムの状態を追跡し、クライアントまたはファイル サーバー上のデータを格納するサーバー アプリケーションを中断せずにフェールオーバーする Windows SMB および NFS プロトコル サーバーを使用するコンポーネントです。 この機能強化は、Windows Server 2012 を実行しているファイル サーバーの継続的な可用性の機能の重要なコンポーネントです。

## <a name="scenarios-for-using-network-file-system"></a>ネットワーク ファイル システムの使用に関するシナリオ

NFS は、Windows および UNIX ベースのオペレーティング システムの混在する環境をサポートします。 次の展開シナリオでは、NFS を使用して、継続的に使用可能な Windows Server 2012 ファイル サーバーを展開する方法の例を示します。

### <a name="provision-file-shares-in-heterogeneous-environments"></a>異機種混在環境でプロビジョニング ファイル共有します。

このシナリオは、組織の Windows と UNIX または Linux ベースのクライアントなどの他のオペレーティング システムの両方で構成される異機種混在環境で使用する該当コンピューター。 このシナリオでは、SMB および NFS の両方のプロトコル経由で同じファイル共有へのアクセスをマルチ プロトコルを行うことができます。 通常、このシナリオでは Windows ファイル サーバーを展開するときに Windows 上のユーザーと UNIX ベースのコンピューター間のコラボレーションが容易にします。 ファイル共有が構成されている場合は、SMB および NFS の両方のプロトコルで、SMB プロトコル経由でそのファイルにアクセスする Windows ユーザーと共有されてし、UNIX ベースのコンピューター上のユーザーは通常、NFS プロトコルを介してファイルにアクセスします。

このシナリオでは、有効な id マッピング ソースの構成が必要です。 Windows Server 2012 には、次の id マッピング ストアがサポートされています。

- マッピング ファイル
- Active Directory ドメイン サービス (AD DS)
- RFC 2307 に準拠していません LDAP は Active Directory ライトウェイト ディレクトリ サービス (AD LDS) など、格納します。
- ユーザー名マッピング (UNM) サーバー

### <a name="provision-file-shares-in-unix-based-environments"></a>UNIX ベースの環境でプロビジョニング ファイル共有します。

このシナリオでは、Windows ファイル サーバーが UNIX ベースのクライアント コンピューターの NFS ファイル共有へのアクセスを提供する、主に UNIX ベースの環境にデプロイされます。 マップされていない UNIX ユーザー アクセス (UUUA) オプションは、サーバーは、UNIX、Windows を作成しなくても NFS データの格納に使用できますが Windows アカウントへのマッピングするために最初に Windows Server 2008 R2 での NFS 共有の実装されました。 UUUA を迅速にプロビジョニングして、アカウントのマッピングを構成することがなく、NFS をデプロイできます。 有効にすると、nfs、UUUA はカスタムのセキュリティ識別子 (Sid) を表すマップされていないユーザーを作成します。 マップされたユーザー アカウントは、標準の Windows セキュリティ識別子 (Sid) を使用し、マップされていないユーザーがカスタム NFS Sid を使用します。

## <a name="system-requirements"></a>システム要件

NFS サーバーは、任意のバージョンの Windows Server 2012 にインストールできます。 またはを実行する、NFS サーバー NFS クライアントこれら NFS サーバーとクライアントの実装に準拠している場合、次のプロトコルの仕様のいずれかの UNIX ベースのコンピューターでは、NFS を使用できます。

1. NFS のバージョン 4.1 プロトコル仕様 (RFC で定義されている[5661](https://tools.ietf.org/html/rfc5661))
2. NFS のバージョン 3 プロトコル仕様 (RFC で定義されている[1813](https://tools.ietf.org/html/rfc1813))
3. NFS バージョン 2 プロトコルの仕様 (RFC で定義されている[1094](https://tools.ietf.org/html/rfc1094))

## <a name="deploy-nfs-infrastructure"></a>NFS のインフラストラクチャをデプロイします。

次のコンピューターを展開すると、ローカル エリア ネットワーク (LAN) 上の接続が必要です。

- NFS コンポーネントの 2 つの主要なサービスをインストールする Windows Server 2012 を実行している 1 つまたは複数のコンピューター:NFS と NFS クライアントのサーバーです。 これらのコンポーネントは、同じコンピューターまたは別のコンピューターにインストールできます。
- 1 つまたは複数 UNIX ベースのコンピューターの NFS サーバーと NFS クライアント ソフトウェアを実行しています。 NFS サーバーを実行している UNIX ベースのコンピューターは、NFS ファイル共有または NFS クライアントを使用するクライアントと Windows Server 2012 を実行しているコンピューターでは、エクスポートをホストします。 必要に応じて、さまざまな UNIX ベースのコンピューター上または同じの UNIX ベースのコンピューターでは、NFS サーバーとクライアント ソフトウェアをインストールできます。
- Windows Server 2008 R2 の機能レベルで実行されているドメイン コント ローラー。 ドメイン コント ローラーは、ユーザーの認証情報と Windows 環境のマッピングを提供します。
- ドメイン コント ローラーがデプロイされていない場合は、UNIX 環境でのユーザーの認証情報を提供するネットワーク情報サービス (NIS) サーバーを使用できます。 または、ユーザー名マッピング サービスを実行しているコンピューターに保存されているパスワードとグループのファイルを使用する場合は、ことができます。

### <a name="install-network-file-system-on-the-server-with-server-manager"></a>サーバーにサーバー マネージャーでネットワーク ファイル システムをインストールします。

1. 役割と機能の追加ウィザードの [サーバーの役割] で、 **[ファイル サービスおよび記憶域サービス]** をクリックします (まだインストールされていない場合)。
2. **ファイルおよび iSCSI サービス**を選択します**ファイル サーバー**と**NFS サーバー**します。 選択**機能の追加**選択した NFS の機能が追加されます。
3. 選択**インストール**サーバー上の NFS コンポーネントをインストールします。

### <a name="install-network-file-system-on-the-server-with-windows-powershell"></a>Windows PowerShell を使用したサーバー上のネットワーク ファイル システムのインストールします。

1. Windows PowerShell を起動します。 タスク バーの PowerShell アイコンを右クリックし、 **[管理者として実行]** をクリックします。
2. 次の Windows PowerShell コマンドを実行します。

```PowerShell
Import-Module ServerManager
Add-WindowsFeature FS-NFS-Service
Import-Module NFS
```

## <a name="configure-nfs-authentication"></a>NFS 認証を構成します。

NFS のバージョン 4.1 と NFS バージョン 3.0 プロトコルを使用する場合は、次の認証とセキュリティ オプションがあります。

- RPCSEC\_GSS
  - **Krb5**: Kerberos version 5 プロトコルを使用すると、ファイル共有へのアクセスを許可する前にユーザーを認証します。
  - **Krb5i**: 整合性チェック (チェックサム) での認証に Kerberos version 5 プロトコルを使用して、データが変更されていないことを確認します。
  - **Krb5p**を使用して Kerberos version 5 プロトコルは、プライバシーを暗号化して NFS トラフィックを認証します。
- AUTH\_SYS

サーバーの承認を使用しないように選択することもできます (認証\_SYS)、マップされていないユーザー アクセスを有効にするオプションを表示します。 マップされていないユーザー アクセスを使用する場合は UID によってマップされていないユーザー アクセスを許可する指定できますが、既定では、GID、または匿名アクセスを許可/。

NFS 認証を構成する手順については、次のセクションで説明します。

## <a name="create-an-nfs-file-share"></a>NFS ファイル共有を作成します。

サーバー マネージャーまたは Windows PowerShell の NFS コマンドレットを使用して NFS ファイル共有を作成することができます。

### <a name="create-an-nfs-file-share-with-server-manager"></a>サーバー マネージャーで NFS ファイル共有を作成します。

1. ローカルの Administrators グループのメンバーとしてサーバーにログオンします。
2. サーバー マネージャーが自動的に起動します。 そのが自動的に起動しない場合は、選択**開始**、型**servermanager.exe**、し、**サーバー マネージャー**します。
3. 左側で、次のように選択します。 **File and Storage Services**、し、**共有**します。
4. 選択**ファイル共有を作成するには、新しい共有ウィザードを起動**します。
5. **プロファイルの選択** ページで、いずれかを選択**NFS の共有 –-簡易**または**NFS 共有 - 高度な**を選択し、**次**。
6. **共有の場所**ページで、サーバーとボリュームを選択し、選択**次**します。
7. **共有名** ページで、新しい共有の名前を指定して選択**次**。
8. **認証** ページで、この共有を使用する認証方法を指定します。
9. **共有のアクセス許可**] ページで、[**追加**、し、ホスト、クライアント グループまたは共有へのアクセス許可を付与する netgroup を指定します。
10. **権限**を選択し、ユーザーのアクセス制御の種類を構成する**OK**。
11. **確認**] ページで、構成を確認し、[**作成**NFS ファイル共有を作成します。

### <a name="windows-powershell-equivalent-commands"></a>Windows PowerShell と同等のコマンド

次の Windows PowerShell コマンドレットは、NFS ファイル共有を作成もできます (場所`nfs1`、共有の名前を指定し、`C:\\shares\\nfsfolder`はファイル パスです)。

```PowerShell
New-NfsShare -name nfs1 -Path C:\shares\nfsfolder
```

### <a name="known-issue"></a>既知の問題
により、NFS バージョン 4.1 はファイルの名前を作成するか、無効な文字を使用してコピーします。 Vi エディターを使用して、ファイルを開こうとすると、破損しているものとして表示されます。 Vi からファイルを保存して名前を変更に移動するか、またはアクセス許可を変更できません。 Illigal 文字を使用しないでください。
