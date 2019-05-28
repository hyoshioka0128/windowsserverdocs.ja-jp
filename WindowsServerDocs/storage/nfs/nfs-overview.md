---
title: ネットワーク ファイル システムの概要
description: ネットワーク ファイル システムを説明します。
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9b0d339df588c784f8fe46f7dd0e6ce2975d0c48
ms.sourcegitcommit: 21165734a0f37c4cd702c275e85c9e7c42d6b3cb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2019
ms.locfileid: "65034653"
---
# <a name="network-file-system-overview"></a>ネットワーク ファイル システムの概要

>適用対象:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

このトピックでは、ネットワーク ファイル システムの役割サービスと Windows server ファイル サービスおよび記憶域サービス サーバーの役割に含まれている機能について説明します。 Network File System (NFS) は、ファイル共有の Windows と Windows 以外のコンピューターの両方に含まれる異種環境を所有している企業のソリューションを提供します。

## <a name="feature-description"></a>機能の説明

NFS プロトコルを使用して、Windows と Linux または UNIX など、他の非 Windows オペレーティング システムを実行するコンピューター間でファイルを転送することができます。

Windows Server での NFS には、NFS と NFS クライアントのサーバーが含まれます。 Windows Server を実行しているコンピューターでは、NFS サーバーを使用して、他の非 Windows クライアント コンピューターの NFS のファイル サーバーとして機能します。 NFS クライアントには、Windows NFS サーバーに格納されているファイルにアクセスする Windows Server を実行している Windows ベースのコンピューターが使用できるようにします。

## <a name="windows-and-windows-server-versions"></a>Windows および Windows Server のバージョン

Windows では、複数のバージョンのオペレーティング システムのバージョンとファミリによって、サーバーと NFS クライアントをサポートします。 

| オペレーティング システム | NFS サーバーのバージョン |NFS クライアントのバージョン|
| ----------------- | ------------------- | ----------------- |
| Windows 7、Windows 8.1、Windows 10 | なし | NFSv2、NFSv3 |
| Windows Server 2008、Windows Server 2008 R2 | NFSv2、NFSv3 | NFSv2、NFSv3 |
| Windows Server 2012、Windows Server 2012 R2、Windows Server 2016、Windows Server 2019 | NFSv2, NFSv3, NFSv4.1  | NFSv2、NFSv3 |

## <a name="practical-applications"></a>実際の適用例

NFS を使用するいくつかの方法を次に示します。

- Windows NFS のファイル サーバーを使用して、マルチプラット フォームのクライアントから同じファイル共有に SMB および NFS の両方のプロトコル経由でのマルチ プロトコルのアクセスを提供します。
- 非 Windows クライアント コンピューターの NFS ファイル共有へのアクセスを提供する大部分の非 Windows オペレーティング システム環境での Windows NFS ファイル サーバーをデプロイします。
- 両方の SMB および NFS プロトコルを介してアクセス可能なファイル共有にデータを格納する 1 つのオペレーティング システムから別のアプリケーションを移行します。

## <a name="new-and-changed-functionality"></a>新機能と変更された機能

ネットワーク ファイル システムで追加または変更された機能には、NFS のバージョン 4.1 のサポートと強化された展開と管理の容易性が含まれています。 Windows Server 2012 で変更または新しくなった機能については、次の表を参照してください。

|機能|新規/更新|説明|
|---|---|---|
|[NFS バージョン 4.1](#nfs-version-41)|新規|セキュリティの強化、パフォーマンス、および相互運用性の NFS version 3 と比較します。|
|[NFS インフラストラクチャ](#nfs-infrastructure)|更新|展開と管理容易性を向上し、セキュリティが向上します。|
|[NFS version 3 の継続的な可用性](#nfs-version-3-continuous-availability)|更新|NFS version 3 のクライアントでの継続的な可用性が向上します。|
|[展開と管理の容易性の向上](#deployment-and-manageability-improvements)|更新|使用すると、簡単にデプロイし、新しい Windows PowerShell コマンドレットと新しい WMI プロバイダーで NFS を管理できます。|

## <a name="nfs-version-41"></a>NFS バージョン 4.1

NFS バージョン 4.1 では、すべての省略可能な側面では、いくつかだけでなく、必要な側面を実装の[RFC 5661](https://tools.ietf.org/html/rfc5661):

- **仮想ファイル システム**、物理的および論理的名前空間を分離し、NFS version 3 と NFS バージョン 2 と互換性をファイル システム。 仮想ファイル システムの一部であるエクスポートされたファイル システムの別名を指定します。
- **Rpc の複合**関連する操作を結合し、頻繁な通信を削減します。
- **セッションとセッションのトランキング**により、1 つにすぎませんセマンティックし、継続的な可用性と NFS 4.1 クライアントと NFS サーバーの間に複数のネットワークを活用してパフォーマンスを向上できるようにします。

## <a name="nfs-infrastructure"></a>NFS インフラストラクチャ

Windows Server 2012 での全体的な NFS インフラストラクチャの機能強化を次に説明します。

- **リモート プロシージャ コール (RPC)/外部データ表記 (XDR)** WinSock ネットワーク プロトコルによって利用したトランスポート インフラストラクチャは両方 NFS サーバーと NFS クライアントを利用できます。 優れたサポートを提供しています、およびスケーラビリティが向上し、Receive Side Scaling (RSS) を提供します。 このトランスポート デバイス Interface (TDI) が置き換えられます。
- **マルチプレクサーの RPC ポート**機能は、ファイアウォールに対応した (を管理する以下のポート) を NFS の展開を簡略化できます。
- **キャッシュの自動チューニングおよびスレッド プール**は動的で、キャッシュを自動的に調整し、スレッド プールのワークロードに基づいて、RPC、XDR スキーマの新しいインフラストラクチャの管理機能をリソースには。 NFS が展開されるとすぐに最適なパフォーマンスを提供するパラメーターのチューニング時に関連する当て推量完全に削除されます。
- **新しい Kerberos プライバシーの実装と認証オプション**既存 krb5 krb5i 認証オプションと Kerberos プライバシー (Krb5p) のサポートを追加するとします。
- **Id マッピングの Windows PowerShell モジュール**コマンドレットやすく id マッピングの管理、Active Directory ライトウェイト ディレクトリ サービス (AD LDS) を構成し、UNIX および Linux の passwd ファイルとフラット ファイルを設定します。
- **ボリューム マウント ポイント**nfs version 4.1 の NFS 共有にマウントされたボリュームにアクセスできます。
- **ポートを多重化**機能は、RPC ポート マルチプレクサー (ポート 2049)、ファイアウォールに対応したされ NFS の展開を簡素化をサポートしています。

## <a name="nfs-version-3-continuous-availability"></a>NFS version 3 の継続的な可用性

NFS version 3 のクライアントには、複数の可用性とダウンタイムの短縮と計画されたフェールオーバーを高速かつ透過的なことができます。 フェールオーバー プロセスは、ために、バージョン 3 の NFS クライアントの高速です。

- クラスタ リング インフラストラクチャには、ネットワーク名リソースのフェールオーバー時間が大幅に向上あたり 1 つのリソースではなく 1 つのリソースで使用できます。
- NFS サーバー内のフェールオーバー パスより優れたパフォーマンスをチューニングします。
- NFS サーバーでのワイルドカードの登録が不要、し、フェールオーバーはより詳細に合わせて調整します。
- ネットワーク ステータス モニター (NSM) の通知が、フェールオーバー プロセスの後に送信され、クライアントが TCP タイムアウト、失敗したに再接続するまで待機する必要がなくなったサーバー上でします。

NFS サーバーは、通常は計画的なメンテナンスの間に、手動で開始する場合にのみ、透過フェールオーバーをサポートすることにご注意ください。 計画外のフェールオーバーが発生した場合、NFS クライアントの接続が失われます。 NFS サーバーも再開キー フィルターとの統合はありません。 つまり、NFS クライアントがアクセスしているファイルと同じファイルに、計画的なフェールオーバーの直後にローカル アプリまたは SMB セッションがアクセスしようとすると、NFS クライアントの接続が失われる可能性があります (透過フェールオーバーは失敗します)。

## <a name="deployment-and-manageability-improvements"></a>展開と管理の容易性の向上

次の方法を展開して、NFS の管理が改善します。

- 40 個以上の新しい Windows PowerShell コマンドレットを簡単に構成して、NFS ファイル共有を管理します。 詳細については、次を参照してください。 [Windows PowerShell で NFS コマンドレット](https://docs.microsoft.com/powershell/module/nfs/?view=win10-ps)します。
- Id マッピングは、フラット ファイルをローカル マッピング ストアと id マッピングを構成するための新しい Windows PowerShell コマンドレットが向上します。
- サーバー マネージャーのグラフィカル ユーザー インターフェイスが使いやすくします。
- 新しい WMI バージョン 2 のプロバイダーは、管理が簡単に使用できます。
- RPC ポート マルチプレクサー (ポート 2049) がファイアウォールに対応したおよび NFS の展開を簡略化します。

## <a name="server-manager-information"></a>サーバー マネージャー情報

サーバー マネージャーでも、新しい[Windows Admin Center](../../manage/windows-admin-center/understand/windows-admin-center.md) -追加の役割と機能のウィザードを使用して、NFS サーバーの役割サービスを追加する (ファイルおよび iSCSI サービスの役割)。 機能のインストールに関する全般的な情報については、「 [役割、役割サービス、または機能のインストールまたはアンインストール](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831809(v=ws.11)>)」を参照してください。 サーバー NFS ツールでは、nfs サーバーを管理するネットワーク ファイル システムの MMC スナップインのサービスと NFS コンポーネント用のクライアントが含まれます。 スナップインを使用して、コンピューターにインストールされている NFS コンポーネント用のサーバーを管理できます。 NFS サーバーには、いくつかの Windows のコマンドライン管理ツールも含まれています。

- **マウント**がリモート NFS 共有を (エクスポート) をローカルにマウントして、Windows クライアント コンピューターのローカル ドライブ文字にマップします。
- **Nfsadmin** NFS コンポーネントおよび nfs クライアントのサーバーの設定の構成を管理します。
- **Nfsshare**で NFS サーバーを使用して共有するフォルダーの NFS 共有の設定を構成します。
- **Nfsstat**を表示または nfs サーバーが受信した呼び出しの統計をリセットします。
- **Showmount** nfs サーバーからエクスポートされたマウントされているファイル システムを表示します。
- **Umount** NFS がマウントされたドライブを削除します。

Windows Server 2012 での NFS は、NFS の具体的にはいくつかの新しいコマンドレットの Windows PowerShell 用の NFS モジュールを紹介します。 これらのコマンドレットは、NFS 管理タスクを自動化する簡単な方法を提供します。 詳細については、次を参照してください。 [Windows PowerShell で NFS コマンドレット](https://docs.microsoft.com/powershell/module/nfs/?view=win10-ps)します。

## <a name="additional-information"></a>追加情報

次の表は、NFS を評価するための他のリソースを示します。

|コンテンツの種類|参考資料|
|---|---|
|展開|[ネットワーク ファイル システムの展開](deploy-nfs.md)|
|操作|[Windows PowerShell で NFS コマンドレット](https://docs.microsoft.com/powershell/module/nfs/?view=win10-ps)|
|関連テクノロジ|[Windows Server でのストレージ](../storage.md)|