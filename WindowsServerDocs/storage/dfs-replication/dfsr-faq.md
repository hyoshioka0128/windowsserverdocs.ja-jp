---
Title: 'DFS レプリケーション: よく寄せられる質問 (FAQ)'
ms.date: 06/18/2014
ms.prod: windows-server-threshold
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 00bb3dfd79096e28f9752053152571ea9919edcf
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284265"
---
# <a name="dfs-replication-frequently-asked-questions-faq"></a>DFS レプリケーション: よく寄せられる質問 (FAQ)


更新:2019 年 4 月 30日

適用先:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

この FAQ は、Windows Server の分散ファイル システム (DFS) レプリケーション (DFS-R または DFSR とも呼ばれます) に関する質問に回答します。

DFS 名前空間については、次を参照してください。 [DFS 名前空間。よく寄せられる質問](https://technet.microsoft.com/library/ee404780)します。

DFS レプリケーションでは新しい方法の詳細については、次のトピックを参照してください。

  - [DFS 名前空間と DFS レプリケーションの概要](https://technet.microsoft.com/library/jj127250)(で Windows Server 2012)  
      
  - [分散ファイル システムで新](https://technet.microsoft.com/library/ee307957)トピック[で変更された Windows Server 2008 から Windows Server 2008 R2 の機能](https://technet.microsoft.com/library/dd391932)  
      
  - [分散ファイル システム](https://technet.microsoft.com/library/cc753479)トピック[で変更された Windows Server 2003 SP1 から Windows Server 2008 の機能](https://technet.microsoft.com/library/cc753208)  
      

このトピックに対する最近の変更については、「 [変更履歴](#change-history) 」を参照してください。

      

## <a name="interoperability"></a>相互運用性

### <a name="can-dfs-replication-communicate-with-frs"></a>DFS レプリケーションは、FRS と通信できますか。

No. DFS レプリケーションでは、ファイル レプリケーション サービス (FRS) は通信しません。 DFS レプリケーションと FRS と同時に、同じサーバー上に実行できますが、データの損失が発生することができますので、同じフォルダーまたはサブフォルダーをレプリケートするように構成することはありません必要があります。

### <a name="can-dfs-replication-replace-frs-for-sysvol-replication"></a>置き換えることが DFS レプリケーション FRS の SYSVOL のレプリケーション

はい、DFS レプリケーションでは、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、または Windows Server 2008 を実行しているサーバー上の SYSVOL レプリケーション用 FRS を置き換えることができます。 Windows Server 2003 R2 を実行しているサーバーは、SYSVOL フォルダーのレプリケートに DFS レプリケーションの使用をサポートしていません。

DFS レプリケーションを使用して SYSVOL をレプリケートする方法の詳細については、次を参照してください。、 [SYSVOL レプリケーション移行ガイド。FRS DFS レプリケーションから](https://technet.microsoft.com/library/dd640019)します。

### <a name="can-i-upgrade-from-frs-to-dfs-replication-without-losing-configuration-settings"></a>アップグレードできます FRS から DFS レプリケーションの構成設定を失うことがなくでしょうか。

[はい]。 FRS から DFS レプリケーションへのレプリケーションを移行は、次のドキュメントを参照してください。

  - SYSVOL フォルダー以外のフォルダーのレプリケーションを移行するには、次を参照してください。 [DFS 操作ガイド。FRS から DFS レプリケーションへの移行](http://go.microsoft.com/fwlink/?linkid=192776)と[FRS2DFSR – FRS、DFSR 移行ユーティリティ](http://go.microsoft.com/fwlink/?linkid=195437)(http://go.microsoft.com/fwlink/?LinkID=195437) します。  
      
  - SYSVOL フォルダーのレプリケーションを DFS レプリケーションに移行する、次を参照してください。 [SYSVOL レプリケーション移行ガイド。FRS DFS レプリケーションから](https://technet.microsoft.com/library/dd640019)します。  
      

### <a name="can-i-use-dfs-replication-in-a-mixed-windowsunix-environment"></a>Windows または UNIX の混在環境で DFS レプリケーションを使用することができますか。

[はい]。 DFS レプリケーションでは、Windows Server を実行しているサーバーの間でレプリケートするコンテンツのみサポートしていますが、UNIX クライアントは、Windows サーバー上のファイル共有にアクセスできます。 これを行うには、DFS レプリケーション サーバーでネットワーク ファイル システム (NFS) 用サービスをインストールします。

この機能は制限が多くの場合、または (を使用して SMB 署名を無効にするなど、Windows 環境の変更が必要ですが、Windows ファイル共有に直接アクセスする UNIX クライアントの数に含まれる SMB/CIFS クライアント機能を使用することもできます。グループ ポリシーの場合)。

DFS レプリケーションは、Windows Server オペレーティング システムを実行するサーバーで、NFS と相互運用が NFS のマウント ポイントをレプリケートすることはできません。

### <a name="can-i-use-the-volume-shadow-copy-service-with-dfs-replication"></a>DFS レプリケーションで、ボリューム シャドウ コピー サービスを使用することができますか。

[はい]。 ボリューム シャドウ コピー サービス (VSS) のボリュームの DFS レプリケーションがサポートされており、以前のスナップショットは以前のバージョンのクライアントで正常に復元できます。

### <a name="can-i-use-windowsbackup-ntbackupexe-to-remotely-back-up-a-replicated-folder"></a>Windows バックアップ (Ntbackup.exe) を使用してリモートでレプリケート フォルダーをバックアップできますか。

いいえ、Windows Server 2003 を実行するコンピューターで、または Windows Server 2012 を実行しているコンピューター上のレプリケート フォルダーの内容をバックアップするには、以前は、Windows バックアップ (Ntbackup.exe) を使用して、Windows Server 2008 R2、または Windows Server 2008 がサポートされていません。

レプリケートされたフォルダーに格納されているファイルをバックアップするには、Windows Server バックアップまたは Microsoft® System Center Data Protection Manager を使用します。 Windows Server 2008 R2 および Windows Server 2008 でのバックアップと回復の機能については、次を参照してください。[バックアップと回復](https://technet.microsoft.com/library/Cc754097)します。 詳細については、次を参照してください。 [System Center Data Protection Manager](http://go.microsoft.com/fwlink/?linkid=182261) (http://go.microsoft.com/fwlink/?LinkId=182261) します。

### <a name="do-file-system-policies-impact-dfs-replication"></a>ファイル システムのポリシーは DFS レプリケーションに影響しますか。

[はい]。 レプリケート フォルダーのファイル システムのポリシーを構成しないでください。 ファイル システムのポリシーでは、すべてグループ ポリシーの更新間隔に NTFS アクセス許可を再適用されます。 これにより、ファイルが閉じられるまで、開いているファイルがレプリケートされていないために、共有違反。

### <a name="does-dfs-replication-replicate-mailboxes-hosted-on-microsoft-exchange-server"></a>DFS レプリケーションは、Microsoft Exchange Server にホストされているメールボックスをレプリケートしますか。

No. DFS レプリケーションを使用して、Microsoft Exchange Server にホストされているメールボックスをレプリケートすることはできません。

### <a name="does-dfs-replication-support-file-screens-created-by-file-server-resource-manager"></a>DFS レプリケーションは、ファイル サーバー リソース マネージャーによって作成されたファイル スクリーンをサポートしますか。

[はい]。 ただし、ファイル サーバー リソース マネージャー (FSRM) ファイルのスクリーン処理の設定は、レプリケーションの両方の end で一致しなければなりません。 さらに、DFS レプリケーションでは、ファイルとフォルダーをレプリケーションから特定のファイルおよびファイルの種類を除外するのに使用できる、独自のフィルター メカニズムがあります。

次に、ファイル スクリーンやクォータを実装するためのベスト プラクティスを示します。

  - クォータまたはファイル スクリーンの対象と非表示の DfsrPrivate フォルダーでなければなりません。  
      
  - スクリーン処理が有効にする前に、任意のレプリケート フォルダーでスクリーン ファイルが存在しない必要があります。  
      
  - フォルダーを超えないクォータ、クォータを有効にする前に、。  
      
  - 慎重にハード クォータを使用する必要があります。 レプリケーションでは、前に、クォータ内で維持がそれを超えるファイルがレプリケートされるときにレプリケーション グループの個々 のメンバーのことができます。 たとえば、ユーザー (つまり、ハード制限で) 10 メガバイト (MB) にファイルをサーバー A のコピーし、別のユーザーが次のレプリケーションが発生した場合、サーバー B に 5 MB のファイルをコピー、両方のサーバーがクォータを超えます、5 メガバイト単位で。 これには、DFS レプリケーション、バージョン ベクターと可能なパフォーマンスの問題の穴を原因と、ファイルをレプリケートを再試行し続ける可能性があります。  
      

### <a name="is-dfs-replication-cluster-aware"></a>DFS レプリケーションのクラスターを認識しますか。

はい、Windows Server 2012 R2、Windows Server 2012 および Windows Server 2008 R2 での DFS レプリケーションには、レプリケーション グループのメンバーとしてフェールオーバー クラスターを追加する機能が含まれています。 詳細については、次を参照してください。[をレプリケーション グループのフェールオーバー クラスターの追加](http://go.microsoft.com/fwlink/?linkid=155085)(http://go.microsoft.com/fwlink/?LinkId=155085) します。 バージョンの Windows Server 2008 R2 より前の Windows での DFS レプリケーション サービスは、フェールオーバー クラスターでは、連携するものはありませんし、サービスが別のノードにフェールオーバーしていません。


> [!NOTE]
> DFS レプリケーションでは、クラスターの共有ボリュームにファイルをレプリケートできません。 
<br>


### <a name="is-dfs-replication-compatible-with-data-deduplication"></a>DFS レプリケーションは、データ重複除去と互換性のあるでしょうか。

はい、DFS レプリケーションでは、Windows Server でデータ重複除去を使用しているボリューム上のフォルダーをレプリケートできます。

### <a name="is-dfs-replication-compatible-with-ris-and-wds"></a>DFS レプリケーションは、RIS、WDS と互換性のあるでしょうか。

[はい]。 DFS レプリケーションは、単一インスタンス記憶域 (SIS) が有効になっているボリュームを複製します。 SIS は、リモート インストール サービス (RIS)、Windows 展開サービス (WDS)、および Windows Storage Server で使用されます。

### <a name="is-it-possible-to-use-dfs-replication-with-offline-files"></a>オフライン ファイルでの DFS レプリケーションを使用することはできますか。

安全に一緒に使用する DFS レプリケーションとオフライン ファイルのシナリオでファイルを書いている時点で 1 つだけのユーザーがある場合。 これは 2 つのブランチ オフィス間を移動し、どちらのブランチでは、そのファイルにアクセス中にしたりできるようにするユーザー向けには役立ちます。 オフラインです。 オフライン ファイルはオフラインで使用するローカル ファイルをキャッシュし、DFS レプリケーションは、各ブランチ オフィスの間でデータをレプリケートします。

DFS レプリケーションで使わないオフライン ファイル、マルチ ユーザー環境で DFS レプリケーションは、任意の分散のロック メカニズムまたはファイルのチェック アウト機能を提供しないためです。 2 人のユーザーは、異なるサーバーで同時に同じファイルを変更する場合、古いファイルは、DfsrPrivate に移動 DFS レプリケーション\\次のレプリケーション中に ConflictandDeleted フォルダー (レプリケート フォルダーのローカル パスの下にあります)。

### <a name="what-antivirus-applications-are-compatible-with-dfs-replication"></a>DFS レプリケーションとの互換性のあるウイルス対策アプリケーションですか。

過度のレプリケーションは、スキャンのアクティビティは、レプリケートされたフォルダー内のファイルを変更する場合、ウイルス対策アプリケーションで発生することができます。 詳細については、 [DFS レプリケーションとウイルス対策アプリケーションの相互運用テスト](http://go.microsoft.com/fwlink/?linkid=73990)(http://go.microsoft.com/fwlink/?LinkId=73990) します。

### <a name="what-are-the-benefits-of-using-dfs-replication-instead-of-windows-sharepoint-services"></a>Windows SharePoint Services ではなく、DFS レプリケーションを使用する利点とは

Windows® SharePoint® Services に DFS レプリケーションはないファイルのチェック アウト機能の形式で緊密な一貫性を提供します。 複数の人が同じファイルの編集に関する懸念がある場合は、Windows SharePoint Services の使用をお勧めします。 Windows SharePoint Services 2.0 Service Pack 2 では使用可能な Windows Server 2003 R2 の一部として。 Windows SharePoint Services は、Microsoft Web サイトからダウンロードできます。新しいバージョンの Windows Server では含まれません。 ただし、複数のサイト間でデータをレプリケートする場合、ユーザーが同時に同じファイルを編集できません DFS レプリケーションにはより広い帯域幅と簡単に管理が提供します。

## <a name="limitations-and-requirements"></a>制限事項と要件

### <a name="can-dfs-replication-replicate-between-branch-offices-without-a-vpn-connection"></a>DFS レプリケーションは VPN 接続がないブランチ オフィスの間でレプリケートできますか。

[はい]-ブランチ オフィスに接続するプライベート ワイド エリア ネットワーク (WAN) リンク (インターネットではなく) があると仮定します。 ただし、外部ファイアウォールで適切なポートを開く必要があります。 DFS レプリケーションには、RPC エンドポイント マッパー (ポート 135) および 1024 より大きい場合は、ランダムに割り当てられたエフェメラル ポートが使用されます。 使用することができます、 **Dfsrdiag**エフェメラル ポートではなく静的ポートを指定するコマンド ライン ツール。 RPC エンドポイント マッパーを指定する方法の詳細については、次を参照してください。 [154596](http://go.microsoft.com/fwlink/?linkid=73991)でマイクロソフト サポート技術情報 (http://go.microsoft.com/fwlink/?LinkId=73991) します。

### <a name="can-dfs-replication-replicate-files-encrypted-with-the-encrypting-file-system"></a>DFS レプリケーションは暗号化ファイル システムで暗号化されたファイルをレプリケートできますか。

No. DFS レプリケーションは、ファイルや暗号化ファイル システム (EFS) を使用して暗号化されているフォルダーにはレプリケートされません。 ユーザーがレプリケートされていたファイルを暗号化する場合、DFS レプリケーションはレプリケーション グループの他のすべてのメンバーからファイルを削除します。 これにより、ファイルののみ使用可能なコピーがサーバー上の暗号化されたバージョンであります。

### <a name="can-dfs-replication-replicate-outlook-pst-or-microsoft-office-access-database-files"></a>DFS レプリケーションに Outlook の .pst ファイルまたは Microsoft Office Access データベース ファイルをレプリケートできますか。

DFS レプリケーションはレプリケーションを安全に Microsoft Outlook 個人フォルダーのファイル (.pst) および Microsoft Access ファイルこれらは、アーカイブ用に保存され、(を .pst ファイルまたはアクセスを開く Outlook またはアクセスなどのクライアントを使用して、ネットワーク経由でアクセスしない場合にのみファイル、まず、ファイルをコピー、ローカル記憶装置)。 この理由は次のとおりです。

  - ネットワーク接続経由での .pst ファイルを開くと、.pst ファイル内のデータが破損する可能性があります。 .Pst ファイル安全にアクセスできない理由から、ネットワーク経由での詳細については、次を参照してください。[記事 297019](http://go.microsoft.com/fwlink/?linkid=125363)でマイクロソフト サポート技術情報 (http://go.microsoft.com/fwlink/?LinkId=125363) します。  
      
  - .pst ファイルおよびファイルへのアクセスは、Outlook、Office Access などのクライアントによってアクセスされることに時間が長期間開いたままにする傾向があります。 これは DFS レプリケーションが閉じられるまで、これらのファイルをレプリケートすることを防ぎます。  
      

### <a name="can-i-use-dfs-replication-in-a-workgroup"></a>ワークグループで DFS レプリケーションを使用することができますか。

No. DFS レプリケーションは、構成に対する Active Directory® ドメイン サービスに依存します。 ドメイン内にのみ機能します。

### <a name="can-more-than-one-folder-be-replicated-on-a-single-server"></a>1 台のサーバーでは、複数のフォルダーをレプリケートできますか。

[はい]。 DFS レプリケーションは、サーバー間で多数のフォルダーをレプリケートすることができます。 一意の各レプリケート フォルダーができるようにルートのパスと重複しないことです。 たとえば、d:\\Sales と d:\\アカウンティングが 2 つのレプリケートされたフォルダーが d: のルート パスを指定できます\\Sales と d:\\Sales\\レポートが 2 つのレプリケート フォルダーのルート パスにすることはできません。

### <a name="does-dfs-replication-require-dfs-namespaces"></a>DFS レプリケーションは DFS 名前空間が必要ですか。

No. DFS レプリケーションと DFS 名前空間は、個別にまたは組み合わせて使用できます。 DFS レプリケーションを使用して、FRS. でできることではないスタンドアロン DFS 名前空間をレプリケートするさらに、

### <a name="does-dfs-replication-require-time-synchronization-between-servers"></a>DFS レプリケーションはサーバー間で時刻の同期が必要ですか。

No. DFS レプリケーションは、サーバー間の時刻同期を明示的に要求されません。 ただし、DFS レプリケーションでは、サーバーのクロックを近づける必要。 サーバーのクロックは、Kerberos 認証を正常に機能 (既定) には、それぞれの 5 分以内で設定する必要があります。 たとえば、DFS レプリケーションでは、タイムスタンプを使用して、どのファイルが優先の競合が発生した場合を判断します。 正確な時間もガベージ コレクション、スケジュール、およびその他の機能にとって重要です。

### <a name="does-dfs-replication-support-replicating-an-entire-volume"></a>DFS レプリケーションはボリューム全体をレプリケートするか。

[はい]。 ただし、Windows Server 2003 Service Pack 2 または修正プログラムを最初にインストールする必要があります。 詳細については、次を参照してください。[記事 920335](http://go.microsoft.com/fwlink/?linkid=76776)でマイクロソフト サポート技術情報 (http://go.microsoft.com/fwlink/?LinkId=76776) します。 さらに、ボリューム全体をレプリケートするには、次の問題が発生します。

  - ボリュームには、Windows ページング ファイルが含まれる、レプリケーションは失敗し、DFSR イベント 4312 システム イベント ログでログに記録されます。  
      
  - DFS レプリケーションは、移行先サーバー上のレプリケート フォルダーのシステムと非表示属性を設定します。 これは、Windows がボリュームのルート フォルダーに既定では、システムおよび非表示属性を適用するために発生します。 移行先サーバー上のレプリケート フォルダーのローカル パスがボリュームのルートもある場合は、フォルダーの属性をさらに変更が行われません。  
      
  - Windows システム フォルダーを含むボリュームをレプリケートするときに、DFS レプリケーションは、%WINDIR% フォルダーを認識し、レプリケートしません。 ただし、DFS レプリケーションは、アプリケーションが DFS レプリケーションとの相互運用性の問題がある場合、移行先サーバーに、アプリケーションで障害が発生可能性があります、Microsoft 以外のアプリケーションで使用されるフォルダーをレプリケートします。  
      

### <a name="does-dfs-replication-support-rpc-over-http"></a>DFS レプリケーションは、HTTP 経由で RPC をサポートしますか。

No.

### <a name="does-dfs-replication-work-across-wireless-networks"></a>DFS レプリケーションは、ワイヤレス ネットワークの間で動作しますか。

[はい]。 DFS レプリケーションは、接続の種類に依存しません。

### <a name="does-dfs-replication-work-on-refs-or-fat-volumes"></a>DFS レプリケーションは、ReFS ボリュームまたは FAT ボリュームに動作しますか。

No. DFS レプリケーションのみで、NTFS ファイル システムでフォーマットされたボリュームをサポートしていますResilient File System (ReFS) および FAT ファイル システムはサポートされていません。 DFS レプリケーションでは、NTFS の変更ジャーナルを使用しており、その他の機能、NTFS ファイル システムのために NTFS が必要です。

### <a name="does-dfs-replication-work-with-sparse-files"></a>DFS レプリケーションは、スパース ファイルで動作しますか。

[はい]。 スパース ファイルをレプリケートすることができます。 **Sparse**受信メンバーの属性が保持されます。

### <a name="do-i-need-to-log-in-as-administrator-to-replicate-files"></a>ファイルをレプリケートするには管理者としてログインする必要がありますか。

No. DFS レプリケーションは、レプリケートするには管理者としてログインする必要はありませんので、ローカル システム アカウントで実行されるサービスです。 ただし、DFS レプリケーションの構成を変更するには、ドメイン管理者または影響を受けるファイル サーバーのローカルの管理者をする必要があります。

詳細についてで「DFS レプリケーションのセキュリティ要件と委任」を参照、 [DFS レプリケーションを管理する権限を委任](http://go.microsoft.com/fwlink/?linkid=182294)(http://go.microsoft.com/fwlink/?LinkId=182294) します。

### <a name="how-can-i-upgrade-or-replace-a-dfs-replication-member"></a>アップグレードまたは DFS レプリケーションのメンバーを置換する方法は?

アップグレードするか、DFS レプリケーションのメンバーを置換するには、ブログ Ask で Directory Services Team ブログの投稿を参照してください。[DFSR メンバーのハードウェアまたは OS を置き換える](http://blogs.technet.com/b/askds/archive/2010/09/10/series-wrap-up-and-downloads-replacing-dfsr-member-hardware-or-os.aspx)します。

### <a name="is-dfs-replication-suitable-for-replicating-roaming-profiles"></a>DFS レプリケーションはローミング プロファイルをレプリケートするために適していますか。

[はい]。 移動ユーザー プロファイルをレプリケートするときに、特定のシナリオはサポートされています。 サポートされるシナリオについては、次を参照してください。[マイクロソフトのサポート ステートメントをレプリケートされたユーザー プロファイル データ](http://go.microsoft.com/fwlink/?linkid=201282)(http://go.microsoft.com/fwlink/?LinkId=201282) します。

### <a name="is-there-a-file-character-limit-or-limit-to-the-folder-depth"></a>文字の制限をファイルまたはフォルダの深さに制限はありますか。

Windows および DFS レプリケーションは、最大 32 桁の文字を含むフォルダーのパスをサポートします。 DFS レプリケーションでは、260 文字のフォルダーのパスに限定されません。

### <a name="must-members-of-a-replication-group-reside-in-the-same-domain"></a>レプリケーション グループのメンバーは同じドメイン内にする必要がありますか。

No. レプリケーション グループは、別のフォレスト全体ではなくが、1 つのフォレスト内のドメイン間にまたがることができます。

### <a name="what-are-the-supported-limits-of-dfs-replication"></a>DFS レプリケーションのサポートされている制限とは

一連の Microsoft Windows Server 2012 R2 上でテスト済みのスケーラビリティのガイドラインを次に示します。

  - サーバー上のすべてのレプリケートされたファイルのサイズ:100 のテラバイト以上。  
      
  - ボリューム上のレプリケートされたファイルの数:7,000万件です。  
      
  - 最大ファイル サイズ:250 ギガバイトです。  
      


> [!IMPORTANT]
> 多数のファイルのサイズと、レプリケーション グループを作成するときに、データベースの複製をエクスポートして、事前シード処理の手法を使用する初期レプリケーションの実行時間を最小限に抑えるお勧めします。 詳細については、次を参照してください。 <A href="http://blogs.technet.com/b/filecab/archive/2013/08/21/dfs-replication-initial-sync-in-windows-server-2012-r2-attack-of-the-clones.aspx">Windows Server 2012 R2 の DFS レプリケーションの初期同期。クローンの攻撃</A>します。 
<br>


一連の Windows Server 2012、Windows Server 2008 R2、および Windows Server 2008 で Microsoft によってテスト済みのスケーラビリティのガイドラインを次に示します。

  - サーバー上のすべてのレプリケートされたファイルのサイズ:10 テラバイトです。  
      
  - ボリューム上のレプリケートされたファイルの数:11 ドルです。  
      
  - 最大ファイル サイズ:64 ギガバイトです。  
      


> [!NOTE]
> レプリケーション グループ、レプリケート フォルダー、接続、またはレプリケーション グループのメンバーの数に制限はありません。 
<br>


Windows Server 2003 R2 の Microsoft によってテスト済みのスケーラビリティに関するガイドラインの一覧は、次を参照してください。 [DFS レプリケーションのスケーラビリティに関するガイドライン](http://go.microsoft.com/fwlink/?linkid=75043)(http://go.microsoft.com/fwlink/?LinkId=75043) します。

### <a name="when-should-i-not-use-dfs-replication"></a>いないように使い分ければよい DFS レプリケーションでしょうか。

複数のユーザーが更新または、別のサーバー上で同時に同じファイルを変更する環境では、DFS レプリケーションを使用しません。 DFS レプリケーション ファイルのコピーが競合しているを非表示の DfsrPrivate に移動する原因になります\\ConflictandDeleted フォルダー。

複数のユーザーは、異なるサーバーで同時に同じファイルを変更する必要があります、Windows SharePoint Services のファイルのチェック アウト機能を使用して、その 1 つだけのユーザーがファイルを操作することを確認します。 Windows SharePoint Services 2.0 Service Pack 2 では使用可能な Windows Server 2003 R2 の一部として。 Windows SharePoint Services は、Microsoft Web サイトからダウンロードできます。新しいバージョンの Windows Server では含まれません。

### <a name="why-is-a-schema-update-required-for-dfs-replication"></a>DFS レプリケーションに必要なスキーマの更新はなぜですか。

DFS レプリケーションでは、Active Directory Domain Services のドメイン名前付けコンテキストで新しいオブジェクトを使用して、構成情報を格納します。 Active Directory ドメイン サービス スキーマを更新すると、これらのオブジェクトが作成されます。 詳細については、次を参照してください。 [DFS レプリケーションの要件をレビュー](http://go.microsoft.com/fwlink/?linkid=182264) (http://go.microsoft.com/fwlink/?LinkId=182264) します。

## <a name="monitoring-and-management-tools"></a>監視および管理ツール

### <a name="can-i-automate-the-health-report-to-receive-warnings"></a>警告を受信する正常性レポートを自動化することができますか。

[はい]。 正常性レポートを自動化する 3 つの方法はあります。

  - 正常性レポートを定期的に生成するのにには、スケジュールされたタスクと組み合わせて、Windows Server 2012 R2 または DfsrAdmin.exe に含まれる DFSR の Windows PowerShell モジュールを使用します。 詳細については、次を参照してください。 [DFS レプリケーションの正常性レポートの自動化](http://go.microsoft.com/fwlink/?linkid=74010)(http://go.microsoft.com/fwlink/?LinkId=74010) します。  
      
  - System Center Operations Manager 用の DFS レプリケーションの管理パックを使用すると、指定した条件に基づいてアラートを作成できます。  
      
  - 警告のスクリプトを DFS レプリケーション WMI プロバイダーを使用します。  
      

### <a name="can-i-use-microsoft-system-center-operations-manager-to-monitor-dfs-replication"></a>Microsoft System Center Operations Manager を使用して、DFS レプリケーションを監視できますか。

[はい]。 詳細については、次を参照してください。、 [System Center Operations Manager 2007 用の DFS レプリケーションの管理パック](http://go.microsoft.com/fwlink/?linkid=182265)、Microsoft ダウンロード センター (http://go.microsoft.com/fwlink/?LinkId=182265) します。

### <a name="does-dfs-replication-support-remote-management"></a>DFS レプリケーションは、リモート管理をサポートしますか。

[はい]。 DFS レプリケーションは、DFS の管理コンソールを使用してリモート管理をサポートしていると、**レプリケーション グループの追加**コマンド。 たとえば、サーバー A、サーバー A と B のメンバーとして持つフォレストで定義されたレプリケーション グループに接続できます。

DFS の管理は、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008、および Windows Server 2003 R2 に含まれています。 Windows の他のバージョンから DFS レプリケーションを管理するには、リモート デスクトップを使用または[リモート サーバー管理ツールの Windows 7](https://technet.microsoft.com/library/Ee449475)します。


> [!IMPORTANT]
> を表示または読み取り専用のレプリケート フォルダーまたはフェールオーバー クラスターであるメンバーを含むレプリケーション グループを管理するには、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、、に含まれているDFSの管理のバージョンを使用する必要があります<a href="http://go.microsoft.com/fwlink/p/?linkid=238560">Windows 8 用リモート サーバー管理ツール</a>、または<a href="https://technet.microsoft.com/library/ee449475">Windows 7 用のリモート サーバー管理ツール</a>します。 
<br>


### <a name="do-ultrasound-and-sonar-work-with-dfs-replication"></a>Ultrasound と Sonar うまく DFS レプリケーションを使用しますか。

No. DFS レプリケーションには、監視および診断ツールの独自セットがあります。 Ultrasound と Sonar が FRS. を監視できるのみ

### <a name="how-can-files-be-recovered-from-the-conflictanddeleted-or-preexisting-folders"></a>ファイルは、ConflictAndDeleted または PreExisting フォルダーからどのように回復できるでしょうか。

ファイルの復元、ファイル システム フォルダーまたはファイルの履歴を使用して共有フォルダーからファイルを復元する、**以前のバージョンを復元**エクスプ ローラーで、またはバックアップからファイルを復元することによってコマンド。 ConflictAndDeleted または PreExisting フォルダーから直接ファイルを回復するには、使用、`Get-DfsrPreservedFiles`と`Restore-DfsrPreservedFiles`(Windows Server 2012 R2 の DFSR モジュールに含まれます)、Windows PowerShell コマンドレットまたは[RestoreDFSR](http://code.msdn.microsoft.com/restoredfsr)MSDN コード ギャラリーからのサンプル スクリプトです。 このスクリプトは、ディザスター リカバリーのためにだけ使用し、提供 AS-保証も伴わず、です。

### <a name="is-there-a-way-to-know-the-state-of-replication"></a>レプリケーションの状態を把握する方法はありますか。

[はい]。 レプリケーションを監視する方法を数多くあります。

  - DFS レプリケーションでは、プロアクティブな監視を提供する System Center Operations Manager 管理パックがあります。  
      
  - DFS の管理は、レプリケーションのバックログ、レプリケーションの効率性、および特定のレプリケーション グループのファイルとフォルダーの数の組み込みの診断レポートが。  
      
  - Windows Server 2012 R2 の DFSR の Windows PowerShell モジュールには、伝達テストを開始し、伝達と正常性レポートを作成するためのコマンドレットが含まれています。 詳細については、次を参照してください。[分散ファイル システム レプリケーション Windows PowerShell コマンドレット](https://technet.microsoft.com/library/dn296601.aspx)します。  
      
  - Dfsrdiag.exe は、バックログの数またはトリガー伝達テストを生成できるコマンド ライン ツールです。 両方のレプリケーションの状態が表示されます。 伝達は、ファイルがすべてのノードにレプリケートされるかどうかを示します。 バックログには、ファイルの数が 2 台のコンピューターが同期される前にレプリケートする必要がありますが表示されます。バックログの数は、レプリケーション グループのメンバーが処理されていない更新プログラムの数です。 Windows Server 2012 R2、Windows Server 2012 または Windows Server 2008 R2 を実行するコンピューターで、Dfsrdiag.exe は、DFS レプリケーションが現在レプリケートしている更新プログラムにも表示できます。  
      
  - スクリプトは、WMI を使用して、バックログの情報を収集する — 手動でまたは MOM を使用します。  
      

## <a name="performance"></a>パフォーマンス

### <a name="does-dfs-replication-support-dial-up-connections"></a>DFS レプリケーションは、ダイヤルアップ接続をサポートしますか。

DFS レプリケーションではダイヤルアップの速度で動作する多数の変更のレプリケートがある場合バックログを取得できます。 既存のファイルには、小さな変更が加えられた、Remote Differential Compression (RDC) での DFS レプリケーションは、ファイルを直接コピーするよりもはるかに高いパフォーマンスを提供します。

### <a name="does-dfs-replication-perform-bandwidth-sensing"></a>DFS レプリケーションは、帯域幅の検出を実行しますか。

No. DFS レプリケーションでは、帯域幅の検出は実行されません。 (帯域幅の調整) 接続ごとに帯域幅の制限の量を使用する、DFS レプリケーションを構成することができます。 ただし、DFS レプリケーションはさらに縮小されません帯域幅使用率、ネットワーク インターフェイスが飽和し、短い時間では、DFS レプリケーションにより、リンクが飽和状態ことができる場合。 DFS レプリケーションは RPC 呼び出しの調整によって調整される帯域幅の調整のため、帯域幅調整の DFS レプリケーションでは完全に正確ではありません。 その結果、RPC を含むネットワーク スタックの下位レベルでのさまざまなバッファーが干渉し、ネットワーク トラフィックの急激な増加の原因します。

### <a name="does-dfs-replication-throttle-bandwidth-per-schedule-per-server-or-per-connection"></a>DFS レプリケーションは、スケジュール、サーバー、または 1 つの接続の帯域幅を調整しますか。

スケジュールを指定する場合に帯域幅の調整を構成する場合は、そのレプリケーション グループのすべての接続は帯域幅の調整の設定を使用します。 帯域幅の調整は、DFS の管理を使用して、接続レベルの設定としても設定することができます。

### <a name="does-dfs-replication-use-active-directory-domain-services-to-calculate-site-links-and-connection-costs"></a>DFS レプリケーションは、サイト リンクと接続のコストを計算するのに Active Directory Domain Services を使用しますか。

No. DFS レプリケーションは、これはサイト コストを Active Directory Domain Services に依存しないと、管理者によって定義されたトポロジを使用します。

### <a name="how-can-i-improve-replication-performance"></a>レプリケーションのパフォーマンスを向上させる方法は?

レプリケーションのパフォーマンスのチューニングのさまざまな方法の詳細については、次を参照してください。 [DFSR でレプリケーションのパフォーマンス チューニング](http://blogs.technet.com/b/askds/archive/2010/03/31/tuning-replication-performance-in-dfsr-especially-on-win2008-r2.aspx)上、[への質問 Directory Services Team ブログ](http://blogs.technet.com/b/askds/)します。

### <a name="how-does-dfs-replication-avoid-saturating-a-connection"></a>DFS レプリケーションは接続の飽和をどのように回避するのでしょうか。

DFS レプリケーションでは、接続で使用する最大帯域幅を設定し、サービスは、ネットワーク使用率のレベルを保持します。 これは異なるから、バック グラウンド インテリジェント転送サービス (BITS)、あり、適切に設定した場合に、DFS レプリケーションで、接続が飽和されません。

それでも、100% 正確でない、帯域幅の調整と、短時間では、DFS レプリケーションにより、リンクが飽和状態ことができます。 DFS レプリケーションは、RPC 呼び出しの調整によって調整される帯域幅を調整するためです。 このプロセスは、RPC を含む、ネットワーク スタックの下位レベルでのさまざまなバッファーに依存しているために、レプリケーション トラフィックは、ネットワーク リンクをワークロードが時を大量に移動する傾向があります。

Windows Server 2008 での DFS レプリケーションにはで説明したようにいくつかのパフォーマンス強化が含まれます[分散ファイル システム](https://technet.microsoft.com/library/Cc753479)、トピック[で変更された Windows Server 2003 SP1 から Windows Server の機能2008](https://technet.microsoft.com/library/cc753208)します。

### <a name="how-does-dfs-replication-performance-compare-with-frs"></a>FRS と DFS レプリケーションのパフォーマンスを比較方法はありますか

DFS レプリケーションは、特に大きなファイルを小さな変更が行われ、RDC が有効になっている場合に FRS をより高速です。 など、RDC で 2 MB PowerPoint® プレゼンテーションを少し変更する可能性がのみ 60 キロバイト (KB、ネットワーク経由で送信される)、転送されたバイト数の 97% の割引。

RDC で使用されていないファイル 64 KB 未満とできない高速の Lan のネットワーク帯域幅が競合はありません。 DFS の管理を使用して接続ごとには、RDC を無効にすることができます。

### <a name="how-frequently-does-dfs-replication-replicate-data"></a>DFS レプリケーションが、データをレプリケートする頻度

設定したスケジュールに従ってデータをレプリケートします。 たとえば、するスケジュールを設定できます、15 分間隔を週 7 日。 これらの間隔中にレプリケーションを有効にします。 レプリケーションでは、(通常は数秒で)、ファイルの変更が検出された後すぐに開始されます。

接続スケジュールは、受信メンバーのローカル時刻に設定されているレプリケーション グループのスケジュールを世界協定時刻 (UTC) に設定することがあります。 レプリケーション グループが複数のタイム ゾーンにまたがるときに、にこれを考慮します。 現地時刻では、受信接続をホストしているメンバーの時間を意味します。 受信接続と対応する送信接続の表示されているスケジュールは、現地時刻にスケジュールが設定されている場合、タイム ゾーンの違いを反映します。

### <a name="how-much-of-my-servers-system-resources-will-dfs-replication-consume"></a>サーバーのシステム リソースの量が DFS レプリケーションを使用しますか?

ディスク、メモリ、および DFS レプリケーションで使用される CPU リソースは、変更、レプリケーション グループのメンバーの数、およびレプリケート フォルダーの数の割合、ファイルのサイズと数などの要因の数によって異なります。 さらに、いくつかのリソースを推定する難しくなります。 たとえば、DFS レプリケーション データベースで使用する Extensible Storage Engine (ESE) テクノロジは、オンデマンドで解放される、使用可能なメモリの大部分を利用できます。 サーバーの構成に応じて、同じサーバーでは、DFS レプリケーション以外のアプリケーションをホストすることができます。 ただし、複数のアプリケーションまたは単一のサーバーでサーバーの役割をホストする場合、運用環境で実装する前に、この構成をテストすることが重要です。

### <a name="what-happens-if-a-wan-link-fails-during-replication"></a>レプリケーション中に WAN 接続に失敗するとどうなりますか。

接続がダウンした場合、DFS レプリケーションは、スケジュールが開いている間にレプリケートするを続けます。 (アラート) を事前に MOM と DFS レプリケーションの正常性レポート (リアクティブ、ときに管理者がこれを実行) などを使用して収集できる DFS レプリケーション イベント ログに記載されている接続のエラーもあります。

## <a name="remote-differential-compression-details"></a>リモートの差分圧縮の詳細

### <a name="are-changes-compressed-before-being-replicated"></a>変更がレプリケートされる前に圧縮されますか。

[はい]。 ファイルの変更部分がすべてのファイル (既に圧縮) を次を除くの種類に送信される前に圧縮: .wma、.wmv、.zip、.jpg、.mpg、.mpeg、.m1v、.mp2、.mp3、.mpa、.cab、.wav、.snd、.au、.asf、.wm、.avi、システム、.gz、.tgz、およびインポートします。 これらのファイルの種類の圧縮設定では、Windows Server 2003 R2 で構成できません。

### <a name="can-an-administrator-turn-off-rdc-or-change-the-threshold"></a>管理者はできます RDC オフにするか、しきい値を変更しますか。

[はい]。 特定の接続のプロパティ ページで、RDC オフにすることができます。 RDC を無効にすると、CPU 使用率とレプリケーションの待機時間で高速ローカル エリア ネットワーク (LAN) リンク帯域幅の制約がないまたは主に 64 KB よりも小さいファイルで構成される、レプリケーション グループを削減できます。 接続で RDC を無効にすることを選択する場合は、レプリケーションのパフォーマンスを向上することを確認する変更の前後にレプリケーションの効率性をテストします。

使用して、RDC サイズのしきい値を変更することができます、 **Dfsradmin 接続設定**コマンド、DFS レプリケーション WMI プロバイダー、またはファイルを手動で構成 XML を編集します。

### <a name="does-rdc-work-on-all-file-types"></a>RDC は、すべてのファイルの種類に動作しますか。

[はい]。 RDC は、ファイル データの種類に関係なく、ブロック レベルで差分を計算します。 ただし、RDC は、Word 文書、PST ファイル、VHD イメージなどの特定のファイル種類ではより効率的に機能します。

### <a name="how-does-rdc-work-on-a-compressed-file"></a>圧縮ファイルで RDC のしくみ

DFS レプリケーションでは、RDC で、計算が変更され、ネットワーク経由でそれらのブロックのみを送信するファイルのブロックを使用します。 DFS レプリケーションは、ファイルの内容について何も知る必要はありません: ブロックのみが変更されました。

### <a name="is-cross-file-rdc-enabled-when-upgrading-to-windows-server-enterprise-edition-or-datacenter-edition"></a>Windows Server Enterprise Edition または Datacenter Edition にアップグレードするときに有効になっている RDC ファイル間でしょうか。

Windows Server の Standard エディションをサポートしていない RDC ファイル間。 ただし、サポートしていますが、RDC ファイル間をエディションにアップグレードする場合、またはレプリケーション接続のメンバーには、サポートされているエディションが実行されている場合は自動的に有効です。 レプリケート ファイル RDC をサポートするエディションの一覧は、ファイル間 RDC のどのエディションの Windows オペレーティング システムのサポートを参照してください。

### <a name="is-rdc-true-block-level-replication"></a>RDC は true。 ブロック レベルのレプリケーションとは

No. RDC は、ファイル転送の圧縮の汎用プロトコルです。 DFS レプリケーションは、RDC を使用して、ディスクのブロック レベルではなくファイル レベルでブロックします。 RDC は、ファイルをブロックに分割します。 ファイル内の各ブロックに対してより大きなブロックを表すことのできるバイト数が少ないのは、署名を計算します。 一連のシグネチャは、サーバーからクライアントに転送されます。 クライアントでは、独自にサーバーの署名と比較します。 クライアントを要求、サーバーが既にクライアントではない署名のデータのみを送信します。

### <a name="what-happens-if-i-rename-a-file"></a>ファイルの名前を変更するとどうなりますか。

DFS レプリケーションでは、次のレプリケーション中に他のすべてのレプリケーション グループのメンバーでファイルを変更します。 ファイルは、追跡対象一意の ID を使用して、そのため、ファイルの名前を変更および移動、レプリカ内のファイルは、ファイルをレプリケートする DFS レプリケーションの機能に影響を与えません。

### <a name="what-is-cross-file-rdc"></a>RDC をファイル間は何ですか。

ファイル間 RDC により、DFS レプリケーションと同じ名前のファイルがクライアント側に存在しない場合でも、RDC を使用します。 ファイル間 RDC では、ヒューリスティックを使用して、レプリケートする必要のあるファイルのようなファイルを決定し、WAN 経由で転送されるデータの量を最小限に抑えるにレプリケートするファイルと同じですが、同様のファイルのブロックを使用します。 ファイル間 RDC は、このプロセスで最大 5 つのようなファイルのブロックを使用できます。

使用する RDC ファイル間レプリケーション接続の 1 つのメンバーする必要がありますが、実行、Windows のエディション レプリケート ファイル RDC をサポートしています。 レプリケート ファイル RDC をサポートするエディションの一覧は、ファイル間 RDC のどのエディションの Windows オペレーティング システムのサポートを参照してください。

### <a name="what-is-rdc"></a>RDC は何ですか。

リモート differential compression (RDC) は、帯域幅が制限ネットワーク経由でファイルを効率的に更新するのに使用できるクライアント/サーバー プロトコルです。 RDC により、ファイルでは、挿入、削除、およびデータの再配置を検出ファイルが更新されたときにのみ、変更のレプリケートに DFS レプリケーションの有効化が実現します。 RDC は、既定で以上 64 KB であるファイルに対してのみ使用されます。 RDC は、以前のバージョンのファイルを使用して、レプリケート フォルダー内、または、DfsrPrivate では、同じ名前を持つ\\ConflictandDeleted のフォルダー (レプリケート フォルダーのローカル パスの下にあります)。

### <a name="when-is-rdc-used-for-replication"></a>RDC はレプリケーションで使用される場合

RDC はファイルが最小サイズのしきい値を超えた場合に使用されます。 このサイズのしきい値は、既定で 64 KB です。 そのしきい値を超えるファイルがレプリケートされて、更新されたバージョンのファイルは、ファイルの大部分が変更されたか、RDC を無効にしない限り、常に、RDC を使用します。

### <a name="which-editions-of-the-windows-operating-system-support-cross-file-rdc"></a>のどのエディションの Windows オペレーティング システムのサポートにファイル間 RDC がでしょうか。

使用する RDC ファイル間レプリケーション接続の 1 つのメンバーする必要がありますが、実行、エディション、Windows オペレーティング システムのレプリケート ファイル RDC をサポートしています。 次の表は、Windows オペレーティング システムのエディションのサポートにファイル間 RDC が。

### <a name="cross-file-rdc-availability-in-editions-of-the-windows-operating-system"></a>Windows オペレーティング システムのエディションで RDC 可用性のファイル間します。

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>オペレーティング システムのバージョン</th>
<th>Standard Edition</th>
<th>Enterprise Edition</th>
<th>Datacenter Edition</th>
</tr>
</thead>
<tbody>
<tr class="even">
<td><p>Windows Server 2012 R2</p></td>
<td><p>うん<em></p></td>
<td><p>使用できません</p></td>
<td><p>〇</em></p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2012</p></td>
<td><p>〇</p></td>
<td><p>使用できません</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2008 R2</p></td>
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2008</p></td>
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2003 R2</p></td>
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>

\* 無効にすることができます必要に応じて Windows Server 2012 R2 で RDC ファイル間。

## <a name="replication-details"></a>レプリケーションの詳細

### <a name="can-i-change-the-path-for-a-replicated-folder-after-it-is-created"></a>作成した後、レプリケート フォルダーのパスを変更できますか。

No. レプリケート フォルダーのパスを変更する必要がある場合を DFS の管理では削除し、新しいレプリケート フォルダーとして再度追加する必要があります。 DFS レプリケーションは、Remote Differential Compression (RDC) を使用して、データが送信と受信メンバーで同じかどうかを判別する同期を実行します。 フォルダー内のすべてのデータをもう一度レプリケートにはされません。

### <a name="can-i-configure-which-file-attributes-are-replicated"></a>レプリケートされるファイル属性を構成できますか。

いいえ、DFS レプリケーションによってレプリケートされるファイル属性を構成することはできません。

属性値とその説明の一覧は、次を参照してください。[ファイル属性](http://go.microsoft.com/fwlink/?linkid=182268)msdn (http://go.microsoft.com/fwlink/?LinkId=182268) します。

次の属性値を使用して設定されて、`SetFileAttributes dwFileAttributes`関数、およびそれらが DFS レプリケーションによってレプリケートされます。 これらの属性値への変更は、属性のレプリケーションをトリガーします。 内容にも変更しない限り、ファイルの内容はレプリケートされません。 詳細については、次を参照してください。 [SetFileAttributes 関数](http://go.microsoft.com/fwlink/?linkid=182269)、MSDN ライブラリ (http://go.microsoft.com/fwlink/?LinkId=182269) します。

  - ファイル\_属性\_非表示  
      
  - ファイル\_属性\_読み取り専用  
      
  - ファイル\_属性\_システム  
      
  - ファイル\_属性\_いない\_コンテンツ\_インデックス  
      
  - ファイル\_属性\_オフライン  
      

次の属性値は、DFS レプリケーションによってレプリケートされますが、レプリケーションをトリガーしません。

  - ファイル\_属性\_アーカイブ  
      
  - ファイル\_属性\_標準  
      

次のファイル属性の値は、レプリケーションもトリガーを使用して、設定することはできませんが、`SetFileAttributes`関数 (を使用して、`GetFileAttributes`属性値を表示する関数)。

  - ファイル\_属性\_再解析\_ポイント  
      

> [!NOTE]
> DFS レプリケーションは、再解析タグが IO_REPARSE_TAG_SYMLINK でない限り、再解析ポイントの属性の値をレプリケートしません。 Io_reparse_tag_dedup を含む、IO_REPARSE_TAG_SIS または IO_REPARSE_TAG_HSM 再解析タグを持つファイルは、通常のファイルとしてレプリケートされます。 ただし、再解析タグと再解析データ バッファーはレプリケートされません他のサーバーに再解析ポイントがローカル システムでのみ機能するため。 
<br>

  - ファイル\_属性\_圧縮  
      
  - ファイル\_属性\_暗号化  
      

> [!NOTE]
> DFS レプリケーションでは、暗号化ファイル システム (EFS) を使用して暗号化されたファイルはレプリケートされません。 DFS レプリケーションでは、Microsoft 以外のソフトウェアを使用して暗号化されたが、ファイルの FILE_ATTRIBUTE_ENCRYPTED 属性の値を設定しない場合にのみファイルをレプリケートします。 
<br>

  - ファイル\_属性\_SPARSE\_ファイル  
      
  - ファイル\_属性\_ディレクトリ  
      

DFS レプリケーションは、ファイルをレプリケートしません\_属性\_一時的な値。

### <a name="can-i-control-which-member-is-replicated"></a>メンバーのレプリケートを制御できますか。

[はい]。 レプリケーション グループを作成するときに、トポロジを選択できます。 選択または**トポロジ**し、レプリケーション グループが作成された後に手動で接続を構成しません。

### <a name="can-i-seed-a-replication-group-member-with-data-prior-to-the-initial-replication"></a>初期レプリケーションの前にデータをレプリケーション グループのメンバーをシードできますか。

[はい]。 DFS レプリケーションは、初期レプリケーション前に、レプリケーション グループのメンバーにファイルのコピーをサポートします。 この「事前登録」では、初期レプリケーションでレプリケートされたデータの量を大幅に削減できます。

初期レプリケーションは、ファイルが、実際の属性またはタイムスタンプのみが異なる場合に、内容をレプリケートする必要はありません。 実際の属性は、Win32 関数によって設定できる属性`SetFileAttributes`します。 詳細については、次を参照してください。 [SetFileAttributes 関数](http://go.microsoft.com/fwlink/?linkid=182269)、MSDN ライブラリ (http://go.microsoft.com/fwlink/?LinkId=182269) します。 2 つのファイル圧縮などの他の属性が異なる場合、ファイルの内容はレプリケートされます。

レプリケーション グループのメンバーを事前設定するには、移行先サーバー上の適切なフォルダーにファイルをコピー、レプリケーション グループを作成およびプライマリ メンバーを選択します。 プライマリ メンバーの内容が「優先」と見なされるためにレプリケートする、最新のファイルを持つメンバーを選択します。 これは、初期レプリケーションの際、プライマリ メンバーのファイルにより常に上書きされるレプリケーション グループの他のメンバー上のファイルの他のバージョンを意味します。

事前シード処理し、DFSR データベースを複製する方法については、次を参照してください。 [Windows Server 2012 R2 の DFS レプリケーションの初期同期。クローンの攻撃](http://blogs.technet.com/b/filecab/archive/2013/08/21/dfs-replication-initial-sync-in-windows-server-2012-r2-attack-of-the-clones.aspx)します。

初期レプリケーションの詳細については、次を参照してください。[レプリケーション グループを作成する](https://technet.microsoft.com/library/cc725893)します。

### <a name="does-dfs-replication-overcome-common-file-replication-service-issues"></a>DFS レプリケーションは、ファイル レプリケーション サービスの一般的な問題を克服しますか。

[はい]。 DFS レプリケーションは、FRS の 3 つの一般的な問題を解決します。

  - ジャーナル ラップします。DFS レプリケーションは、その場でジャーナル ラップから復元します。 既存のファイルまたはフォルダーが journalWrap としてマークされているし、レプリケーションをもう一度有効にする前に、ファイル システムに対して検証します。 復元中は、このボリュームは、どちらの方向のレプリケーションで利用可能ではありません。  
      
  - 過剰なレプリケーションの場合:過度のレプリケーションを防ぐには、DFS レプリケーションは、クレジットのシステムを使用します。  
      
  - 変形フォルダーがあります。変形フォルダー名を防ぐためには、DFS レプリケーションでは、非表示の DfsrPrivate に競合するデータを格納\\ConflictandDeleted のフォルダー (レプリケート フォルダーのローカル パスの下にあります)。 たとえば、FRS を使用してレプリケートされた別のサーバーに同じ名前の同時に複数のフォルダーを作成すると、古いフォルダーの名前を変更する FRS が。 代わりに、DFS レプリケーションでは、古いフォルダーがローカル競合して削除されたフォルダーに移動します。  
      

### <a name="does-dfs-replication-replicate-files-in-chronological-order"></a>DFS レプリケーションは、時系列内のファイルをレプリケートしますか。

No. 誤順序のファイルをレプリケートする場合があります。

### <a name="does-dfs-replication-replicate-files-that-are-being-used-by-another-application"></a>DFS レプリケーションは、別のアプリケーションによって使用されているファイルをレプリケートしますか。

アプリケーションはファイルを開き、ファイルのロックを作成します (他のアプリケーションで開いているときに使用されるを防止) に場合、DFS レプリケーションはレプリケートされませんファイル閉じられるまでです。 アプリケーションでは、共有読み取りアクセス権を持つファイルを開き、ファイルがレプリケートもできます。

### <a name="does-dfs-replication-replicate-ntfs-file-permissions-alternate-data-streams-hard-links-and-reparse-points"></a>DFS レプリケーションは NTFS ファイル アクセス許可、代替データ ストリーム、ハード リンクをレプリケートして、再解析ポイントですか。

  - DFS レプリケーションは、NTFS ファイル アクセス許可と代替データ ストリームを複製します。  
      
  - Microsoft は、レプリケート フォルダーの NTFS ハード リンクの作成とファイルの間をサポートしていません-実行発生する可能性がレプリケーションの問題の影響を受けるファイル。 ハード リンク ファイルは、DFS レプリケーションでは無視されはレプリケートされません。 接合ポイントはレプリケートされません、し、DFS レプリケーションが発生した各接合ポイント イベント 4406 ログに記録します。  
      
  - DFS レプリケーションによりレプリケートされる唯一の再解析ポイントは、IO を使用するような\_再解析\_タグ\_シンボリック リンク タグです。 ただし、DFS レプリケーションとは限りませんシンボリック リンクのターゲットがレプリケートされます。 詳細については、次を参照してください。、[への質問 Directory Services Team ブログ](http://blogs.technet.com/b/askds/archive/2011/09/30/friday-mail-sack-super-slo-mo-edition.aspx)します。  
      
  - ファイル IO を\_再解析\_タグ\_重複除去、IO\_再解析\_タグ\_SIS、または IO\_再解析\_タグ\_HSM の再解析タグがレプリケートされます通常のファイルとして 再解析タグと再解析データ バッファーはレプリケートされません他のサーバーに再解析ポイントがローカル システムでのみ機能するため。 そのため、DFS レプリケーションは、Windows Server 2012、または単一インスタンス記憶域 (SIS) でデータ重複除去を使用しているボリューム上のフォルダーをレプリケートできます、役割サービスを有効にする各サーバーでデータ重複除去の情報を個別に管理は、ただし、します。  
      

### <a name="does-dfs-replication-replicate-timestamp-changes-if-no-other-changes-are-made-to-the-file"></a>場合は、ファイルにその他の変更は行われません、タイムスタンプの変更のレプリケートを DFS レプリケーションはでしょうか。

いいえ、DFS レプリケーションでは、ファイルの唯一の違いは、タイムスタンプの変更はレプリケートされません。 さらに、ファイルに変更されていない場合、レプリケーション グループの他のメンバーに変更されたタイムスタンプはレプリケートされません。

### <a name="does-dfs-replication-replicate-updated-permissions-on-a-file-or-folder"></a>ファイルまたはフォルダーで DFS レプリケーション レプリケート更新されたアクセス許可のでしょうか

[はい]。 DFS レプリケーションは、ファイルとフォルダーのアクセス許可の変更をレプリケートします。 アクセス制御リスト (ACL) に関連付けられているファイルの一部のみをレプリケートすると、DFS レプリケーションは、ステージング領域にファイル全体を読み取るもする必要があります。


> [!NOTE]
> 多数のファイルの Acl を変更すると、レプリケーションのパフォーマンスに影響があります。 ただし、RDC を使用する場合、転送データの量はファイル全体のサイズではなく、Acl のサイズに比例します。 ディスク トラフィックの量は、ステージング フォルダーとファイルを読み取る必要がありますので、ファイルのサイズにも比例します。 
<br>


### <a name="does-dfs-replication-support-merging-text-files-in-the-event-of-a-conflict"></a>DFS レプリケーションは、競合が発生した場合のテキスト ファイルのマージをサポートしますか。

DFS レプリケーションは、競合がある場合、ファイルをマージできません。 ただし、非表示の DfsrPrivate 内のファイルの古いバージョンを保持するためにしようとして\\ConflictandDeleted コンピューターのフォルダーに、競合が検出されました。

### <a name="does-dfs-replication-use-encryption-when-transmitting-data"></a>データを送信するときに、暗号化の使用を DFS レプリケーションはでしょうか。

[はい]。 DFS レプリケーションは、暗号化、リモート プロシージャ コール (RPC) 接続を使用します。

### <a name="is-it-possible-to-disable-the-use-of-encrypted-rpc"></a>暗号化された RPC の使用を無効にすることはできますか。

No. DFS レプリケーション サービスでは、TCP 経由でリモート プロシージャ コール (RPC) を使用して、データをレプリケートします。 認証レベルの定数を常に使用する、DFS レプリケーション サービスを設計、インターネット経由でデータ転送をセキュリティで保護`RPC_C_AUTHN_LEVEL_PKT_PRIVACY`します。 これにより、インターネット経由で RPC 通信が常に暗号化されています。 そのため、DFS レプリケーション サービスによって暗号化された RPC の使用を無効にすることはできません。

詳細については、次の Microsoft Web サイトを参照してください。

  - [RPC のテクニカル リファレンス](http://go.microsoft.com/fwlink/?linkid=182278)  
      
  - [Remote Differential Compression について](http://go.microsoft.com/fwlink/?linkid=182279)  
      
  - [認証レベルの定数](http://go.microsoft.com/fwlink/?linkid=182280)  
      

### <a name="how-are-simultaneous-replications-handled"></a>同時のレプリケーションの処理方法

レプリケート フォルダーごとに 1 つの更新マネージャーがあります。 それぞれ独立して作業をマネージャーを更新します。

既定では最大 16 (4 つの Windows Server 2003 R2) の同時ダウンロード数は、すべての接続とレプリケーション グループ間で共有します。 接続およびレプリケーション グループの更新プログラムがシリアル化されないために、更新プログラムが受信される特定の順序はありません。 2 つのスケジュールが開かれている場合の更新プログラムの一般に受け取りし、同時に両方の接続からインストールします。

### <a name="how-do-i-force-replication-or-polling"></a>レプリケーションまたはポーリングを強制する方法は?

強制的にレプリケーションすぐに、DFS の管理を使用する」の説明に従って[レプリケーション スケジュールの編集](https://technet.microsoft.com/library/Cc732278)します。 使用してレプリケーションを強制することもできます、`Sync-DfsReplicationGroup`コマンドレットは、Windows Server 2012 R2 で導入された DFSR PowerShell モジュールに含まれる、または**Dfsrdiag SyncNow**コマンド。 使用してポーリングを強制することができます、`Update-DfsrConfigurationFromAD`コマンドレット、または**Dfsrdiag PollAD**コマンド。

### <a name="is-it-possible-to-configure-a-quiet-time-between-replications-for-files-that-change-frequently"></a>頻繁に変更されるファイルのレプリケーションの間の待ち時間を構成することはできますか。

No. スケジュールが開いている場合、それらを認識すると、DFS レプリケーションは変更をレプリケートします。 ファイルの時間帯を構成する方法はありません。

### <a name="is-it-possible-to-configure-one-way-replication-with-dfs-replication"></a>DFS レプリケーションと一方向のレプリケーションを構成することはできますか。

[はい]。 Windows Server 2012 または Windows Server 2008 R2 を使用している場合は、一方向の接続経由でコンテンツをレプリケートするための読み取り専用レプリケート フォルダーを作成できます。 詳細については、次を参照してください。[ことを特定のメンバーで、フォルダーのレプリケートされた読み取り専用](http://go.microsoft.com/fwlink/?linkid=156740)(http://go.microsoft.com/fwlink/?LinkId=156740) します。

Windows Server 2008 または Windows Server 2003 R2 での DFS レプリケーションと、一方向のレプリケーション接続を作成することはできません。 そうと、正常性チェックのトポロジ エラー、ステージングの問題、および DFS レプリケーション データベースの問題を含む多数の問題が発生することができます。

Windows Server 2008 または Windows Server 2003 R2 を使用している場合は、次の操作を実行して一方向の接続をシミュレートできます。

  - プライマリ サーバーとして指定するサーバーでのみ変更する管理者を教育します。 その後、変更内容を移行先サーバーにレプリケートします。  
      
  - エンドユーザーに書き込みアクセス許可が必要があるないように、移行先サーバーに共有アクセス許可を構成します。 変更は許可されません、ブランチ サーバーへのレプリケーション、何もないし、一方向の接続をシミュレートし、WAN の使用率を推し進める場合。  
      

### <a name="is-there-a-way-to-force-a-complete-replication-of-all-files-including-unchanged-files"></a>未変更のファイルを含むすべてのファイルの完全なレプリケーションを強制する方法はありますか。

No. DFS レプリケーションは、同じファイルを考慮する場合にレプリケートされません。 変更されたファイルがレプリケートされていない場合は、DFS レプリケーションは自動的にこれらをレプリケートするように構成されている場合。 構成されたスケジュールを上書きするには、WMI メソッドを使用して**ForceReplicate()** します。 ただし、これはのみ、スケジュールを変更して、変更されていない、または同一のファイルのレプリケーションを強制しません。

### <a name="what-happens-if-the-primary-member-suffers-a-database-loss-during-initial-replication"></a>プライマリ メンバーは、初期レプリケーション中にデータベースの損失を悪化するとどうなりますか。

初期レプリケーションの際、プライマリ メンバーのファイルが常に優先受信側メンバーにプライマリ メンバー上のファイルの異なるバージョンがある場合に発生する競合の解決でします。 Active Directory Domain services では、プライマリ メンバーの指定が格納されているし、レプリケーションのすべてのメンバー グループのレプリケート前に、プライマリ メンバーが、レプリケート準備済みの表記がクリアされます。

場合は、初期レプリケーションが失敗するか、レプリケーション中、DFS レプリケーション サービスの再起動、プライマリ メンバーは、ローカルの DFS レプリケーション データベースにプライマリ メンバーの指定を認識し、初期レプリケーションを再試行します。 Active Directory Domain services では、プライマリの表記を消去した後にプライマリ メンバーの DFS レプリケーション データベースが失われた場合は、レプリケーション グループのすべてのメンバーは、初期レプリケーションを完了する前に、レプリケーション グループのすべてのメンバーに失敗します。フォルダーをレプリケートして、プライマリ メンバーとしてサーバーが指定されていないためです。 この場合、使用、 **Dfsradmin メンバーシップ/set/isprimary:true**プライマリ メンバー サーバーのプライマリ メンバーの指定を手動で復元するコマンド。

初期レプリケーションの詳細については、次を参照してください。[レプリケーション グループを作成する](https://technet.microsoft.com/library/cc725893)します。


> [!WARNING]
> プライマリ メンバーの指定は、初期レプリケーション プロセス中にのみ使用されます。 使用する場合、 <STRONG>Dfsradmin</STRONG>レプリケート フォルダーのレプリケーション後のプライマリ メンバーが完了したら、DFS レプリケーションは Active Directory Domain Services にプライマリ メンバーとして、サーバーを指定しないを指定するコマンド。 ただし、サーバー上の DFS レプリケーション データベースは、その後、元に戻せない破損やデータ損失が低下すれば場合、サーバーは、レプリケーションの別のメンバーからのデータの回復ではなく、プライマリ メンバーとして、初期レプリケーションを実行しようとグループ。 基本的には、サーバーでは、競合が発生することができますが、悪意のあるプライマリ サーバーになります。 このため、初期レプリケーションが失敗した修復不可能の場合のみ、プライマリ メンバーを手動で指定します。 
<br>


### <a name="what-happens-if-the-replication-schedule-closes-while-a-file-is-being-replicated"></a>ファイルがレプリケートされ、レプリケーション スケジュールが終了するとどうなりますか。

接続でリモート differential compression (RDC) が有効な場合は、スケジュールの終了する直前にレプリケートを開始した、64 KB を超えるファイルのレプリケーションを受信 (または変更する**No 帯域幅**) ときに引き続き、スケジュールが表示されます (以外のものに変更または**No 帯域幅**)。 レプリケーションは、レプリケーションが停止したときの状態から続行されます。

RDC を無効にすると、DFS レプリケーションは、ファイル転送を完全に再起動します。 これは、ファイルが受信側のメンバーで使用可能な場合に遅れることができます。

### <a name="what-happens-when-two-users-simultaneously-update-the-same-file-on-different-servers"></a>2 人のユーザーが同時に複数のサーバー上の同じファイルを更新すると起こりますか。

DFS レプリケーションは、競合を検出した、最後に保存されたファイルのバージョンが使用されます。 これは、他のファイルを DfsrPrivate に移動\\ConflictandDeleted フォルダー (競合を解決しているコンピューター上のレプリケート フォルダーのローカル パス) の下。 競合して削除されたフォルダーがクリーンアップ、競合して削除されたフォルダーは、構成済みのサイズを超えています。 または、DFS レプリケーションには、ディスク領域のエラーが発生したときに発生するまで残りますがあります。 競合して削除されたフォルダーはレプリケートされずの競合の解決には、このメソッドが FRS. で可能に変形ディレクトリの問題を回避します。

競合が発生するときに、DFS レプリケーションは、DFS レプリケーションのイベント ログに情報イベントを記録します。 このイベントには、次の理由でユーザーの操作が不要します。

  - これは (サーバー管理者にのみ表示される) のユーザーに表示されません。  
      
  - 競合して削除されたフォルダーは、DFS レプリケーションは、キャッシュとして扱います。 クォータのしきい値に達すると、それらのファイルの一部をクリーンアップします。 競合するファイルが保存される保証はありません。  
      
  - 競合は、競合の元とは別のサーバー上に存在でした。  
      

## <a name="staging"></a>ステージング

### <a name="does-dfs-replication-continue-staging-files-when-replication-is-disabled-by-a-schedule-or-bandwidth-throttling-quota-or-when-a-connection-is-manually-disabled"></a>DFS レプリケーションは、スケジュールまたは帯域幅クォータの調整によってレプリケーションが無効にした場合、または接続を手動で無効にするファイルのステージングを続行しますか。

No. 帯域幅調整のクォータを超過した場合、または接続が無効にした場合は、DFS レプリケーションはスケジュールされたレプリケーションの時間、外部ファイルのステージングには続行されません。

### <a name="does-dfs-replication-prevent-other-applications-from-accessing-a-file-during-staging"></a>DFS レプリケーションは他のアプリケーションがステージング中に、ファイルへのアクセスを防止しますか。

No. DFS レプリケーションは、ユーザーや、レプリケーション フォルダーでファイルを開くアプリケーションをブロックしない方法でファイルを開きます。 このメソッドは「便宜的ロック」と呼ばれます

### <a name="is-it-possible-to-change-the-location-of-the-staging-folder-with-the-dfs-management-tool"></a>DFS 管理ツールを使用してステージング フォルダーの場所を変更することはできますか。

[はい]。 ステージング フォルダーの場所が構成されて、**詳細**のタブ、**プロパティ**レプリケーション グループのメンバーごとのダイアログ ボックス。

### <a name="when-are-files-staged"></a>ファイルがステージングされますか。

受信側のメンバーは、ファイルを要求したときに、送信元のメンバーでファイルがステージングされます (ファイルが 64 KB ではない限り、または小さい) 次の表に示すようにします。 256 KB である場合を除き、ファイルがステージングされた接続では、Remote Differential Compression (RDC) が無効である場合または小さくします。 ファイルは、16 KB ~ 1 mb には、この設定を構成する場合は、64 KB 未満のサイズ、転送中にも、受信側メンバーにステージングされます。 スケジュールが閉じている場合、ファイルはステージされませんでした。

### <a name="the-minimum-file-sizes-for-staging-files"></a>ファイルのステージング ファイルの最小サイズ

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th> </th>
<th>RDC が有効になっています。</th>
<th>RDC を無効になっています</th>
</tr>
</thead>
<tbody>
<tr class="even">
<td><p>メンバーを送信します。</p></td>
<td><p>64 KB</p></td>
<td><p>256 KB</p></td>
</tr>
<tr class="odd">
<td><p>受信側メンバー</p></td>
<td><p>既定では 64 KB</p></td>
<td><p>既定では 64 KB</p></td>
</tr>
</tbody>
</table>

### <a name="what-happens-if-a-file-is-changed-after-it-is-staged-but-before-it-is-completely-transmitted-to-the-remote-site"></a>これは、リモート サイトに送信して完全に前に、ステージングした後にファイルが変更するとどうなりますか。

ファイルの任意の部分は、既に転送中は、DFS レプリケーションは、転送を続行します。 DFS レプリケーションは、ファイル転送を開始する前に、ファイルが変更されると、新しいバージョンのファイルが送信されます。

## <a name="change-history"></a>変更履歴


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>日付</th>
<th>説明</th>
<th>Reason</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>2018 年 11 月 15 日</p></td>
<td><p>Windows Server 2019 が更新されました。</p></td>
<td><p>新しいオペレーティング システムです。</p></td>
</tr>
<tr class="even">
<td><p>2013 年 10 月 9 日</p></td>
<td><p>DFS レプリケーションのサポートされている制限とは、更新しますか。Windows Server 2012 R2 でのテストから得られた結果セクション。</p></td>
<td><p>Windows Server の最新バージョンの更新プログラム</p></td>
</tr>
<tr class="odd">
<td><p>2013 年 1 月 30 日</p></td>
<td><p>DFS レプリケーションを追加するスケジュールまたは帯域幅クォータの調整によってレプリケーションが無効にした場合、または接続を手動で無効にするファイルのステージングを続行しますか?エントリ。</p></td>
<td><p>お客様の質問</p></td>
</tr>
<tr class="even">
<td><p>2012 年 10 月 31 日</p></td>
<td><p>DFS レプリケーションのサポートされている制限とは、編集しますか。ボリューム上のレプリケートされたファイルのテストの数を増やすエントリ。</p></td>
<td><p>カスタマー フィードバック</p></td>
</tr>
<tr class="odd">
<td><p>2012 年 8 月 15 日</p></td>
<td><p>DFS レプリケーションのレプリケートの NTFS ファイル アクセス許可、代替データ ストリーム、ハード リンク、および再解析ポイントを編集しますか?エントリをさらに DFS レプリケーションがハード リンクを処理する方法を明確にし、再解析ポイントします。</p></td>
<td><p>カスタマー サポート サービスからのフィードバック</p></td>
</tr>
<tr class="even">
<td><p>2012 年 6 月 13 日</p></td>
<td><p>ReFS ボリュームまたは FAT ボリュームの DFS レプリケーションの作業を編集しますか。ReFS のディスカッションを追加するエントリ。</p></td>
<td><p>カスタマー フィードバック</p></td>
</tr>
<tr class="odd">
<td><p>2012 年 4 月 25 日</p></td>
<td><p>DFS レプリケーションのレプリケートの NTFS ファイル アクセス許可、代替データ ストリーム、ハード リンク、および再解析ポイントを編集しますか?DFS レプリケーションがハード リンクを処理する方法を明確にするエントリ。</p></td>
<td><p>潜在的な混乱を削減します。</p></td>
</tr>
<tr class="even">
<td><p>2011 年 3 月 30 日</p></td>
<td><p>DFS レプリケーションのことができますレプリケート Outlook .pst または Microsoft Office Access データベース ファイルを編集しますか。DFS レプリケーションの .pst ファイルへのアクセスと使用の潜在的な影響を修正するエントリ。</p>
<p>レプリケーションのパフォーマンスを向上する方法を追加しますか?</p></td>
<td><p>前のエントリは、.pst ファイルまたはファイルへのアクセスをレプリケートすると、DFS レプリケーション データベースが壊れる可能性がありますいると正しく指定に関するお客様の質問。</p></td>
</tr>
<tr class="odd">
<td><p>2011 年 1 月 26 日</p></td>
<td><p>どのファイルから回復できる、ConflictAndDeleted を追加または既存のフォルダーですか。</p></td>
<td><p>カスタマー フィードバック</p></td>
</tr>
<tr class="even">
<td><p>2010 年 10 月 20 日</p></td>
<td><p>アップグレードまたはすれば DFS レプリケーションのメンバーを置換を追加しますか。</p></td>
<td><p>カスタマー フィードバック</p></td>
</tr>
</tbody>
</table>

