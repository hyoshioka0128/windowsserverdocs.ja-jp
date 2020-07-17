---
title: ネットワーク ファイル システムの概要
description: ネットワークファイルシステムについて説明します。
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2589e21c54fa864629f81b5889d0442c6f0de254
ms.sourcegitcommit: 568b924d32421256f64abfee171304f1daf320d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "85070564"
---
# <a name="network-file-system-overview"></a>ネットワーク ファイル システムの概要

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、Windows Server のファイルサービスおよび記憶域サービスのサーバーの役割に含まれるネットワークファイルシステムの役割サービスと機能について説明します。 Network File System (NFS) は、Windows コンピューターと Windows 以外のコンピューターの両方を含む異種環境がある企業向けのファイル共有ソリューションを提供します。

## <a name="feature-description"></a>機能の説明

NFS プロトコルを使用すると、Windows を実行しているコンピューターと、Linux や UNIX などの Windows 以外のオペレーティングシステムの間でファイルを転送できます。

Windows Server の NFS には、NFS サーバーと NFS クライアントが含まれています。 Windows Server を実行しているコンピューターは、NFS サーバーを使用して、他の Windows 以外のクライアントコンピューターの NFS ファイルサーバーとして機能できます。 NFS クライアントを使用すると、windows Server を実行している Windows ベースのコンピューターは、windows 以外の NFS サーバーに格納されているファイルにアクセスできます。

## <a name="windows-and-windows-server-versions"></a>Windows および Windows Server のバージョン

Windows では、オペレーティングシステムのバージョンとファミリに応じて、複数のバージョンの NFS クライアントおよびサーバーがサポートされています。 

| オペレーティング システム | NFS サーバーのバージョン |NFS クライアントのバージョン|
| ----------------- | ------------------- | ----------------- |
| Windows 7、Windows 8.1、Windows 10 | N/A | NFSv2、NFSv3 |
| Windows Server 2008、Windows Server 2008 R2 | NFSv2、NFSv3 | NFSv2、NFSv3 |
| Windows Server 2012、Windows Server 2012 R2、Windows Server 2016、Windows Server 2019 | NFSv2、NFSv3、NFSv 4.1  | NFSv2、NFSv3 |

## <a name="practical-applications"></a>実際の適用例

NFS を使用するいくつかの方法を次に示します。

- Windows NFS ファイルサーバーを使用して、マルチプラットフォームクライアントからの SMB プロトコルと NFS プロトコルの両方で同じファイル共有へのマルチプロトコルアクセスを提供します。
- Windows 以外のオペレーティングシステム環境で windows NFS ファイルサーバーを展開し、Windows 以外のクライアントコンピューターに NFS ファイル共有へのアクセスを提供します。
- SMB プロトコルと NFS プロトコルの両方を介してアクセス可能なファイル共有にデータを格納することによって、あるオペレーティングシステムから別のオペレーティングシステムにアプリケーションを移行します。

## <a name="new-and-changed-functionality"></a>新機能と変更された機能

Network File System の新機能と変更された機能には、NFS バージョン4.1 のサポートと、展開と管理の強化が含まれています。 Windows Server 2012 で新しく追加または変更された機能の詳細については、次の表を参照してください。

|機能|新規/更新|説明|
|---|---|---|
|[NFS バージョン4.1](#nfs-version-41)|新規|NFS バージョン3と比較して、セキュリティ、パフォーマンス、および相互運用性が向上しました。|
|[NFS インフラストラクチャ](#nfs-infrastructure)|更新済み|は、展開と管理性を向上させ、セキュリティを強化します。|
|[NFS バージョン3の継続的可用性](#nfs-version-3-continuous-availability)|更新済み|NFS バージョン3クライアントの継続的な可用性を向上させます。|
|[展開と管理の容易性の向上](#deployment-and-manageability-improvements)|更新済み|新しい Windows PowerShell コマンドレットと新しい WMI プロバイダーを使用して NFS を簡単に展開および管理できます。|

## <a name="nfs-version-41"></a>NFS バージョン4.1

NFS バージョン4.1 では、 [RFC 5661](https://tools.ietf.org/html/rfc5661)のいくつかのオプションの側面に加えて、必要なすべての側面が実装されています。

- **擬似ファイルシステム**。物理および論理名前空間を分離し、nfs version 3 および nfs バージョン2と互換性があります。 エクスポートされたファイルシステムには、擬似ファイルシステムの一部である別名が用意されています。
- **複合 rpc**は関連する操作を結合し、頻繁な通信を減らします。
- **セッションとセッションのトランク**によって、1つのセマンティックのみが有効になり、nfs 4.1 クライアントと nfs サーバー間で複数のネットワークを利用しながら、継続的な可用性とパフォーマンスが向上します。

## <a name="nfs-infrastructure"></a>NFS インフラストラクチャ

以下では、Windows Server 2012 の NFS インフラストラクチャ全体の機能強化について説明します。

- WinSock ネットワークプロトコルによって提供される**リモートプロシージャコール (RPC)/外部データ表現 (XDR)** トランスポートインフラストラクチャは、nfs サーバーと nfs クライアントの両方で使用できます。 これはトランスポートデバイスインターフェイス (TDI) に代わるものであり、より優れたサポートを提供し、より優れたスケーラビリティと Receive Side Scaling (RSS) を提供します。
- **RPC ポートマルチプレクサー**の機能は、ファイアウォールを使いやすく (管理するポートが少ない)、NFS の展開を簡略化します。
- **自動調整されたキャッシュとスレッドプール**は、新しい RPC/XDR インフラストラクチャのリソース管理機能であり、ワークロードに基づいてキャッシュとスレッドプールが動的に自動的に調整されます。 これにより、パラメーターをチューニングするときに必要な推測が完全に削除され、NFS が展開されるとすぐに最適なパフォーマンスが得られます。
- Kerberos プライバシー (Krb5p) のサポートと既存の krb5.conf および krb5i 認証オプションの追加による**新しい kerberos プライバシーの実装と認証オプション**。
- **Id マッピング Windows PowerShell モジュール**コマンドレットを使用すると、id マッピングの管理、Active Directory ライトウェイトディレクトリサービスの構成 (AD LDS)、UNIX および Linux の passwd ファイルとフラットファイルの設定が簡単になります。
- **ボリュームマウントポイント**を使用すると、nfs 共有の下にマウントされている、nfs バージョン4.1 のボリュームにアクセスできます。
- **ポートの多重**化機能では、ファイアウォールを使いやすく、NFS の展開を簡素化する RPC ポートマルチプレクサー (ポート 2049) がサポートされています。

## <a name="nfs-version-3-continuous-availability"></a>NFS バージョン3の継続的可用性

NFS version 3 クライアントでは、可用性とダウンタイムの短縮により、高速で透過的な計画フェールオーバーを行うことができます。 NFS バージョン3クライアントでは、次のようなフェールオーバープロセスが高速に実行されます。

- クラスター化インフラストラクチャでは、共有ごとに1つのリソースではなく、ネットワーク名ごとに1つのリソースが許可されるようになり、リソースのフェールオーバー時間が大幅に短縮されました。
- NFS サーバー内のフェールオーバーパスは、パフォーマンス向上のためにチューニングされています。
- NFS サーバーでのワイルドカード登録は必要なくなり、フェールオーバーはより細かく調整されます。
- ネットワーク Status Monitor (NSM) の通知は、フェールオーバープロセスの後に送信され、クライアントは TCP タイムアウトがフェールオーバーされたサーバーに再接続するまで待機する必要がなくなります。

NFS サーバーは、通常は計画的なメンテナンスの間に、手動で開始する場合にのみ、透過フェールオーバーをサポートすることにご注意ください。 計画外のフェールオーバーが発生した場合、NFS クライアントの接続が失われます。 NFS サーバーも、再開キーフィルターとは統合されていません。 つまり、NFS クライアントがアクセスしているファイルと同じファイルに、計画的なフェールオーバーの直後にローカル アプリまたは SMB セッションがアクセスしようとすると、NFS クライアントの接続が失われる可能性があります (透過フェールオーバーは失敗します)。

## <a name="deployment-and-manageability-improvements"></a>展開と管理の容易性の向上

NFS の展開と管理は、次の点で改善されています。

- 40を超える新しい Windows PowerShell コマンドレットを使用すると、NFS ファイル共有の構成と管理が簡単になります。 詳細については、「 [Windows PowerShell の NFS コマンドレット](https://docs.microsoft.com/powershell/module/nfs/?view=win10-ps)」を参照してください。
- Id マッピングは、ローカルのフラットファイルマッピングストアと、id マッピングを構成するための新しい Windows PowerShell コマンドレットによって強化されています。
- サーバーマネージャーのグラフィカルユーザーインターフェイスは使いやすくなっています。
- 新しい WMI バージョン2プロバイダーは、管理を容易にするために使用できます。
- RPC ポートマルチプレクサー (ポート 2049) は、ファイアウォールを使いやすく、NFS の展開を簡略化します。

## <a name="server-manager-information"></a>サーバー マネージャー情報

サーバーマネージャーまたはそれ以降の[Windows 管理センター](../../manage/windows-admin-center/understand/windows-admin-center.md)では、役割と機能の追加ウィザードを使用して、NFS サーバーの役割サービス (ファイルと iSCSI サービスの役割の下) を追加します。 機能のインストールに関する全般的な情報については、「 [役割、役割サービス、または機能のインストールまたはアンインストール](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831809(v=ws.11)>)」を参照してください。 NFS サーバーツールには、NFS サーバーと NFS クライアントコンポーネントを管理するための、Network File System MMC スナップイン用のサービスが含まれています。 スナップインを使用すると、コンピューターにインストールされている NFS サーバーコンポーネントを管理できます。 NFS サーバーには、Windows のコマンドライン管理ツールもいくつか含まれています。

- **Mount**は、リモート NFS 共有 (エクスポートとも呼ばれます) をローカルにマウントし、Windows クライアントコンピューター上のローカルドライブ文字にマップします。
- **Nfsadmin**は、nfs サーバーと nfs クライアントコンポーネントの構成設定を管理します。
- NFS サーバーを使用して共有されるフォルダーに対して**nfs 共有の設定を構成し**ます。
- **Nfsstat**は、NFS サーバーによって受信された呼び出しの統計を表示またはリセットします。
- **Showmount**は、NFS サーバーによってエクスポートされたマウント済みのファイルシステムを表示します。
- **マウント解除さ**れた NFS ドライブを削除します。

Windows Server 2012 の NFS では、nfs 用に nfs モジュールが導入されています。これには、NFS 専用の新しいコマンドレットがいくつかあります。 これらのコマンドレットは、NFS 管理タスクを自動化する簡単な方法を提供します。 詳細については、「 [Windows PowerShell の NFS コマンドレット](https://docs.microsoft.com/powershell/module/nfs/?view=win10-ps)」を参照してください。

## <a name="additional-information"></a>関連情報

次の表に、NFS の評価に関するその他のリソースを示します。

|コンテンツ タイプ|参考資料|
|---|---|
|デプロイ|[ネットワーク ファイル システムの展開](deploy-nfs.md)|
|操作|[Windows PowerShell の NFS コマンドレット](https://docs.microsoft.com/powershell/module/nfs/?view=win10-ps)|
|関連テクノロジ|[Windows Server の記憶域](../storage.yml)|