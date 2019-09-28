---
title: 'DFS レプリケーション: よく寄せられる質問 (FAQ)'
ms.date: 06/18/2014
ms.prod: windows-server
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 12410d619245153f759b54e7a8aff257888f04dc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386072"
---
# <a name="dfs-replication-frequently-asked-questions-faq"></a>DFS レプリケーション: よく寄せられる質問 (FAQ)


更新:2019年4月30日

適用先:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

この FAQ では、Windows Server の分散ファイルシステム (DFS) レプリケーション (DFS-R または DFSR とも呼ばれます) に関する質問に回答します。

Dfs 名前空間の詳細につい[ては、次を参照してください。 dfs 名前空間:よく寄せら](https://technet.microsoft.com/library/ee404780)れる質問。

DFS レプリケーションの新機能の詳細については、次のトピックを参照してください。

  - [DFS 名前空間と DFS レプリケーションの概要](https://technet.microsoft.com/library/jj127250)(Windows Server 2012)  
      
  - [Windows server 2008 から Windows server 2008 R2 への機能の変更](https://technet.microsoft.com/library/dd391932)に関する[分散ファイルシステムの新](https://technet.microsoft.com/library/ee307957)機能に関するトピック  
      
  - [Windows server 2003 SP1 から Windows server 2008 への機能の変更に関する](https://technet.microsoft.com/library/cc753208)[分散ファイルシステム](https://technet.microsoft.com/library/cc753479)のトピック  
      

このトピックに対する最近の変更については、「 [変更履歴](#change-history) 」を参照してください。

      

## <a name="interoperability"></a>相互運用性

### <a name="can-dfs-replication-communicate-with-frs"></a>FRS と DFS レプリケーション通信できますか。

No. DFS レプリケーションは、ファイルレプリケーションサービス (FRS) と通信しません。 DFS レプリケーションと FRS は、同じサーバーで同時に実行できますが、同じフォルダーやサブフォルダーをレプリケートするように構成する必要はありません。これにより、データが失われる可能性があるためです。

### <a name="can-dfs-replication-replace-frs-for-sysvol-replication"></a>SYSVOL レプリケーションに対して FRS を置換 DFS レプリケーションことができます

はい、DFS レプリケーションは、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、または Windows Server 2008 を実行しているサーバーで、SYSVOL レプリケーションの FRS を置き換えることができます。 Windows Server 2003 R2 を実行しているサーバーでは、SYSVOL フォルダーをレプリケートするための DFS レプリケーションの使用はサポートされていません。

DFS レプリケーションを使用した[sysvol のレプリケートの詳細については、次を参照してください。 sysvol レプリケーション移行ガイド:FRS を DFS レプリケーション](https://technet.microsoft.com/library/dd640019)します。

### <a name="can-i-upgrade-from-frs-to-dfs-replication-without-losing-configuration-settings"></a>構成設定を失わずに、FRS から DFS レプリケーションにアップグレードすることはできますか。

可能。 レプリケーションを FRS から DFS レプリケーションに移行するには、次のドキュメントを参照してください。

  - SYSVOL フォルダー以外のフォルダーのレプリケーションを移行するには[、「DFS 操作ガイド:Frs から DFS レプリケーション](http://go.microsoft.com/fwlink/?linkid=192776)および FRS2DFSR への移行[– frs から DFSR への移行ユーティリティ](http://go.microsoft.com/fwlink/?linkid=195437)(http://go.microsoft.com/fwlink/?LinkID=195437) )。  
      
  - Sysvol フォルダーのレプリケーションを DFS レプリケーションに移行する方法に[ついては、次を参照してください。 sysvol レプリケーション移行ガイド:FRS を DFS レプリケーション](https://technet.microsoft.com/library/dd640019)します。  
      

### <a name="can-i-use-dfs-replication-in-a-mixed-windowsunix-environment"></a>混合 Windows/UNIX 環境で DFS レプリケーションを使用できますか。

可能。 DFS レプリケーションは、Windows Server を実行しているサーバー間でのコンテンツのレプリケートのみをサポートしていますが、UNIX クライアントは Windows サーバー上のファイル共有にアクセスできます。 これを行うには、ネットワークファイルシステム (NFS) 用のサービスを DFS レプリケーションサーバーにインストールします。

また、多くの UNIX クライアントに含まれる SMB/CIFS クライアント機能を使用して Windows ファイル共有に直接アクセスすることもできますが、この機能は限られている場合や、Windows 環境の変更が必要になる場合があります (SMB 署名を無効にするなど)。グループポリシー)。

DFS レプリケーションは、Windows Server オペレーティングシステムを実行しているサーバー上の NFS と相互運用できますが、NFS マウントポイントをレプリケートすることはできません。

### <a name="can-i-use-the-volume-shadow-copy-service-with-dfs-replication"></a>DFS レプリケーションでボリュームシャドウコピーサービスを使用できますか。

可能。 DFS レプリケーションはボリュームシャドウコピーサービス (VSS) ボリュームでサポートされています。以前のバージョンのクライアントでは、以前のスナップショットを正常に復元できます。

### <a name="can-i-use-windowsbackup-ntbackupexe-to-remotely-back-up-a-replicated-folder"></a>Windows バックアップ (Ntbackup.exe) を使用して、レプリケートされたフォルダーをリモートでバックアップできますか。

いいえ。 windows server 2003 以前を実行しているコンピューターで Windows バックアップ (Ntbackup.exe) を使用して、Windows Server 2012、Windows Server 2008 R2、または Windows Server 2008 を実行しているコンピューター上のレプリケートフォルダーの内容をバックアップすることはできません。

レプリケートフォルダーに格納されているファイルをバックアップするには、Windows Server バックアップまたは Microsoft® System Center Data Protection Manager を使用します。 Windows Server 2008 R2 および Windows Server 2008 のバックアップと回復の機能の詳細については、「[バックアップと回復](https://technet.microsoft.com/library/Cc754097)」を参照してください。 詳細については、「 [System Center Data Protection Manager](http://go.microsoft.com/fwlink/?linkid=182261) (http://go.microsoft.com/fwlink/?LinkId=182261) 」を参照してください。

### <a name="do-file-system-policies-impact-dfs-replication"></a>ファイルシステムポリシーは DFS レプリケーションに影響しますか。

可能。 レプリケートフォルダーでは、ファイルシステムポリシーを構成しないでください。 ファイルシステムポリシーは、すべてのグループポリシーの更新間隔で NTFS アクセス許可を再適用します。 これにより、ファイルが閉じられるまで開いているファイルはレプリケートされないため、共有違反が発生する可能性があります。

### <a name="does-dfs-replication-replicate-mailboxes-hosted-on-microsoft-exchange-server"></a>Microsoft Exchange Server でホストされているメールボックスは DFS レプリケーションレプリケートされますか?

No. Microsoft Exchange Server でホストされているメールボックスをレプリケートするために DFS レプリケーションを使用することはできません。

### <a name="does-dfs-replication-support-file-screens-created-by-file-server-resource-manager"></a>ファイルサーバーリソースマネージャーによって作成されたファイルスクリーンはサポート DFS レプリケーション。

可能。 ただし、ファイルサーバーリソースマネージャー (FSRM) のファイルスクリーニング設定が、レプリケーションの両端で一致している必要があります。 さらに、DFS レプリケーションには、レプリケーションから特定のファイルとファイルの種類を除外するために使用できるファイルとフォルダー用の独自のフィルターメカニズムがあります。

次に、ファイルスクリーンまたはクォータを実装するためのベストプラクティスを示します。

  - 非表示の DfsrPrivate フォルダーは、クォータまたはファイルスクリーンの対象にすることはできません。  
      
  - スクリーンファイルは、スクリーニングが有効になる前に、レプリケートフォルダーに存在していてはなりません。  
      
  - クォータを有効にするまで、どのフォルダーもクォータを超えることはできません。  
      
  - ハードクォータは慎重に使用する必要があります。 レプリケーショングループの個々のメンバーは、レプリケーションの前にクォータ内にとどまり、ファイルがレプリケートされるときはそれを超えることができます。 たとえば、ユーザーが 10 mb のファイルをサーバー A (ハード制限) にコピーし、別のユーザーがサーバー B に 5 MB のファイルをコピーした場合、次のレプリケーションが発生すると、両方のサーバーがクォータを 5 mb 超えます。 これにより、DFS レプリケーションによってファイルのレプリケートが連続して再試行され、バージョンベクターのホールが発生し、パフォーマンスの問題が発生する可能性があります。  
      

### <a name="is-dfs-replication-cluster-aware"></a>クラスター対応 DFS レプリケーションですか?

はい、windows server 2012 R2 の DFS レプリケーション、Windows Server 2012 および Windows Server 2008 R2 には、レプリケーショングループのメンバーとしてフェールオーバークラスターを追加する機能が含まれています。 詳細については、「[フェールオーバークラスターをレプリケーショングループに追加する](http://go.microsoft.com/fwlink/?linkid=155085)」 (http://go.microsoft.com/fwlink/?LinkId=155085) を参照してください。 Windows Server 2008 R2 より前のバージョンの Windows での DFS レプリケーションサービスは、フェールオーバークラスターと連携するように設計されていないため、サービスは別のノードにフェールオーバーされません。


> [!NOTE]
> DFS レプリケーションでは、クラスターの共有ボリュームでのファイルのレプリケートはサポートされていません。 
<br>


### <a name="is-dfs-replication-compatible-with-data-deduplication"></a>データ重複除去との互換性は DFS レプリケーションますか?

はい、DFS レプリケーションは、Windows Server でデータ重複除去を使用するボリューム上のフォルダーをレプリケートできます。

### <a name="is-dfs-replication-compatible-with-ris-and-wds"></a>DFS レプリケーションは、RIS と WDS と互換性がありますか。

可能。 DFS レプリケーションは、単一インスタンス記憶域 (SIS) が有効になっているボリュームをレプリケートします。 SIS は、リモートインストールサービス (RIS)、Windows 展開サービス (WDS)、および Windows Storage Server によって使用されます。

### <a name="is-it-possible-to-use-dfs-replication-with-offline-files"></a>オフラインファイルで DFS レプリケーションを使用できますか。

一度に1人のユーザーしかファイルに書き込むことができない場合は、DFS レプリケーションとオフラインファイルを安全に使用できます。 これは、2つのブランチオフィス間を移動し、いずれかの分岐で、またはオフライン中にファイルにアクセスできるようにするユーザーに役立ちます。 オフラインファイルは、オフラインで使用するためにファイルをローカルにキャッシュし、各ブランチオフィス間でデータをレプリケート DFS レプリケーションます。

DFS レプリケーションでは分散ロックメカニズムまたはファイルチェックアウト機能が提供されないため、マルチユーザー環境ではオフラインファイルで DFS レプリケーションを使用しないでください。 2人のユーザーが複数のサーバーで同じファイルを同時に変更した場合、DFS レプリケーションは、次\\のレプリケーション時に古いファイルを DfsrPrivate conflictanddeleted および preexisting フォルダー (レプリケートフォルダーのローカルパスの下にあります) に移動します。

### <a name="what-antivirus-applications-are-compatible-with-dfs-replication"></a>DFS レプリケーションと互換性のあるウイルス対策アプリケーションは何ですか。

ウイルス対策アプリケーションでは、レプリケートフォルダー内のファイルがスキャンアクティビティによって変更されると、過剰なレプリケーションが発生する可能性があります。 詳細については、DFS レプリケーション (http://go.microsoft.com/fwlink/?LinkId=73990) ) との[ウイルス対策アプリケーションの相互運用性のテスト](http://go.microsoft.com/fwlink/?linkid=73990)」を参照してください。

### <a name="what-are-the-benefits-of-using-dfs-replication-instead-of-windows-sharepoint-services"></a>Windows SharePoint Services ではなく DFS レプリケーションを使用する利点は何ですか。

Windows® SharePoint® Services では、ファイルのチェックアウト機能の形式において、DFS レプリケーションには厳密な一貫性がありません。 複数のユーザーが同じファイルを編集することが懸念される場合は、Windows SharePoint Services を使用することをお勧めします。 Windows SharePoint Services 2.0 Service Pack 2 は、Windows Server 2003 R2 の一部として提供されています。 Windows SharePoint Services は、Microsoft Web サイトからダウンロードできます。新しいバージョンの Windows Server には含まれていません。 ただし、複数のサイトにデータをレプリケートしていて、ユーザーが同時に同じファイルを編集しない場合、DFS レプリケーションは帯域幅が大きく、管理が簡単になります。

## <a name="limitations-and-requirements"></a>制限事項と要件

### <a name="can-dfs-replication-replicate-between-branch-offices-without-a-vpn-connection"></a>VPN 接続を使用せずにブランチオフィス間でレプリケート DFS レプリケーションできますか。

○ (インターネットではなく) プライベートワイドエリアネットワーク (WAN) リンクがブランチオフィスに接続されていることを前提としています。 ただし、外部ファイアウォールでは、適切なポートを開く必要があります。 DFS レプリケーションでは、RPC エンドポイントマッパー (ポート 135) と、ランダムに割り当てられた一時的なポート1024を使用します。 **Dfsrdiag.exe**コマンドラインツールを使用して、一時ポートではなく静的ポートを指定できます。 RPC エンドポイントマッパーを指定する方法の詳細については、Microsoft サポート技術情報の[記事 154596](http://go.microsoft.com/fwlink/?linkid=73991) (http://go.microsoft.com/fwlink/?LinkId=73991) 「」を参照してください。

### <a name="can-dfs-replication-replicate-files-encrypted-with-the-encrypting-file-system"></a>暗号化ファイルシステムで暗号化されたファイルをレプリケート DFS レプリケーションことはできますか。

No. DFS レプリケーションは、暗号化ファイルシステム (EFS) を使用して暗号化されたファイルまたはフォルダーをレプリケートしません。 ユーザーが以前にレプリケートされたファイルを暗号化した場合、DFS レプリケーションは、レプリケーショングループの他のすべてのメンバーからファイルを削除します。 これにより、ファイルの唯一の使用可能なコピーがサーバー上で暗号化されたバージョンであることが保証されます。

### <a name="can-dfs-replication-replicate-outlook-pst-or-microsoft-office-access-database-files"></a>Outlook の .pst ファイルまたは Microsoft Office Access データベースファイルを DFS レプリケーションレプリケートできますか。

DFS レプリケーションは、Microsoft Outlook の個人用フォルダーファイル (.pst) と Microsoft Access ファイルを安全にレプリケートすることができるのは、アーカイブ目的で保存されていて、Outlook や Access などのクライアントを使用してネットワーク経由でアクセスされていない場合のみです (.pst またはアクセスを開く場合)。ファイルをコピーします。最初にファイルをローカルストレージデバイスにコピーします)。 この理由は次のとおりです。

  - .Pst ファイルをネットワーク接続経由で開くと、.pst ファイルのデータが破損する可能性があります。 ネットワーク経由で pst ファイルに安全にアクセスできない理由の詳細については、Microsoft サポート技術情報の[記事 297019](http://go.microsoft.com/fwlink/?linkid=125363) (http://go.microsoft.com/fwlink/?LinkId=125363) 「」を参照してください。  
      
  - .pst ファイルと Access ファイルは、Outlook や Office Access などのクライアントによってアクセスされている間、長時間開いたままになる傾向があります。 これにより、DFS レプリケーションが閉じられるまでこれらのファイルをレプリケートできなくなります。  
      

### <a name="can-i-use-dfs-replication-in-a-workgroup"></a>ワークグループで DFS レプリケーションを使用できますか。

No. DFS レプリケーションは Active Directory®ドメインサービスを使用して構成します。 ドメイン内でのみ機能します。

### <a name="can-more-than-one-folder-be-replicated-on-a-single-server"></a>1台のサーバーで複数のフォルダーをレプリケートすることはできますか。

可能。 DFS レプリケーションは、サーバー間で多数のフォルダーをレプリケートできます。 各レプリケートフォルダーに一意のルートパスがあり、重複していないことを確認します。 たとえば、d:\\sales と d:\\Accounting は2つのレプリケートフォルダーのルートパスにすることができ\\ますが、d\\:\\sales レポートと d: sales レポートは2つのレプリケートフォルダーのルートパスにすることはできません。

### <a name="does-dfs-replication-require-dfs-namespaces"></a>DFS 名前空間 DFS レプリケーション必要ですか。

No. DFS レプリケーションと DFS 名前空間は、別々に使用することも一緒に使用することもできます。 また、DFS レプリケーションを使用して、FRS ではできなかったスタンドアロン DFS 名前空間をレプリケートできます。

### <a name="does-dfs-replication-require-time-synchronization-between-servers"></a>サーバー間で時刻の同期が必要 DFS レプリケーションですか。

No. DFS レプリケーションでは、サーバー間の時刻の同期は明示的に要求されません。 ただし、DFS レプリケーションでは、サーバーの時計が厳密に一致している必要があります。 Kerberos 認証が正常に機能するためには、サーバークロックを互いに (既定で) 5 分以内に設定する必要があります。 たとえば、DFS レプリケーションは、タイムスタンプを使用して、競合が発生した場合にどのファイルが優先されるかを判断します。 また、ガベージコレクション、スケジュール、およびその他の機能についても、正確な時刻が重要になります。

### <a name="does-dfs-replication-support-replicating-an-entire-volume"></a>ボリューム全体のレプリケートはサポート DFS レプリケーション。

可能。 ただし、最初に Windows Server 2003 Service Pack 2 または修正プログラムをインストールする必要があります。 詳細については、Microsoft サポート技術情報の[記事 920335](http://go.microsoft.com/fwlink/?linkid=76776) (http://go.microsoft.com/fwlink/?LinkId=76776) ) を参照してください。 さらに、ボリューム全体をレプリケートすると、次の問題が発生する可能性があります。

  - ボリュームに Windows ページングファイルが含まれている場合、レプリケーションは失敗し、システムイベントログに DFSR イベント4312が記録されます。  
      
  - DFS レプリケーションは、移行先サーバー上のレプリケートフォルダーのシステム属性と非表示属性を設定します。 これは、既定では、Windows がシステム属性と非表示属性をボリュームルートフォルダーに適用するために発生します。 コピー先のサーバー上のレプリケートフォルダーのローカルパスもボリュームルートである場合は、それ以上の変更はフォルダー属性に対して行われません。  
      
  - Windows システムフォルダーを含むボリュームをレプリケートする場合、DFS レプリケーションは% WINDIR% フォルダーを認識し、レプリケートしません。 ただし、DFS レプリケーションでは、Microsoft 以外のアプリケーションで使用されるフォルダーがレプリケートされるため、アプリケーションに DFS レプリケーションとの相互運用性の問題がある場合は、移行先サーバーでアプリケーションがエラーになる可能性があります。  
      

### <a name="does-dfs-replication-support-rpc-over-http"></a>HTTP 経由で RPC をサポート DFS レプリケーションですか。

No.

### <a name="does-dfs-replication-work-across-wireless-networks"></a>ワイヤレスネットワーク間で DFS レプリケーション動作しますか。

可能。 DFS レプリケーションは、接続の種類に依存しません。

### <a name="does-dfs-replication-work-on-refs-or-fat-volumes"></a>ReFS ボリュームまたは FAT ボリュームでは DFS レプリケーション動作しますか。

No. DFS レプリケーションでは、NTFS ファイルシステムでフォーマットされたボリュームのみがサポートされます。弾性ファイルシステム (ReFS) および FAT ファイルシステムはサポートされていません。 Ntfs の変更ジャーナルや ntfs ファイルシステムのその他の機能を使用するため、DFS レプリケーションには NTFS が必要です。

### <a name="does-dfs-replication-work-with-sparse-files"></a>スパースファイルで DFS レプリケーション動作しますか。

可能。 スパースファイルをレプリケートできます。 **スパース**属性は、受信側メンバーに保持されます。

### <a name="do-i-need-to-log-in-as-administrator-to-replicate-files"></a>ファイルをレプリケートするには、管理者としてログインする必要がありますか。

No. DFS レプリケーションは、ローカルシステムアカウントで実行されるサービスなので、レプリケートするために管理者としてログインする必要はありません。 ただし、DFS レプリケーションの構成に変更を加えるには、影響を受けるファイルサーバーのドメイン管理者またはローカル管理者である必要があります。

詳細については、「 [DFS レプリケーション管理する機能を委任する](http://go.microsoft.com/fwlink/?linkid=182294)(http://go.microsoft.com/fwlink/?LinkId=182294) 」の「セキュリティ要件と委任の DFS レプリケーション」を参照してください。

### <a name="how-can-i-upgrade-or-replace-a-dfs-replication-member"></a>DFS レプリケーションメンバーをアップグレードまたは置換するにはどうすればよいですか。

DFS レプリケーションメンバーをアップグレードまたは置換するには、「ディレクトリサービスチームに質問する」ブログのブログ投稿を参照してください。[DFSR メンバーのハードウェアまたは OS を置き換え](http://blogs.technet.com/b/askds/archive/2010/09/10/series-wrap-up-and-downloads-replacing-dfsr-member-hardware-or-os.aspx)ます。

### <a name="is-dfs-replication-suitable-for-replicating-roaming-profiles"></a>は、ローミングプロファイルのレプリケーションに適して DFS レプリケーションますか。

可能。 移動ユーザープロファイルをレプリケートする場合は、特定のシナリオがサポートされます。 サポートされるシナリオの詳細については、「レプリケートされたユーザープロファイル http://go.microsoft.com/fwlink/?LinkId=201282) データ () に[関するマイクロソフトのサポートステートメント](http://go.microsoft.com/fwlink/?linkid=201282)」を参照してください。

### <a name="is-there-a-file-character-limit-or-limit-to-the-folder-depth"></a>フォルダーの深さにファイル文字の制限または制限がありますか。

Windows と DFS レプリケーションは、最大32000文字のフォルダーパスをサポートしています。 DFS レプリケーションは、260文字のフォルダーパスに制限されていません。

### <a name="must-members-of-a-replication-group-reside-in-the-same-domain"></a>レプリケーショングループのメンバーは同じドメインに存在する必要がありますか。

No. レプリケーショングループは、1つのフォレスト内の複数のドメインにまたがることができますが、異なるフォレストにまたがることはできません。

### <a name="what-are-the-supported-limits-of-dfs-replication"></a>サポートされている DFS レプリケーションの制限は何ですか。

次の一覧は、Windows Server 2012 R2 で Microsoft によってテストされた一連のスケーラビリティガイドラインを示しています。

  - サーバー上のすべてのレプリケートされたファイルのサイズ:100テラバイト。  
      
  - ボリューム上のレプリケートされたファイルの数:7000万。  
      
  - ファイルの最大サイズ:250ギガバイト。  
      


> [!IMPORTANT]
> 多数のファイルを含むレプリケーショングループを作成する場合は、データベースの複製をエクスポートし、シード前の手法を使用して初期レプリケーションの実行時間を最小限に抑えることをお勧めします。 詳細については<A href="http://blogs.technet.com/b/filecab/archive/2013/08/21/dfs-replication-initial-sync-in-windows-server-2012-r2-attack-of-the-clones.aspx">、「Windows Server 2012 R2 での初期同期の DFS レプリケーション」を参照してください。複製</A>の攻撃。 
<br>


次の一覧は、Windows Server 2012、Windows Server 2008 R2、および Windows Server 2008 で Microsoft によってテストされた一連のスケーラビリティガイドラインを示しています。

  - サーバー上のすべてのレプリケートされたファイルのサイズ:10テラバイト。  
      
  - ボリューム上のレプリケートされたファイルの数:1100万。  
      
  - ファイルの最大サイズ:64ギガバイト。  
      


> [!NOTE]
> レプリケーショングループ、レプリケートフォルダー、接続、またはレプリケーショングループのメンバーの数に制限はなくなりました。 
<br>


Windows Server 2003 R2 で Microsoft によってテストされたスケーラビリティガイドラインの一覧については、「 http://go.microsoft.com/fwlink/?LinkId=75043) DFS レプリケーションのスケーラビリティの[ガイドライン](http://go.microsoft.com/fwlink/?linkid=75043)」 (を参照してください。

### <a name="when-should-i-not-use-dfs-replication"></a>DFS レプリケーションを使用しないのはいつですか?

複数のユーザーが同じファイルを異なるサーバー上で同時に更新または変更する環境では、DFS レプリケーションを使用しないでください。 これにより、DFS レプリケーションによって、ファイルの競合するコピーが隠し\\DfsrPrivate conflictanddeleted および preexisting フォルダーに移動される可能性があります。

複数のユーザーが複数のサーバーで同じファイルを同時に変更する必要がある場合は、Windows SharePoint Services のファイルチェックアウト機能を使用して、1人のユーザーのみがファイルに対して作業していることを確認します。 Windows SharePoint Services 2.0 Service Pack 2 は、Windows Server 2003 R2 の一部として提供されています。 Windows SharePoint Services は、Microsoft Web サイトからダウンロードできます。新しいバージョンの Windows Server には含まれていません。

### <a name="why-is-a-schema-update-required-for-dfs-replication"></a>DFS レプリケーションにスキーマの更新が必要なのはなぜですか。

DFS レプリケーションは、Active Directory Domain Services のドメイン名前付けコンテキストで新しいオブジェクトを使用して、構成情報を格納します。 Active Directory ドメイン サービス スキーマを更新すると、これらのオブジェクトが作成されます。 詳細については、「 [DFS レプリケーションの要件の確認](http://go.microsoft.com/fwlink/?linkid=182264)」 (http://go.microsoft.com/fwlink/?LinkId=182264) を参照してください。

## <a name="monitoring-and-management-tools"></a>監視および管理ツール

### <a name="can-i-automate-the-health-report-to-receive-warnings"></a>正常性レポートを自動化して警告を受け取ることはできますか。

可能。 正常性レポートを自動化するには、次の3つの方法があります。

  - Windows Server 2012 R2 または Dfsradmin.exe に含まれる DFSR Windows PowerShell モジュールをスケジュールされたタスクと共に使用して、正常性レポートを定期的に生成します。 詳細については、「 [DFS レプリケーション正常性レポートの自動化](http://go.microsoft.com/fwlink/?linkid=74010)(http://go.microsoft.com/fwlink/?LinkId=74010) )」を参照してください。  
      
  - System Center Operations Manager 用の DFS レプリケーション管理パックを使用して、指定した条件に基づいてアラートを作成します。  
      
  - 警告をスクリプト化するには、DFS レプリケーション WMI プロバイダーを使用します。  
      

### <a name="can-i-use-microsoft-system-center-operations-manager-to-monitor-dfs-replication"></a>Microsoft System Center Operations Manager を使用して DFS レプリケーションを監視できますか。

可能。 詳細については、Microsoft ダウンロードセンター (http://go.microsoft.com/fwlink/?LinkId=182265) ) の「 [System Center Operations Manager 2007 用 DFS レプリケーション管理パック](http://go.microsoft.com/fwlink/?linkid=182265)」を参照してください。

### <a name="does-dfs-replication-support-remote-management"></a>リモート管理はサポート DFS レプリケーションですか。

可能。 DFS レプリケーションは、DFS 管理コンソールおよび **[レプリケーショングループの追加]** コマンドを使用したリモート管理をサポートしています。 たとえば、サーバー A では、メンバーとしてサーバー A および B を持つフォレストで定義されているレプリケーショングループに接続できます。

DFS の管理は、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008、および Windows Server 2003 R2 に含まれています。 他のバージョンの Windows から DFS レプリケーションを管理するには、リモートデスクトップまたは[windows 7 のリモートサーバー管理ツール](https://technet.microsoft.com/library/Ee449475)を使用します。


> [!IMPORTANT]
> 読み取り専用のレプリケートされたフォルダーまたはフェールオーバークラスターであるメンバーを含むレプリケーショングループを表示または管理するには、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、リモートに含まれているバージョンの DFS 管理を使用する必要があります。 <a href="http://go.microsoft.com/fwlink/p/?linkid=238560">Windows 8 用のサーバー管理ツール</a>、または<a href="https://technet.microsoft.com/library/ee449475">windows 7 用のリモートサーバー管理ツール</a>。 
<br>


### <a name="do-ultrasound-and-sonar-work-with-dfs-replication"></a>DFS レプリケーションでは、Ultrasound と Sonar を操作しますか。

No. DFS レプリケーションには、独自の監視ツールと診断ツールのセットがあります。 Ultrasound と Sonar は、FRS の監視のみを行うことができます。

### <a name="how-can-files-be-recovered-from-the-conflictanddeleted-or-preexisting-folders"></a>Conflictanddeleted および preexisting または既存のフォルダーからファイルを回復するにはどうすればよいですか。

失われたファイルを回復するには、ファイル履歴、ファイルエクスプローラーで [以前のバージョンを**復元**] コマンド、またはバックアップからファイルを復元して、ファイルシステムフォルダーまたは共有フォルダーからファイルを復元します。 Conflictanddeleted および preexisting または既存のフォルダーから直接ファイルを回復するに`Get-DfsrPreservedFiles`は`Restore-DfsrPreservedFiles` 、および windows PowerShell コマンドレット (windows Server 2012 R2 の DFSR モジュールに含まれています)、または、MSDN の[restoredfsr](http://code.msdn.microsoft.com/restoredfsr)サンプルスクリプトを使用します。コードギャラリー。 このスクリプトは、ディザスターリカバリーのみを目的としており、そのままでは保証されません。

### <a name="is-there-a-way-to-know-the-state-of-replication"></a>レプリケーションの状態を知る方法はありますか。

可能。 レプリケーションを監視するには、いくつかの方法があります。

  - DFS レプリケーションには、プロアクティブな監視を提供する System Center Operations Manager 用の管理パックが用意されています。  
      
  - DFS の管理には、レプリケーションバックログ、レプリケーションの効率、および特定のレプリケーショングループ内のファイルとフォルダーの数に関する、インボックス診断レポートが用意されています。  
      
  - Windows Server 2012 R2 の DFSR Windows PowerShell モジュールには、伝達テストを開始し、伝達と正常性レポートを作成するためのコマンドレットが含まれています。 詳細については、「 [Windows PowerShell でのレプリケーションコマンドレットの分散ファイルシステム](https://technet.microsoft.com/library/dn296601.aspx)」を参照してください。  
      
  - Dfsrdiag.exe は、バックログカウントを生成したり、伝達テストをトリガーしたりできるコマンドラインツールです。 どちらもレプリケーションの状態を表示します。 伝達により、すべてのノードにファイルがレプリケートされているかどうかが示されます。 バックログには、2台のコンピューターが同期される前にレプリケートする必要があるファイルの数が表示されます。バックログカウントは、レプリケーショングループメンバーが処理していない更新プログラムの数です。 Windows Server 2012 R2、Windows Server 2012、または Windows Server 2008 R2 を実行しているコンピューターでは、Dfsrdiag.exe は、現在レプリケートしている DFS レプリケーションの更新プログラムを表示することもできます。  
      
  - スクリプトは、WMI を使用して、手動または MOM を介して、バックログ情報を収集できます。  
      

## <a name="performance"></a>パフォーマンス

### <a name="does-dfs-replication-support-dial-up-connections"></a>ダイヤルアップ接続は DFS レプリケーションサポートされるのですか。

DFS レプリケーションはダイヤルアップ速度で動作しますが、レプリケートする変更の数が多い場合は、バックログが発生する可能性があります。 既存のファイルに小さな変更が加えられた場合、Remote Differential Compression (RDC) を使用して DFS レプリケーションすると、ファイルを直接コピーする場合よりもはるかに高いパフォーマンスが得られます。

### <a name="does-dfs-replication-perform-bandwidth-sensing"></a>帯域幅の検出 DFS レプリケーション実行されるか。

No. DFS レプリケーションでは、帯域幅の検出は実行されません。 接続ごとに帯域幅の制限を使用するように DFS レプリケーションを構成することができます (帯域幅調整)。 ただし DFS レプリケーションでは、ネットワークインターフェイスが飽和状態になると帯域幅の使用率がさらに減少することはなく、DFS レプリケーションによって短時間にわたってリンクが飽和状態になる可能性があります。 DFS レプリケーションを使用した帯域幅調整は、RPC 呼び出しを制限することで帯域幅を調整 DFS レプリケーションため、完全に正確ではありません。 その結果、ネットワークスタックの下位レベル (RPC を含む) のさまざまなバッファーが干渉し、ネットワークトラフィックが急増する可能性があります。

### <a name="does-dfs-replication-throttle-bandwidth-per-schedule-per-server-or-per-connection"></a>スケジュール、サーバーごと、または接続ごとに帯域幅を調整 DFS レプリケーションますか?

スケジュールを指定するときに帯域幅の調整を構成すると、そのレプリケーショングループのすべての接続で帯域幅の調整にこの設定が使用されます。 帯域幅調整は、DFS 管理を使用して接続レベルの設定として設定することもできます。

### <a name="does-dfs-replication-use-active-directory-domain-services-to-calculate-site-links-and-connection-costs"></a>Active Directory Domain Services DFS レプリケーション使用してサイトリンクと接続コストを計算しますか。

No. DFS レプリケーションは、管理者によって定義されたトポロジを使用します。これは Active Directory Domain Services サイトのコストに依存しません。

### <a name="how-can-i-improve-replication-performance"></a>レプリケーションのパフォーマンスを向上させるにはどうすればよいですか。

レプリケーションのパフォーマンスをチューニングするさまざまな方法につい[ては、「](http://blogs.technet.com/b/askds/archive/2010/03/31/tuning-replication-performance-in-dfsr-especially-on-win2008-r2.aspx) [ディレクトリサービスチームブログ](http://blogs.technet.com/b/askds/)を参照してください。

### <a name="how-does-dfs-replication-avoid-saturating-a-connection"></a>接続の飽和を回避 DFS レプリケーションにはどうすればよいですか。

DFS レプリケーションでは、接続で使用する最大帯域幅を設定し、サービスはそのネットワーク使用率のレベルを維持します。 これはバックグラウンドインテリジェント転送サービス (BITS) とは異なり、適切に設定した場合、DFS レプリケーションによって接続が飽和状態になることはありません。

ただし、帯域幅の調整は 100% 正確ではなく、DFS レプリケーションによって短時間にリンクが飽和状態になる可能性があります。 これは、DFS レプリケーション RPC 呼び出しを制限することで帯域幅を調整するためです。 このプロセスは、RPC などのネットワークスタックの下位レベルにあるさまざまなバッファーに依存しているため、レプリケーショントラフィックが急増し、ネットワークリンクが飽和状態になることがあります。

Windows Server 2008 の DFS レプリケーションには、「 [Windows server 2003 SP1 から Windows server 2008 への機能の変更](https://technet.microsoft.com/library/cc753208)」で[分散ファイルシステム](https://technet.microsoft.com/library/Cc753479)説明されているように、いくつかのパフォーマンスの向上が含まれています。

### <a name="how-does-dfs-replication-performance-compare-with-frs"></a>DFS レプリケーションパフォーマンスを FRS と比較するにはどうすればよいですか。

DFS レプリケーションは、特に大きなファイルに対して小さな変更が行われ、RDC が有効になっている場合に、FRS よりもはるかに高速になります。 たとえば、RDC を使用すると、2 MB の PowerPoint®プレゼンテーションに小さな変更を行うと、60キロバイト (KB) だけがネットワーク経由で送信される可能性があります。これは、転送されたバイト数の 97% です。

RDC は 64 KB 未満のファイルでは使用されず、ネットワーク帯域幅が競合していない高速 Lan ではメリットがない可能性があります。 RDC は、DFS 管理を使用して、接続ごとに無効にすることができます。

### <a name="how-frequently-does-dfs-replication-replicate-data"></a>DFS レプリケーションデータはどのくらいの頻度でレプリケートされるのですか。

設定したスケジュールに従ってデータがレプリケートされます。 たとえば、スケジュールを15分間隔 (週7日) に設定できます。 これらの間隔中に、レプリケーションが有効になります。 ファイル変更が検出されるとすぐにレプリケーションが開始されます (通常は数秒以内)。

接続スケジュールが受信メンバーのローカル時刻に設定されている場合、レプリケーショングループのスケジュールは、協定世界時 (UTC) に設定できます。 レプリケーショングループが複数のタイムゾーンにまたがる場合は、このことを考慮してください。 ローカル時間は、受信接続をホストしているメンバーの時間を意味します。 スケジュールが現地時刻に設定されている場合、受信接続および対応する送信接続の表示スケジュールには、タイムゾーンの違いが反映されます。

### <a name="how-much-of-my-servers-system-resources-will-dfs-replication-consume"></a>サーバーのシステムリソースの使用 DFS レプリケーション量はどれくらいですか?

DFS レプリケーションによって使用されるディスク、メモリ、および CPU リソースは、ファイルの数とサイズ、変更率、レプリケーショングループメンバーの数、レプリケートされたフォルダーの数など、さまざまな要因によって異なります。 また、リソースによっては、推定が困難なものもあります。 たとえば、DFS レプリケーションデータベースに使用される拡張ストレージエンジン (ESE) テクノロジでは、使用可能なメモリの大部分が消費され、必要に応じて解放されます。 DFS レプリケーション以外のアプリケーションは、サーバーの構成に応じて、同じサーバー上でホストできます。 ただし、1台のサーバーで複数のアプリケーションまたはサーバーの役割をホストする場合は、運用環境で実装する前に、この構成をテストすることが重要です。

### <a name="what-happens-if-a-wan-link-fails-during-replication"></a>レプリケーション中に WAN リンクに障害が発生した場合はどうなりますか。

接続がダウンした場合、DFS レプリケーションはスケジュールが開いている間もレプリケートを試行し続けます。 また、DFS レプリケーションイベントログに記録された接続エラーもあります。これは、MOM (アラートを通じて事前に) および DFS レプリケーション正常性レポート (管理者が実行している場合など) を使用して収集できます。

## <a name="remote-differential-compression-details"></a>Remote Differential Compression の詳細

### <a name="are-changes-compressed-before-being-replicated"></a>変更はレプリケートされる前に圧縮されていますか?

可能。 ファイルの変更部分は、(既に圧縮されている) 以下を除くすべての種類のファイルに対して送信される前に圧縮されます。 wma、.wmv、.zip、.jpg、.mpg、mpeg、.m1v、.mp2、.mp3、.wmv、.cab、.wav、snd、au、.asf、wm、.avi、a-z、gz、tgz、および frx の各形式を持つことができません。このような方法です。 これらのファイルの種類の圧縮設定は、Windows Server 2003 R2 では構成できません。

### <a name="can-an-administrator-turn-off-rdc-or-change-the-threshold"></a>管理者は、RDC を無効にしたり、しきい値を変更したりできますか。

可能。 特定の接続のプロパティページを使用して、RDC を無効にすることができます。 RDC を無効にすると、帯域幅の制約がない高速ローカルエリアネットワーク (LAN) リンク、または主に 64 KB 未満のファイルを構成するレプリケーショングループで、CPU 使用率とレプリケーション待機時間が短縮されます。 接続で RDC を無効にする場合は、変更前と変更後のレプリケーション効率をテストして、レプリケーションのパフォーマンスが向上したことを確認します。

RDC サイズのしきい値を変更するには、 **Dfsradmin.exe 接続セット**コマンド、DFS レプリケーション WMI プロバイダーを使用するか、構成 XML ファイルを手動で編集します。

### <a name="does-rdc-work-on-all-file-types"></a>RDC はすべてのファイルの種類で動作しますか。

可能。 RDC では、ファイルのデータ型に関係なく、ブロックレベルでの相違が計算されます。 ただし、Word 文書、PST ファイル、VHD イメージなどの特定のファイルの種類では、RDC の方が効率的に動作します。

### <a name="how-does-rdc-work-on-a-compressed-file"></a>圧縮されたファイルでの RDC の動作

DFS レプリケーションは、変更されたファイル内のブロックを計算し、それらのブロックのみをネットワーク経由で送信する RDC を使用します。 DFS レプリケーションでは、ファイルの内容について何も知る必要はありません。変更されたブロックのみです。

### <a name="is-cross-file-rdc-enabled-when-upgrading-to-windows-server-enterprise-edition-or-datacenter-edition"></a>Windows Server Enterprise Edition または Datacenter Edition にアップグレードするときに、ファイル間 RDC が有効になっていますか?

Windows Server の Standard Edition では、ファイル間 RDC はサポートされていません。 ただし、ファイル間 RDC をサポートするエディションにアップグレードする場合、またはレプリケーション接続のメンバーがサポートされているエディションを実行している場合は、自動的に有効になります。 ファイル間 RDC をサポートするエディションの一覧については、「ファイル間 RDC をサポートする Windows オペレーティングシステムのエディション」を参照してください。

### <a name="is-rdc-true-block-level-replication"></a>RDC true ブロックレベルのレプリケーションですか?

No. RDC は、ファイル転送を圧縮する汎用プロトコルです。 DFS レプリケーションは、ディスクブロックレベルではなく、ファイルレベルのブロックに対して RDC を使用します。 RDC はファイルをブロックに分割します。 ファイル内の各ブロックに対して、より大きなブロックを表すことのできるバイト数が少ない、署名を計算します。 署名のセットは、サーバーからクライアントに転送されます。 クライアントは、サーバーの署名をそれ自体と比較します。 クライアントは、クライアントにまだ存在しない署名のデータのみを送信するようにサーバーに要求します。

### <a name="what-happens-if-i-rename-a-file"></a>ファイル名を変更するとどうなりますか。

DFS レプリケーションは、次のレプリケーション時に、レプリケーショングループの他のすべてのメンバーのファイルの名前を変更します。 ファイルは一意の ID を使用して追跡されるので、ファイルの名前を変更し、レプリカ内のファイルを移動しても、ファイルをレプリケートする DFS レプリケーションの機能には影響しません。

### <a name="what-is-cross-file-rdc"></a>ファイル間 RDC とは何ですか。

ファイル間 RDC を使用すると、クライアント側で同じ名前のファイルが存在しない場合でも、DFS レプリケーションで RDC を使用できます。 ファイル間 RDC では、ヒューリスティックを使用して、レプリケートする必要があるファイルに類似したファイルを特定し、レプリケートファイルと同一の類似ファイルのブロックを使用して、WAN 経由で転送されるデータの量を最小限に抑えます。 ファイル間 RDC では、このプロセスで最大5つの類似ファイルのブロックを使用できます。

ファイル間 RDC を使用するには、レプリケーション接続の1つのメンバーが、ファイル間 RDC をサポートする Windows のエディションを実行している必要があります。 ファイル間 RDC をサポートするエディションの一覧については、「ファイル間 RDC をサポートする Windows オペレーティングシステムのエディション」を参照してください。

### <a name="what-is-rdc"></a>RDC とは

Remote differential compression (RDC) は、制限された帯域幅のネットワーク経由でファイルを効率的に更新するために使用できるクライアントサーバープロトコルです。 RDC は、ファイル内のデータの挿入、削除、および再配置を検出し、ファイルが更新された場合にのみ、DFS レプリケーションが変更をレプリケートできるようにします。 RDC は、既定では 64 KB 以上のファイルに対してのみ使用されます。 RDC では、レプリケートされたフォルダーまたは DfsrPrivate\\conflictanddeleted および preexisting フォルダー (レプリケートフォルダーのローカルパスの下にある) で同じ名前を持つ古いバージョンのファイルを使用できます。

### <a name="when-is-rdc-used-for-replication"></a>レプリケーションに RDC を使用する場合

RDC は、ファイルが最小サイズのしきい値を超えた場合に使用されます。 既定では、このサイズのしきい値は 64 KB です。 このしきい値を超えるファイルがレプリケートされると、ファイルの大きな部分が変更されたり、RDC が無効になっていない限り、ファイルの更新バージョンでは常に RDC が使用されます。

### <a name="which-editions-of-the-windows-operating-system-support-cross-file-rdc"></a>ファイル間 RDC はどのエディションの Windows オペレーティングシステムでサポートされていますか。

ファイル間 RDC を使用するには、レプリケーション接続の1つのメンバーが、ファイル間 RDC をサポートする Windows オペレーティングシステムのエディションを実行している必要があります。 次の表は、Windows オペレーティングシステムのどのエディションでファイル間 RDC がサポートされているかを示しています。

### <a name="cross-file-rdc-availability-in-editions-of-the-windows-operating-system"></a>Windows オペレーティングシステムの各エディションでのファイル間 RDC の可用性

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
<td><p>〇<em></p></td>
<td><p>使用できません</p></td>
<td><p>はい</em></p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2012</p></td>
<td><p>はい</p></td>
<td><p>使用できません</p></td>
<td><p>はい</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2008 R2</p></td>
<td><p>いいえ</p></td>
<td><p>はい</p></td>
<td><p>はい</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2008</p></td>
<td><p>いいえ</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2003 R2</p></td>
<td><p>いいえ</p></td>
<td><p>はい</p></td>
<td><p>いいえ</p></td>
</tr>
</tbody>
</table>

\*必要に応じて、Windows Server 2012 R2 でファイル間 RDC を無効にすることができます。

## <a name="replication-details"></a>レプリケーションの詳細

### <a name="can-i-change-the-path-for-a-replicated-folder-after-it-is-created"></a>レプリケートフォルダーの作成後に、そのパスを変更できますか。

No. レプリケートフォルダーのパスを変更する必要がある場合は、DFS 管理でそのパスを削除し、新しいレプリケートフォルダーとして追加し直す必要があります。 次に、remote Differential Compression (RDC) を使用して、送信メンバーと受信メンバーのデータが同じであるかどうかを判断する同期を実行します。 DFS レプリケーション フォルダー内のすべてのデータが再度レプリケートされるわけではありません。

### <a name="can-i-configure-which-file-attributes-are-replicated"></a>レプリケートするファイル属性を構成できますか。

いいえ。 DFS レプリケーションレプリケートするファイル属性を構成することはできません。

属性値とその説明の一覧については、MSDN の「[ファイル属性](http://go.microsoft.com/fwlink/?linkid=182268)」 (http://go.microsoft.com/fwlink/?LinkId=182268) を参照してください。

次の属性値は、 `SetFileAttributes dwFileAttributes`関数を使用して設定され、DFS レプリケーションによってレプリケートされます。 これらの属性値を変更すると、属性のレプリケーションがトリガーされます。 コンテンツが変更されない限り、ファイルの内容はレプリケートされません。 詳細については、MSDN ライブラリの「 [Setfileattributes 関数](http://go.microsoft.com/fwlink/?linkid=182269)」 (http://go.microsoft.com/fwlink/?LinkId=182269) を参照してください。

  - ファイル\_属性\_の非表示  
      
  - ファイル\_属性\_読み取り専用  
      
  - ファイル\_属性\_システム  
      
  - コンテンツ\_\_\_にインデックスが設定されていないファイル属性\_  
      
  - ファイル\_属性\_をオフラインにする  
      

次の属性値は DFS レプリケーションによってレプリケートされますが、レプリケーションはトリガーされません。

  - ファイル\_属性\_アーカイブ  
      
  - ファイル\_属性\_-標準  
      

次のファイル属性値もレプリケーションをトリガーしますが、 `SetFileAttributes`関数を使用して設定することはできません (属性値を表示するには`GetFileAttributes`関数を使用します)。

  - ファイル\_\_属性\_の再解析ポイント  
      

> [!NOTE]
> 再解析タグが IO_REPARSE_TAG_SYMLINK されていない場合、DFS レプリケーションは再解析ポイントの属性値をレプリケートしません。 IO_REPARSE_TAG_DEDUP、IO_REPARSE_TAG_SIS、または IO_REPARSE_TAG_HSM の再解析タグを持つファイルは、通常のファイルとしてレプリケートされます。 ただし、再解析タグと再解析データバッファーは、ローカルシステムでのみ機能するため、他のサーバーにはレプリケートされません。 
<br>

  - 圧縮\_さ\_れたファイル属性  
      
  - 暗号化\_さ\_れたファイル属性  
      

> [!NOTE]
> DFS レプリケーションでは、暗号化ファイルシステム (EFS) を使用して暗号化されたファイルはレプリケートされません。 DFS レプリケーションは、Microsoft 以外のソフトウェアを使用して暗号化されたファイルをレプリケートしますが、ファイルに FILE_ATTRIBUTE_ENCRYPTED 属性値が設定されていない場合に限ります。 
<br>

  - ファイル\_属性\_スパースファイル\_  
      
  - ファイル\_属性\_ディレクトリ  
      

DFS レプリケーションでは、ファイル\_属性\_の一時的な値はレプリケートされません。

### <a name="can-i-control-which-member-is-replicated"></a>どのメンバーをレプリケートするかを制御できますか。

可能。 レプリケーショングループを作成するときに、トポロジを選択できます。 または、 **[トポロジなし]** を選択し、レプリケーショングループの作成後に手動で接続を構成することもできます。

### <a name="can-i-seed-a-replication-group-member-with-data-prior-to-the-initial-replication"></a>初期レプリケーションの前に、データを使用してレプリケーショングループメンバーをシードすることはできますか。

可能。 DFS レプリケーションは、初期レプリケーションの前に、レプリケーショングループメンバーへのファイルのコピーをサポートしています。 この "事前設定" により、初期レプリケーション中にレプリケートされるデータの量を大幅に削減できます。

ファイルが実際の属性またはタイムスタンプのみで異なる場合、初期レプリケーションでコンテンツをレプリケートする必要はありません。 実際の属性は、Win32 関数`SetFileAttributes`によって設定できる属性です。 詳細については、MSDN ライブラリの「 [Setfileattributes 関数](http://go.microsoft.com/fwlink/?linkid=182269)」 (http://go.microsoft.com/fwlink/?LinkId=182269) を参照してください。 2つのファイルが、圧縮などの他の属性によって異なる場合は、ファイルの内容がレプリケートされます。

レプリケーショングループメンバーを事前設定するには、移行先サーバーの適切なフォルダーにファイルをコピーし、レプリケーショングループを作成してから、プライマリメンバーを選択します。 プライマリメンバーのコンテンツは "権限がある" と見なされるため、レプリケートする最新のファイルを持つメンバーを選択します。 これは、初期レプリケーション時に、レプリケーショングループの他のメンバーのファイルの他のバージョンが、プライマリメンバーのファイルによって常に上書きされることを意味します。

DFSR データベースのプリシードと複製の詳細については[、「Windows Server 2012 R2 での初期同期の DFS レプリケーション」を参照してください。複製](http://blogs.technet.com/b/filecab/archive/2013/08/21/dfs-replication-initial-sync-in-windows-server-2012-r2-attack-of-the-clones.aspx)の攻撃。

初期レプリケーションの詳細については、「[レプリケーショングループの作成](https://technet.microsoft.com/library/cc725893)」を参照してください。

### <a name="does-dfs-replication-overcome-common-file-replication-service-issues"></a>ファイルレプリケーションサービスの一般的な問題を解決 DFS レプリケーション

可能。 DFS レプリケーションは、次の3つの一般的な FRS の問題を解決します。

  - ジャーナルのラップ:DFS レプリケーションは、ジャーナルを即座にラップから回復します。 レプリケーションを再度有効にする前に、既存の各ファイルまたはフォルダーは journalWrap としてマークされ、ファイルシステムに対して検証されます。 回復中、このボリュームは、どちらの方向でもレプリケーションに使用できません。  
      
  - 過剰なレプリケーション:過剰なレプリケーションを防ぐために、DFS レプリケーションではクレジットシステムを使用します。  
      
  - モーフィングパスフォルダー:フォルダー名のモーフィングパスを防ぐため、DFS レプリケーションは、競合するデータ\\を隠し DfsrPrivate conflictanddeleted および preexisting フォルダー (レプリケートフォルダーのローカルパスの下にあります) に格納します。 たとえば、FRS を使用してレプリケートされた複数のサーバーで同じ名前を持つ複数のフォルダーを同時に作成すると、FRS によって古いフォルダーの名前が変更されます。 代わりに、DFS レプリケーションは、古いフォルダーをローカルの競合して削除されたフォルダーに移動します。  
      

### <a name="does-dfs-replication-replicate-files-in-chronological-order"></a>ファイルは時系列の順序でレプリケート DFS レプリケーションますか?

No. ファイルは、順不同でレプリケートされる可能性があります。

### <a name="does-dfs-replication-replicate-files-that-are-being-used-by-another-application"></a>別のアプリケーションによって使用されているファイルをレプリケート DFS レプリケーションますか?

アプリケーションがファイルを開いてファイルロックを作成した場合 (開いている他のアプリケーションがそのファイルを使用できないようにする場合)、DFS レプリケーションは、ファイルが閉じられるまでファイルをレプリケートしません。 アプリケーションが読み取り共有アクセスでファイルを開いた場合でも、ファイルをレプリケートできます。

### <a name="does-dfs-replication-replicate-ntfs-file-permissions-alternate-data-streams-hard-links-and-reparse-points"></a>NTFS ファイルのアクセス許可、代替データストリーム、ハードリンク、および再解析ポイントをレプリケート DFS レプリケーションますか。

  - DFS レプリケーションは、NTFS ファイルのアクセス許可と代替データストリームをレプリケートします。  
      
  - Microsoft では、レプリケートフォルダー内のファイルとの間での NTFS ハードリンクの作成をサポートしていません。そのため、影響を受けるファイルのレプリケーションの問題が発生する可能性があります。 ハードリンクファイルは DFS レプリケーションによって無視され、レプリケートされません。 また、接合ポイントもレプリケートされず、DFS レプリケーション発生した各分岐点に対してイベント4406をログに記録します。  
      
  - DFS レプリケーションによってレプリケートされる再解析ポイントは、IO\_再\_解析\_タグのシンボリックリンクタグを使用するものだけです。ただし、DFS レプリケーションでは、シンボリックリンクのターゲットもレプリケートされることは保証されません。 詳細については、「 [Ask The Directory Services Team ブログ](http://blogs.technet.com/b/askds/archive/2011/09/30/friday-mail-sack-super-slo-mo-edition.aspx)」を参照してください。  
      
  - \_Io\_再解析\_\_\_タグ重複除去、io\_再解析タグ SIS、または io 再\_解析タグを持つファイルがレプリケートされます。\_\_通常のファイルとして。 再解析ポイントはローカルシステムでのみ機能するため、再解析タグと再解析データバッファーは他のサーバーにレプリケートされません。 そのため、DFS レプリケーションは、Windows Server 2012 または単一インスタンス記憶域 (SIS) でデータ重複除去を使用するボリューム上のフォルダーをレプリケートできますが、データ重複除去情報は、役割サービスが有効になっている各サーバーによって個別に保持されます。  
      

### <a name="does-dfs-replication-replicate-timestamp-changes-if-no-other-changes-are-made-to-the-file"></a>ファイルに他の変更が加えられない場合、DFS レプリケーションはタイムスタンプの変更をレプリケートしますか?

いいえ、DFS レプリケーションによって、変更がタイムスタンプに変更されるファイルはレプリケートされません。 また、変更されたタイムスタンプは、ファイルに他の変更が加えられていない限り、レプリケーショングループの他のメンバーにはレプリケートされません。

### <a name="does-dfs-replication-replicate-updated-permissions-on-a-file-or-folder"></a>ファイルまたはフォルダーに対して更新されたアクセス許可をレプリケート DFS レプリケーションますか?

可能。 DFS レプリケーションは、ファイルとフォルダーのアクセス許可の変更をレプリケートします。 Access Control リスト (ACL) に関連付けられているファイルの部分のみがレプリケートされますが、DFS レプリケーションでも、ファイル全体をステージング領域に読み取る必要があります。


> [!NOTE]
> 多数のファイルで Acl を変更すると、レプリケーションのパフォーマンスに影響を与える可能性があります。 ただし、RDC を使用する場合、転送されるデータの量は、ファイル全体のサイズではなく、Acl のサイズに比例します。 ファイルがステージングフォルダーとの間で読み取られる必要があるため、ファイルのサイズに比例してディスクトラフィックの量が増加しています。 
<br>


### <a name="does-dfs-replication-support-merging-text-files-in-the-event-of-a-conflict"></a>競合が発生した場合、テキストファイルのマージはサポート DFS レプリケーション。

競合がある場合、DFS レプリケーションはファイルをマージしません。 ただし、競合が検出されたコンピューターの隠し DfsrPrivate\\conflictanddeleted および preexisting フォルダーに、古いバージョンのファイルを保存しようとします。

### <a name="does-dfs-replication-use-encryption-when-transmitting-data"></a>データの送信時に暗号化を使用 DFS レプリケーションますか。

可能。 DFS レプリケーションでは、暗号化を使用してリモートプロシージャコール (RPC) 接続を使用します。

### <a name="is-it-possible-to-disable-the-use-of-encrypted-rpc"></a>暗号化された RPC の使用を無効にすることはできますか。

No. DFS レプリケーションサービスは、TCP 経由のリモートプロシージャコール (RPC) を使用してデータをレプリケートします。 インターネット経由でのデータ転送をセキュリティで保護するために、DFS レプリケーションサービスは常に認証レベルの`RPC_C_AUTHN_LEVEL_PKT_PRIVACY`定数を使用するように設計されています。 これにより、インターネットを介した RPC 通信が常に暗号化されます。 そのため、DFS レプリケーションサービスによる暗号化 RPC の使用を無効にすることはできません。

詳細については、次の Microsoft Web サイトを参照してください。

  - [RPC テクニカルリファレンス](http://go.microsoft.com/fwlink/?linkid=182278)  
      
  - [Remote Differential Compression について](http://go.microsoft.com/fwlink/?linkid=182279)  
      
  - [認証レベルの定数](http://go.microsoft.com/fwlink/?linkid=182280)  
      

### <a name="how-are-simultaneous-replications-handled"></a>同時レプリケーションはどのように処理されますか?

レプリケートフォルダーごとに更新マネージャーが1つあります。 更新マネージャーは、相互に独立して動作します。

既定では、最大 16 (Windows Server 2003 R2 では4個) の同時ダウンロードが、すべての接続とレプリケーショングループで共有されます。 接続とレプリケーショングループの更新はシリアル化されないため、更新プログラムを受信する順序は特にありません。 2つのスケジュールが開かれている場合、通常、更新プログラムは両方の接続から同時に受信およびインストールされます。

### <a name="how-do-i-force-replication-or-polling"></a>レプリケーションまたはポーリングを強制操作方法ますか?

「[レプリケーションスケジュールの編集](https://technet.microsoft.com/library/Cc732278)」で説明されているように、DFS 管理を使用して直ちにレプリケーションを強制することができます。 Windows Server 2012 R2 または`Sync-DfsReplicationGroup` **dfsrdiag.exe syncnow**コマンドで導入された DFSR PowerShell モジュールに含まれるコマンドレットを使用して、レプリケーションを強制することもできます。 `Update-DfsrConfigurationFromAD`コマンドレットまたは**dfsrdiag.exe pollad**コマンドを使用して、強制的にポーリングできます。

### <a name="is-it-possible-to-configure-a-quiet-time-between-replications-for-files-that-change-frequently"></a>頻繁に変更されるファイルのレプリケーションの間隔を短くすることはできますか。

No. スケジュールが開いている場合は、DFS レプリケーションによって通知された変更がレプリケートされます。 ファイルの時間を短縮することはできません。

### <a name="is-it-possible-to-configure-one-way-replication-with-dfs-replication"></a>DFS レプリケーションで一方向のレプリケーションを構成することはできますか。

可能。 Windows Server 2012 または Windows Server 2008 R2 を使用している場合は、一方向の接続を介してコンテンツをレプリケートする読み取り専用のレプリケートフォルダーを作成できます。 詳細については、「[特定のメンバーでレプリケートフォルダーを読み取り専用にする](http://go.microsoft.com/fwlink/?linkid=156740)(http://go.microsoft.com/fwlink/?LinkId=156740) 」を参照してください。

Windows Server 2008 または Windows Server 2003 R2 で DFS レプリケーションを使用した一方向のレプリケーション接続の作成はサポートされていません。 これにより、正常性チェックのトポロジエラー、ステージングの問題、および DFS レプリケーションデータベースに関する問題など、さまざまな問題が発生する可能性があります。

Windows Server 2008 または Windows Server 2003 R2 を使用している場合は、次の操作を実行することで一方向の接続をシミュレートできます。

  - プライマリサーバーとして指定するサーバー上でのみ変更を行うには、管理者をトレーニングします。 次に、変更を移行先サーバーにレプリケートします。  
      
  - エンドユーザーに書き込みアクセス許可がないように、移行先サーバーで共有アクセス許可を構成します。 ブランチサーバーで変更が許可されていない場合、一方向の接続をシミュレートし、WAN の使用率を低く抑えるために、レプリケートするものはありません。  
      

### <a name="is-there-a-way-to-force-a-complete-replication-of-all-files-including-unchanged-files"></a>変更されていないファイルを含むすべてのファイルの完全なレプリケーションを強制する方法はありますか。

No. DFS レプリケーションでファイルが同一であると見なされる場合、それらのファイルはレプリケートされません。 変更したファイルがレプリケートされていない場合は、そのように構成すると、DFS レプリケーションによって自動的にレプリケートされます。 構成されたスケジュールを上書きするには、WMI メソッド**ForceReplicate ()** を使用します。 ただし、これはスケジュールの上書きであるため、変更されていないファイルまたは同一のファイルのレプリケーションは強制されません。

### <a name="what-happens-if-the-primary-member-suffers-a-database-loss-during-initial-replication"></a>プライマリメンバーが初期レプリケーション中にデータベースの損失を発生させるとどうなりますか。

初期レプリケーション中、受信側メンバーのファイルのバージョンがプライマリメンバーと異なる場合は、プライマリメンバーのファイルが常に優先されます。 プライマリメンバーの指定は Active Directory Domain Services に格納され、プライマリメンバーのレプリケートの準備ができた後、レプリケーショングループのすべてのメンバーがレプリケートされる前に、指定された指定がクリアされます。

初期レプリケーションが失敗した場合、またはレプリケーション中に DFS レプリケーションサービスが再起動した場合、プライマリメンバーには、ローカル DFS レプリケーションデータベースのプライマリメンバーの指定が表示され、初期レプリケーションが再試行されます。 Active Directory Domain Services でプライマリの指定をクリアした後、プライマリメンバーの DFS レプリケーションデータベースが失われても、レプリケーショングループのすべてのメンバーが初期レプリケーションを完了する前に、レプリケーショングループのすべてのメンバーが失敗します。サーバーがプライマリメンバーとして指定されていないため、フォルダーをレプリケートします。 この問題が発生した場合は、プライマリメンバーサーバーで**dfsradmin.exe membership/set/isprimary: true**コマンドを使用して、プライマリメンバーの指定を手動で復元します。

初期レプリケーションの詳細については、「[レプリケーショングループの作成](https://technet.microsoft.com/library/cc725893)」を参照してください。


> [!WARNING]
> プライマリメンバーの指定は、初期レプリケーションプロセス中にのみ使用されます。 レプリケーションの完了後に<STRONG>dfsradmin.exe</STRONG>コマンドを使用してレプリケートされたフォルダーのプライマリメンバーを指定した場合、DFS レプリケーションでは Active Directory Domain Services のプライマリメンバーとしてサーバーが指定されません。 ただし、その後、サーバー上の DFS レプリケーションデータベースで破損またはデータの損失が発生した場合、サーバーはレプリケーションの別のメンバーからデータを回復するのではなく、プライマリメンバーとして初期レプリケーションを実行しようとします。グループ. 基本的に、サーバーは偽のプライマリサーバーになり、競合が発生する可能性があります。 このため、初期レプリケーションの不可能ほどが失敗したことが確実である場合にのみ、プライマリメンバーを手動で指定してください。 
<br>


### <a name="what-happens-if-the-replication-schedule-closes-while-a-file-is-being-replicated"></a>ファイルのレプリケート中にレプリケーションスケジュールを終了するとどうなりますか。

接続で remote differential compression (RDC) が有効になっている場合、スケジュールが開いたとき (または**帯域**外に変更された場合) に直ちにレプリケートが開始された、64 KB を超えるファイルの入力方向のレプリケーションが、スケジュールが開いたときに続行されます (または、**帯域幅なし**の変更)。 レプリケーションは、レプリケーションが停止したときの状態から続行されます。

RDC がオフになっている場合は、DFS レプリケーションによってファイル転送が完全に再起動されます。 これにより、受信側メンバーでファイルが使用可能になると遅延が発生する可能性があります。

### <a name="what-happens-when-two-users-simultaneously-update-the-same-file-on-different-servers"></a>2人のユーザーが、異なるサーバー上の同じファイルを同時に更新するとどうなりますか。

DFS レプリケーションが競合を検出すると、最後に保存されたファイルのバージョンが使用されます。 他のファイルを DfsrPrivate\\conflictanddeleted および preexisting フォルダー (競合を解決したコンピューター上のレプリケートフォルダーのローカルパスの下) に移動します。 競合し、削除されたフォルダーが構成されたサイズを超えた場合、または DFS レプリケーションがディスク領域不足のエラーを検出した場合に発生します。 競合して削除されたフォルダーはレプリケートされません。この競合解決方法により、FRS で使用可能だったモーフィングパスの問題が回避されます。

競合が発生すると、DFS レプリケーションによって、情報イベントが DFS レプリケーションイベントログに記録されます。 このイベントでは、次の理由により、ユーザーの操作は必要ありません。

  - ユーザーには表示されません (サーバー管理者のみが表示できます)。  
      
  - DFS レプリケーションは、競合して削除されたフォルダーをキャッシュとして扱います。 クォータのしきい値に達すると、それらのファイルの一部がクリーンアップされます。 競合するファイルが保存される保証はありません。  
      
  - 競合は、競合の発生元とは異なるサーバー上に存在する可能性があります。  
      

## <a name="staging"></a>ステージング

### <a name="does-dfs-replication-continue-staging-files-when-replication-is-disabled-by-a-schedule-or-bandwidth-throttling-quota-or-when-a-connection-is-manually-disabled"></a>スケジュールまたは帯域幅の調整クォータによってレプリケーションが無効になっている場合、または手動で接続が無効になっている場合に、ファイルのステージング DFS レプリケーション続行しますか?

No. DFS レプリケーションでは、スケジュールされたレプリケーション時間外のファイルのステージングは続行されません。帯域幅調整クォータを超過した場合、または接続が無効になっている場合です。

### <a name="does-dfs-replication-prevent-other-applications-from-accessing-a-file-during-staging"></a>ステージング中に他のアプリケーションがファイルにアクセスできないように DFS レプリケーションしますか。

No. DFS レプリケーションでは、ユーザーまたはアプリケーションがレプリケーションフォルダー内のファイルを開くことをブロックしない方法でファイルを開きます。 このメソッドは "便宜的ロック" と呼ばれます。

### <a name="is-it-possible-to-change-the-location-of-the-staging-folder-with-the-dfs-management-tool"></a>DFS 管理ツールを使用して、ステージングフォルダーの場所を変更することはできますか。

可能。 ステージングフォルダーの場所は、レプリケーショングループの各メンバーについて、 **[プロパティ]** ダイアログボックスの **[詳細設定]** タブで構成します。

### <a name="when-are-files-staged"></a>ファイルはどのようなときにステージングされますか。

次の表に示すように、受信側メンバーがファイルを要求したときに、ファイルが送信メンバーにステージングされます (ファイルが 64 KB 以下である場合を除きます)。 接続で RDC (Remote Differential Compression) が無効になっている場合、ファイルは 256 KB 以下でない限りステージングされます。 ファイルは、サイズが 64 KB 未満の場合に転送されるため、受信側メンバーでもステージングされます。ただし、この設定は 16 KB ~ 1 MB の範囲で構成できます。 スケジュールを終了すると、ファイルはステージングされません。

### <a name="the-minimum-file-sizes-for-staging-files"></a>ステージングファイルの最小ファイルサイズ

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th> </th>
<th>RDC 有効</th>
<th>無効な RDC</th>
</tr>
</thead>
<tbody>
<tr class="even">
<td><p>メンバーの送信</p></td>
<td><p>64 KB</p></td>
<td><p>256 KB</p></td>
</tr>
<tr class="odd">
<td><p>受信メンバー</p></td>
<td><p>64 KB (既定)</p></td>
<td><p>64 KB (既定)</p></td>
</tr>
</tbody>
</table>

### <a name="what-happens-if-a-file-is-changed-after-it-is-staged-but-before-it-is-completely-transmitted-to-the-remote-site"></a>ステージング後、リモートサイトに完全に転送される前にファイルが変更された場合はどうなりますか。

ファイルのいずれかの部分が既に転送されている場合、DFS レプリケーションは転送を続行します。 ファイルの送信が開始される前にファイルが変更された場合、ファイルの新しいバージョンが送信され DFS レプリケーション。

## <a name="change-history"></a>変更履歴


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>date</th>
<th>説明</th>
<th>Reason</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>2018 年 11 月 15 日</p></td>
<td><p>Windows Server 2019 用に更新されました。</p></td>
<td><p>新しいオペレーティングシステム。</p></td>
</tr>
<tr class="even">
<td><p>2013 年 10 月 9 日</p></td>
<td><p>DFS レプリケーションのサポートされる制限を更新しましたか?Windows Server 2012 R2 でのテストの結果を含むセクション。</p></td>
<td><p>最新バージョンの Windows Server の更新プログラム</p></td>
</tr>
<tr class="odd">
<td><p>2013年1月30日</p></td>
<td><p>スケジュールまたは帯域幅の調整クォータによってレプリケーションが無効になっている場合、または手動で接続を無効にした場合に、ステージングファイルを続行 DFS レプリケーションが追加されました。キー.</p></td>
<td><p>お客様の質問</p></td>
</tr>
<tr class="even">
<td><p>2012年10月31日</p></td>
<td><p>DFS レプリケーションのサポートされている制限を編集していますか。エントリを入力して、ボリューム上のレプリケートされたファイルの数を増やします。</p></td>
<td><p>カスタマー フィードバック</p></td>
</tr>
<tr class="odd">
<td><p>2012年8月15日</p></td>
<td><p>を編集すると、NTFS ファイルのアクセス許可、代替データストリーム、ハードリンク、および再解析ポイントがレプリケート DFS レプリケーションますか。DFS レプリケーションがハードリンクと再解析ポイントを処理する方法を明確にするためのエントリ。</p></td>
<td><p>カスタマーサポートサービスからのフィードバック</p></td>
</tr>
<tr class="even">
<td><p>2012年6月13日</p></td>
<td><p>ReFS または FAT ボリュームで動作 DFS レプリケーションが編集されたか。参照の説明を追加するエントリ。</p></td>
<td><p>カスタマー フィードバック</p></td>
</tr>
<tr class="odd">
<td><p>2012年4月25日</p></td>
<td><p>を編集すると、NTFS ファイルのアクセス許可、代替データストリーム、ハードリンク、および再解析ポイントがレプリケート DFS レプリケーションますか。DFS レプリケーションがハードリンクを処理する方法を明確にするためのエントリ。</p></td>
<td><p>潜在的な混乱を減らす</p></td>
</tr>
<tr class="even">
<td><p>2011年3月30日</p></td>
<td><p>を編集すると、Outlook の .pst または Microsoft Office Access データベースファイルをレプリケート DFS レプリケーションことができますか。DFS レプリケーションを使用して、.pst ファイルと Access ファイルを使用することによって生じる可能性のある影響を修正します。</p>
<p>レプリケーションのパフォーマンスを向上させる方法を追加しましたか?</p></td>
<td><p>前のエントリに関する質問。これにより、.pst ファイルまたは Access ファイルをレプリケートすると、DFS レプリケーションデータベースが破損する可能性があります。</p></td>
</tr>
<tr class="odd">
<td><p>2011年1月26日</p></td>
<td><p>Conflictanddeleted および preexisting または既存のフォルダーからファイルを回復する方法を追加しましたか。</p></td>
<td><p>カスタマー フィードバック</p></td>
</tr>
<tr class="even">
<td><p>2010年10月20日</p></td>
<td><p>DFS レプリケーションメンバーをアップグレードまたは置換する方法を追加しましたか?</p></td>
<td><p>カスタマー フィードバック</p></td>
</tr>
</tbody>
</table>

