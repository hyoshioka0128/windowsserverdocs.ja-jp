---
title: 'DFS レプリケーション: よく寄せられる質問 (FAQ)'
ms.date: 06/18/2014
ms.prod: windows-server
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: e92ada07140b88ef4178a5aecdb263b825380c2d
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2020
ms.locfileid: "75950283"
---
# <a name="dfs-replication-frequently-asked-questions-faq"></a>DFS レプリケーション: よく寄せられる質問 (FAQ)


更新:2019 年 4 月 30 日

適用先:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

この FAQ では、Windows Server の分散ファイル システム (DFS) レプリケーション (DFS-R または DFSR とも呼ばれます) に関する質問に回答します。

DFS 名前空間については、「[DFS 名前空間: よく寄せられる質問](https://technet.microsoft.com/library/ee404780)」をご覧ください。

DFS レプリケーションの新機能については、次のトピックをご覧ください。

  - [DFS 名前空間と DFS レプリケーションの概要](https://technet.microsoft.com/library/jj127250) (Windows Server 2012)  
      
  - 「[Windows Server 2008 から Windows Server 2008 R2 への機能の変更点](https://technet.microsoft.com/library/dd391932)」の「[分散ファイル システムの新機能](https://technet.microsoft.com/library/ee307957)」トピック  
      
  - 「[Windows Server 2003 SP1 から Windows Server 2008 への機能の変更点](https://technet.microsoft.com/library/cc753208)」の「[分散ファイル システム](https://technet.microsoft.com/library/cc753479)」トピック  
      

このトピックに対する最近の変更については、「 [変更履歴](#change-history) 」を参照してください。

      

## <a name="interoperability"></a>相互運用性

### <a name="can-dfs-replication-communicate-with-frs"></a>DFS レプリケーションは FRS と通信できますか?

いいえ。 DFS レプリケーションは、ファイル レプリケーション サービス (FRS) と通信しません。 DFS レプリケーションと FRS は同じサーバー上で同時に実行できますが、それらが同じフォルダーやサブフォルダーをレプリケートするように構成してはなりません。そのように構成すると、データが失われる可能性があります。

### <a name="can-dfs-replication-replace-frs-for-sysvol-replication"></a>SYSVOL 用の FRS レプリケーションの代わりに DFS レプリケーションを使用できますか?

はい。Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、または Windows Server 2008 が実行されているサーバーでは、SYSVOL 用の FRS レプリケーションの代わりに DFS レプリケーションを使用できます。 Windows Server 2003 R2 が実行されているサーバーでは、SYSVOL フォルダーをレプリケートするために DFS レプリケーションを使用することはできません。

DFS レプリケーションを使用した SYSVOL のレプリケートについて詳しくは、「[SYSVOL レプリケーション移行ガイド: FRS から DFS レプリケーション](https://technet.microsoft.com/library/dd640019)」をご覧ください。

### <a name="can-i-upgrade-from-frs-to-dfs-replication-without-losing-configuration-settings"></a>構成設定を失わずに、FRS から DFS レプリケーションにアップグレードできますか?

はい。 レプリケーションを FRS から DFS レプリケーションに移行するには、次のドキュメントを参照してください。

  - SYSVOL フォルダー以外のフォルダーのレプリケーションを移行するには、「[DFS 操作ガイド: FRS から DFS レプリケーションへの移行](https://go.microsoft.com/fwlink/?linkid=192776)」および [FRS2DFSR – FRS から DFSR への移行ユーティリティ](https://go.microsoft.com/fwlink/?linkid=195437) (https://go.microsoft.com/fwlink/?LinkID=195437) を参照してください。  
      
  - SYSVOL フォルダーのレプリケーションを DFS レプリケーションに移行する方法については、「[SYSVOL レプリケーション移行ガイド: FRS から DFS レプリケーション](https://technet.microsoft.com/library/dd640019)」をご覧ください。  
      

### <a name="can-i-use-dfs-replication-in-a-mixed-windowsunix-environment"></a>Windows と UNIX が混在する環境で DFS レプリケーションを使用できますか?

はい。 DFS レプリケーションでサポートされているのは、Windows Server が実行されているサーバー間での内容のレプリケートだけですが、UNIX クライアントは Windows Server 上のファイル共有にアクセスできます。 そのためには、ネットワーク ファイル システム (NFS) 用のサービスを DFS レプリケーション サーバーにインストールします。

また、多くの UNIX クライアントに含まれる SMB/CIFS クライアント機能を使用して、Windows ファイル共有に直接アクセスすることもできます。ただし、この機能は、制限がある場合や、Windows 環境への変更が必要な場合がよくあります (グループ ポリシーを使用した SMB 署名の無効化など)。

DFS レプリケーションは、Windows Server オペレーティングシステムが実行されているサーバー上の NFS と相互運用できますが、NFS マウント ポイントをレプリケートすることはできません。

### <a name="can-i-use-the-volume-shadow-copy-service-with-dfs-replication"></a>DFS レプリケーションでボリューム シャドウ コピー サービスを使用できますか?

はい。 DFS レプリケーションはボリューム シャドウ コピー サービス (VSS) ボリュームでサポートされており、以前のスナップショットを以前のバージョンのクライアントで正常に復元できます。

### <a name="can-i-use-windowsbackup-ntbackupexe-to-remotely-back-up-a-replicated-folder"></a>Windows バックアップ (Ntbackup.exe) を使用して、レプリケート フォルダーをリモート環境からバックアップできますか?

いいえ。Windows Server 2003 以前が実行されているコンピューター上の Windows バックアップ (Ntbackup.exe) を使用して、Windows Server 2012、Windows Server 2008 R2、または Windows Server 2008 が実行されているコンピューター上のレプリケート フォルダーの内容を、バックアップすることはできません。

レプリケート フォルダーに格納されているファイルをバックアップするには、Windows Server バックアップまたは Microsoft® System Center Data Protection Manager を使用します。 Windows Server 2008 R2 および Windows Server 2008 のバックアップと回復の機能の詳細については、「[バックアップと回復](https://technet.microsoft.com/library/Cc754097)」を参照してください。 詳細については、「[System Center Data Protection Manager](https://go.microsoft.com/fwlink/?linkid=182261)」 (https://go.microsoft.com/fwlink/?LinkId=182261) を参照してください。

### <a name="do-file-system-policies-impact-dfs-replication"></a>ファイル システム ポリシーは DFS レプリケーションに影響しますか?

はい。 レプリケート フォルダーには、ファイル システム ポリシーを構成しないでください。 ファイル システム ポリシーでは、すべてのグループ ポリシー更新間隔で NTFS のアクセス許可が再適用されます。 これにより、開かれているファイルは閉じられるまでレプリケートされないため、共有違反が発生する可能性があります。

### <a name="does-dfs-replication-replicate-mailboxes-hosted-on-microsoft-exchange-server"></a>DFS レプリケーションでは、Microsoft Exchange Server でホストされているメールボックスはレプリケートされますか?

いいえ。 DFS レプリケーションを使用して、Microsoft Exchange Server でホストされているメールボックスをレプリケートすることはできません。

### <a name="does-dfs-replication-support-file-screens-created-by-file-server-resource-manager"></a>DFS レプリケーションでは、ファイル サーバー リソース マネージャーによって作成されたファイル スクリーンはサポートされますか?

はい。 ただし、ファイル サーバー リソース マネージャー (FSRM) でのファイル スクリーンの設定が、レプリケーションの両側で一致している必要があります。 さらに、DFS レプリケーションには、レプリケーションから特定のファイルとファイルの種類を除外するために使用できる、ファイルとフォルダー用の独自のフィルター メカニズムがあります。

ファイル スクリーンまたはクォータを実装するためのベスト プラクティスを次に示します。

  - 非表示の DfsrPrivate フォルダーを、クォータまたはファイル スクリーンの対象にすることはできません。  
      
  - スクリーニングを有効にする前に、スクリーニングされるファイルがレプリケート フォルダーに存在していてはなりません。  
      
  - クォータを有効にする前に、どのフォルダーもクォータを超えていてはなりません。  
      
  - ハード クォータは慎重に使用する必要があります。 レプリケーション グループの個々のメンバーは、レプリケーションの前にはクォータの範囲内であっても、ファイルがレプリケートされるとそれを超える可能性があります。 たとえば、あるユーザーが 10 メガバイト (MB) のファイルをサーバー A にコピーし (ハード制限に達します)、別のユーザーがサーバー B に 5 MB のファイルをコピーした場合、次のレプリケーションが発生すると、どちらのサーバーもクォータを 5 MB だけ超えます。 これにより、DFS レプリケーションではファイルのレプリケーションの再試行が続けられ、バージョン ベクターにホールが発生して、パフォーマンスの問題が発生する可能性があります。  
      

### <a name="is-dfs-replication-cluster-aware"></a>DFS レプリケーションはクラスターに対応していますか?

はい。Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2 の DFS レプリケーションには、レプリケーション グループのメンバーとしてフェールオーバー クラスターを追加する機能が含まれています。 詳細については、「[レプリケーション グループにフェールオーバー クラスターを追加する](https://go.microsoft.com/fwlink/?linkid=155085)」 (https://go.microsoft.com/fwlink/?LinkId=155085) ) を参照してください。 Windows Server 2008 R2 より前のバージョンの Windows の DFS レプリケーション サービスは、フェールオーバー クラスターと連携するように設計されていないため、サービスは別のノードにフェールオーバーされません。


> [!NOTE]
> DFS レプリケーションでは、クラスターの共有ボリューム上のファイルのレプリケーションはサポートされていません。 
<br>


### <a name="is-dfs-replication-compatible-with-data-deduplication"></a>DFS レプリケーションはデータ重複除去と互換性がありますか?

はい。DFS レプリケーションでは、Windows Server のデータ重複除去を使用するボリューム上のフォルダーをレプリケートできます。

### <a name="is-dfs-replication-compatible-with-ris-and-wds"></a>DFS レプリケーションは RIS および WDS と互換性がありますか?

はい。 DFS レプリケーションでは、単一インスタンス記憶域 (SIS) が有効になっているボリュームをレプリケートします。 SIS は、リモート インストール サービス (RIS)、Windows 展開サービス (WDS)、Windows Storage Server によって使用されます。

### <a name="is-it-possible-to-use-dfs-replication-with-offline-files"></a>オフライン ファイルで DFS レプリケーションを使用できますか?

ファイルに書き込むユーザーが一度に 1 人だけの場合は、DFS レプリケーションとオフライン ファイルを安全に併用できます。 これは、ユーザーが 2 つのブランチ オフィス間を移動し、両方のブランチまたはオフライン中にファイルにアクセスしたい場合に役立ちます。 オフライン ファイルによりオフラインで使用できるようにファイルがローカル環境にキャッシュされ、DFS レプリケーションにより各ブランチ オフィス間でデータがレプリケートされます。

DFS レプリケーションには分散ロック メカニズムまたはファイル チェックアウト機能がないため、マルチユーザー環境では、オフライン ファイルと DFS レプリケーションを併用しないでください。 2 人のユーザーが異なるサーバーで同じファイルを同時に変更した場合、DFS レプリケーションにより、次のレプリケーション時に、古いファイルが DfsrPrivate\\ConflictandDeleted フォルダー (レプリケート フォルダーのローカル パスの下にあります) に移動されます。

### <a name="what-antivirus-applications-are-compatible-with-dfs-replication"></a>DFS レプリケーションと互換性のあるウイルス対策アプリケーションは何ですか?

ウイルス対策アプリケーションのスキャン アクティビティによりレプリケート フォルダー内のファイルが変更された場合、過剰なレプリケーションが発生する可能性があります。 詳しくは、[ウイルス対策アプリケーションの DFS レプリケーションとの相互運用性テスト](https://go.microsoft.com/fwlink/?linkid=73990) (https://go.microsoft.com/fwlink/?LinkId=73990) に関する記事をご覧ください。

### <a name="what-are-the-benefits-of-using-dfs-replication-instead-of-windows-sharepoint-services"></a>Windows SharePoint Services ではなく DFS レプリケーションを使用する利点は何ですか?

Windows® SharePoint® Services では、ファイル チェックアウト機能の形式で厳密な一貫性が提供されますが、DFS レプリケーションにはこの機能はありません。 複数のユーザーが同じファイルを編集することが考えられる場合は、Windows SharePoint Services を使用することをお勧めします。 Windows SharePoint Services 2.0 Service Pack 2 は、Windows Server 2003 R2 の一部として利用できます。 Windows SharePoint Services は、Microsoft Web サイトからダウンロードできます。新しいバージョンの Windows Server には含まれていません。 一方、複数のサイト間でデータをレプリケートしていて、ユーザーが同時に同じファイルを編集しない場合、DFS レプリケーションでは帯域幅が大きく、管理が簡単になります。

## <a name="limitations-and-requirements"></a>制限事項と要件

### <a name="can-dfs-replication-replicate-between-branch-offices-without-a-vpn-connection"></a>DFS レプリケーションを使うと、VPN 接続を使用せずにブランチ オフィス間でレプリケートできますか?

はい。ブランチ オフィスが (インターネットではなく) プライベート ワイド エリア ネットワーク (WAN) リンクで接続されていることが前提となります。 ただし、外部ファイアウォールで適切なポートを開く必要があります。 DFS レプリケーションでは、RPC エンドポイント マッパー (ポート 135) と、ランダムに割り当てられた 1024 より大きいエフェメラル ポートが使用されます。 **Dfsrdiag** コマンド ライン ツールを使用すると、エフェメラル ポートの代わりに静的ポートを指定できます。 RPC エンドポイント マッパーの指定方法の詳細については、Microsoft サポート技術情報の[記事 154596](https://go.microsoft.com/fwlink/?linkid=73991) (https://go.microsoft.com/fwlink/?LinkId=73991) を参照してください。

### <a name="can-dfs-replication-replicate-files-encrypted-with-the-encrypting-file-system"></a>暗号化ファイル システムで暗号化されたファイルを DFS レプリケーションでレプリケートできますか?

いいえ。 DFS レプリケーションでは、暗号化ファイル システム (EFS) を使用して暗号化されたファイルまたはフォルダーはレプリケートされません。 以前にレプリケートされたファイルを暗号化した場合、DFS レプリケーションにより、レプリケーション グループの他のすべてのメンバーからそのファイルが削除されます。 これにより、ファイルの使用可能な唯一のコピーがサーバー上で暗号化されたバージョンであることが保証されます。

### <a name="can-dfs-replication-replicate-outlook-pst-or-microsoft-office-access-database-files"></a>Outlook の .pst ファイルまたは Microsoft Office Access のデータベース ファイルを、DFS レプリケーションでレプリケートできますか?

DFS レプリケーションで Microsoft Outlook の個人用フォルダー ファイル (.pst) と Microsoft Access のファイルを安全にレプリケートできるのは、それらがアーカイブ目的で保存されていて、Outlook や Access などのクライアントを使用してネットワーク経由でアクセスされない場合のみです (.pst ファイルまたは Access ファイルを開くには、最初にファイルをローカル ストレージ デバイスにコピーします)。 これには次のような理由があります。

  - ネットワーク接続経由で .pst ファイルを開くと、.pst ファイルのデータが破損する可能性があります。 ネットワーク経由で .pst ファイルに安全にアクセスできない理由について詳しくは、Microsoft サポート技術情報の[記事 297019](https://go.microsoft.com/fwlink/?linkid=125363) (https://go.microsoft.com/fwlink/?LinkId=125363) を参照してください。  
      
  - .pst ファイルと Access ファイルは、Outlook や Office Access などのクライアントによってアクセスされている間、長時間開かれたままになる傾向があります。 これにより、ファイルが閉じられるまで、DFS レプリケーションではこれらのファイルをレプリケートできなくなります。  
      

### <a name="can-i-use-dfs-replication-in-a-workgroup"></a>ワークグループで DFS レプリケーションを使用できますか?

いいえ。 DFS レプリケーションの構成は Active Directory® Domain Services に依存しています。 それはドメイン内でのみ機能します。

### <a name="can-more-than-one-folder-be-replicated-on-a-single-server"></a>1 台のサーバー上の複数のフォルダーをレプリケートできますか?

はい。 DFS レプリケーションを使うと、サーバー間で多数のフォルダーをレプリケートできます。 各レプリケート フォルダーのルート パスが一意であり、重複していないことを確認してください。 たとえば、D:\\Sales と D:\\Accounting は 2 つのレプリケート対象フォルダーのルート パスにできますが、D:\\Sales と D:\\Sales\\Reports を 2 つのレプリケート フォルダーのルート パスにすることはできません。

### <a name="does-dfs-replication-require-dfs-namespaces"></a>DFS レプリケーションに DFS 名前空間は必要ですか?

いいえ。 DFS レプリケーションと DFS 名前空間は、別々に使うことも一緒に使うこともできます。 また、DFS レプリケーションを使うと、FRS ではできなかったスタンドアロン DFS 名前空間のレプリケーションが可能です。

### <a name="does-dfs-replication-require-time-synchronization-between-servers"></a>DFS レプリケーションを使うには、サーバー間で時刻を同期する必要がありますか?

いいえ。 DFS レプリケーションを使うのに、サーバー間で時刻を明示的に同期する必要はありません。 ただし、DFS レプリケーションでは、サーバーの時計がよく一致している必要があります。 Kerberos 認証が正常に機能するためには、サーバー クロックが相互に (既定では) 5 分以内に設定されている必要があります。 たとえば、DFS レプリケーションでは、競合が発生した場合、タイムスタンプを使用して優先されるファイルが判断されます。 また、ガベージ コレクション、スケジュール、その他の機能でも、正確な時刻が重要になります。

### <a name="does-dfs-replication-support-replicating-an-entire-volume"></a>DFS レプリケーションではボリューム全体のレプリケーションがサポートされますか?

はい。 ただし、最初に Windows Server 2003 Service Pack 2 または修正プログラムをインストールする必要があります。 詳しくは、Microsoft サポート技術情報の[記事 920335](https://go.microsoft.com/fwlink/?linkid=76776) (https://go.microsoft.com/fwlink/?LinkId=76776) を参照してください。 また、ボリューム全体をレプリケートすると、次の問題が発生する可能性があります。

  - ボリュームに Windows のページング ファイルが含まれている場合、レプリケーションは失敗し、システム イベント ログに DFSR イベント 4312 が記録されます。  
      
  - DFS レプリケーションでは、レプリケート先サーバー上のレプリケート フォルダーにシステム属性と隠し属性が設定されます。 このようになるのは、Windows ではボリューム ルート フォルダーにシステム属性と隠し属性が既定で適用されるためです。 レプリケート先サーバー上のレプリケート フォルダーのローカル パスもボリューム ルートである場合は、フォルダー属性に対してそれ以上の変更は行われません。  
      
  - Windows システム フォルダーが含まれるボリュームをレプリケートする場合、DFS レプリケーションにより %WINDIR% フォルダーが認識されて、それはレプリケートされません。 ただし、Microsoft 以外のアプリケーションで使用されているフォルダーは DFS レプリケーションによってレプリケートされるため、アプリケーションと DFS レプリケーションの間に相互運用性の問題がある場合は、レプリケート先サーバーでアプリケーションがエラーになる可能性があります。  
      

### <a name="does-dfs-replication-support-rpc-over-http"></a>DFS レプリケーションでは RPC over HTTP はサポートされますか?

いいえ。

### <a name="does-dfs-replication-work-across-wireless-networks"></a>DFS レプリケーションはワイヤレス ネットワークで動作しますか?

はい。 DFS レプリケーションは、接続の種類に依存しません。

### <a name="does-dfs-replication-work-on-refs-or-fat-volumes"></a>DFS レプリケーションは ReFS ボリュームまたは FAT ボリュームで動作しますか?

いいえ。 DFS レプリケーションでは、NTFS ファイル システムでフォーマットされたボリュームのみがサポートされます。つまり、Resilient File System (ReFS) および FAT ファイル システムはサポートされていません。 DFS レプリケーションでは、NTFS 変更ジャーナルや NTFS ファイル システムの他の機能が使用されるため、NTFS が必要です。

### <a name="does-dfs-replication-work-with-sparse-files"></a>DFS レプリケーションはスパース ファイルで動作しますか?

はい。 スパース ファイルをレプリケートできます。 受信側メンバーでは、**スパース**属性が保持されます。

### <a name="do-i-need-to-log-in-as-administrator-to-replicate-files"></a>ファイルをレプリケートするには、管理者としてログインする必要がありますか?

いいえ。 DFS レプリケーションは、ローカル システム アカウントで実行されるサービスなので、レプリケートするために管理者としてログインする必要はありません。 ただし、DFS レプリケーションの構成を変更するには、影響を受けるファイル サーバーのドメイン管理者またはローカル管理者である必要があります。

詳しくは、「[DFS レプリケーションを管理する機能を委任する](https://go.microsoft.com/fwlink/?linkid=182294)」 (https://go.microsoft.com/fwlink/?LinkId=182294) で "DFS レプリケーションのセキュリティ要件と委任" に関する説明をご覧ください。

### <a name="how-can-i-upgrade-or-replace-a-dfs-replication-member"></a>DFS レプリケーション メンバーをアップグレードまたは置換するにはどうすればよいですか?

DFS レプリケーション メンバーをアップグレードまたは置換するには、ディレクトリ サービス チームに対する質問での次のブログ投稿をご覧ください: [DFSR メンバーのハードウェアまたは OS を置き換える](https://blogs.technet.com/b/askds/archive/2010/09/10/series-wrap-up-and-downloads-replacing-dfsr-member-hardware-or-os.aspx)。

### <a name="is-dfs-replication-suitable-for-replicating-roaming-profiles"></a>DFS レプリケーションは移動プロファイルのレプリケーションに適していますか?

はい。 移動ユーザー プロファイルをレプリケートするときは、特定のシナリオがサポートされます。 サポートされるシナリオについては、[レプリケートされるユーザー プロファイル データに関する Microsoft のサポートに関する声明](https://go.microsoft.com/fwlink/?linkid=201282) (https://go.microsoft.com/fwlink/?LinkId=201282) に関するページをご覧ください。

### <a name="is-there-a-file-character-limit-or-limit-to-the-folder-depth"></a>ファイルの文字またはフォルダーの深さに制限はありますか?

Windows と DFS レプリケーションでは、最大 32,000 文字のフォルダー パスがサポートされます。 DFS レプリケーションには、260 文字のフォルダー パス制限はありません。

### <a name="must-members-of-a-replication-group-reside-in-the-same-domain"></a>レプリケーション グループのメンバーは同じドメインに存在する必要がありますか?

いいえ。 レプリケーション グループは、1 つのフォレスト内の複数のドメインにまたがることはできますが、異なるフォレストにまたがることはできません。

### <a name="what-are-the-supported-limits-of-dfs-replication"></a>DFS レプリケーションにはどのような制限がありますか?

次の一覧では、Microsoft によってテストされていて、Windows Server 2012 R2、Windows Server 2016、Windows Server 2019 に適用される、一連のスケーラビリティ ガイドラインを示します

  - サーバーでレプリケートされるすべてのファイルのサイズ: 100 テラバイト。  
      
  - ボリュームでレプリケートされるファイルの数: 7,000 万。  
      
  - ファイルの最大サイズ: 250 ギガバイト。  
      


> [!IMPORTANT]
> 多数のファイルまたは大きいファイルが含まれるレプリケーション グループを作成するときは、データベースの複製をエクスポートし、事前シード手法を使って、初期レプリケーションの期間を最小限に抑えることをお勧めします。 詳しくは、「[Windows Server 2012 R2 での DFS レプリケーションの初期同期: 複製の攻撃](https://techcommunity.microsoft.com/t5/Storage-at-Microsoft/DFS-Replication-Initial-Sync-in-Windows-Server-2012-R2-Attack-of/ba-p/424877)」をご覧ください。 
<br>


次の一覧では、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008 で Microsoft によってテストされた一連のスケーラビリティ ガイドラインを示します。

  - サーバーでレプリケートされるすべてのファイルのサイズ: 10 テラバイト。  
      
  - ボリュームでレプリケートされるファイルの数: 1,100 万。  
      
  - ファイルの最大サイズ: 64 ギガバイト。  
      


> [!NOTE]
> レプリケーション グループ、レプリケート フォルダー、接続、またはレプリケーション グループのメンバーの数に対する制限はなくなりました。 
<br>


Windows Server 2003 R2 に関して Microsoft によってテストされたスケーラビリティ ガイドラインの一覧については、「[DFS レプリケーションのスケーラビリティ ガイドライン](https://go.microsoft.com/fwlink/?linkid=75043)」 (https://go.microsoft.com/fwlink/?LinkId=75043) をご覧ください。

### <a name="when-should-i-not-use-dfs-replication"></a>DFS レプリケーションを使用してはならないのはどのような場合ですか?

複数のユーザーが異なるサーバー上の同じファイルを同時に更新または変更する場合は、DFS レプリケーションを使用しないでください。 それを行うと、DFS レプリケーションにより、ファイルの競合するコピーが隠し属性の DfsrPrivate\\ConflictandDeleted フォルダーに移動される可能性があります。

複数のユーザーが異なるサーバー上の同じファイルを同時に変更する必要がある場合は、Windows SharePoint Services のファイル チェックアウト機能を使用して、1 人のユーザーだけがファイルを作業できるようにしてください。 Windows SharePoint Services 2.0 Service Pack 2 は、Windows Server 2003 R2 の一部として利用できます。 Windows SharePoint Services は、Microsoft Web サイトからダウンロードできます。新しいバージョンの Windows Server には含まれていません。

### <a name="why-is-a-schema-update-required-for-dfs-replication"></a>DFS レプリケーションにスキーマの更新が必要なのはなぜですか?

DFS レプリケーションでは、構成情報を格納するために、Active Directory Domain Services のドメイン名前付けコンテキストで新しいオブジェクトが使用されます。 Active Directory ドメイン サービス スキーマを更新すると、これらのオブジェクトが作成されます。 詳しくは、「[DFS レプリケーションの要件を確認する](https://go.microsoft.com/fwlink/?linkid=182264)」 (https://go.microsoft.com/fwlink/?LinkId=182264) をご覧ください。

## <a name="monitoring-and-management-tools"></a>監視ツールと管理ツール

### <a name="can-i-automate-the-health-report-to-receive-warnings"></a>正常性レポートを自動化して警告を受け取ることはできますか?

はい。 正常性レポートを自動化するには、次の 3 つの方法があります。

  - Windows Server 2012 R2 または DfsrAdmin.exe に含まれる DFSR Windows PowerShell モジュールをスケジュールされたタスクと共に使用して、正常性レポートを定期的に生成します。 詳しくは、[DFS レプリケーションの正常性レポートの自動化](https://go.microsoft.com/fwlink/?linkid=74010) (https://go.microsoft.com/fwlink/?LinkId=74010) に関するページをご覧ください。  
      
  - System Center Operations Manager 用の DFS レプリケーション管理パックを使用し、指定した条件に基づいてアラートを作成します。  
      
  - DFS レプリケーション WMI プロバイダーを使用して、アラートをスクリプト化します。  
      

### <a name="can-i-use-microsoft-system-center-operations-manager-to-monitor-dfs-replication"></a>Microsoft System Center Operations Manager を使用して DFS レプリケーションを監視できますか?

はい。 詳しくは、Microsoft ダウンロード センターの「[System Center Operations Manager 2007 用の DFS レプリケーション管理パック](https://go.microsoft.com/fwlink/?linkid=182265)」 (https://go.microsoft.com/fwlink/?LinkId=182265) をご覧ください。

### <a name="does-dfs-replication-support-remote-management"></a>DFS レプリケーションではリモート管理はサポートされていますか?

はい。 DFS レプリケーションでは、DFS 管理コンソールと **[レプリケーション グループの追加]** コマンドを使用してリモート管理がサポートされています。 たとえば、フォレストでサーバー A と B をメンバーとして定義されているレプリケーション グループに、サーバー A で接続できます。

DFS 管理は、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008、Windows Server 2003 R2 に含まれます。 他のバージョンの Windows から DFS レプリケーションを管理するには、リモート デスクトップまたは [Windows 7 用のリモート サーバー管理ツール](https://technet.microsoft.com/library/Ee449475)を使用します。


> [!IMPORTANT]
> フェールオーバー クラスターである読み取り専用のレプリケート フォルダーまたはメンバーが含まれるレプリケーション グループを表示または管理するには、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、<a href="https://go.microsoft.com/fwlink/p/?linkid=238560">Windows 8 用リモート サーバー管理ツール</a>、または <a href="https://technet.microsoft.com/library/ee449475">Windows 7 用リモート サーバー管理ツール</a>に含まれるバージョンの DFS 管理を使用する必要があります。 
<br>


### <a name="do-ultrasound-and-sonar-work-with-dfs-replication"></a>DFS レプリケーションでは Ultrasound と Sonar は動作しますか?

いいえ。 DFS レプリケーションには、独自の監視ツールと診断ツールのセットがあります。 Ultrasound と Sonar では、FRS の監視のみを行うことができます。

### <a name="how-can-files-be-recovered-from-the-conflictanddeleted-or-preexisting-folders"></a>ConflictAndDeleted または PreExisting フォルダーからファイルを回復するにはどうすればよいですか?

失われたファイルを回復するには、ファイル履歴、エクスプローラーの **[以前のバージョンの復元]** コマンド、またはバックアップからのファイルの復元を使用して、ファイル システム フォルダーまたは共有フォルダーからファイルを復元します。 ConflictAndDeleted フォルダーまたは PreExisting フォルダーからファイルを直接回復するには、Windows PowerShell の `Get-DfsrPreservedFiles` および `Restore-DfsrPreservedFiles` コマンドレット (Windows Server 2012 R2 の DFSR モジュールに含まれます)、または MSDN コード ギャラリーの [RestoreDFSR](https://code.msdn.microsoft.com/restoredfsr) サンプル スクリプトを使用します。 このスクリプトはディザスター リカバリーのみを目的としたもので、現状のまま保証なしで提供されます。

### <a name="is-there-a-way-to-know-the-state-of-replication"></a>レプリケーションの状態を知る方法はありますか?

はい。 レプリケーションを監視するには、いくつかの方法があります。

  - DFS レプリケーションには、プロアクティブな監視を提供する System Center Operations Manager 用の管理パックが用意されています。  
      
  - DFS の管理には、レプリケーション バックログ、レプリケーションの効率、および特定のレプリケーション グループ内のファイルとフォルダーの数に関する、インボックスの診断レポートが用意されています。  
      
  - Windows Server 2012 R2 の DFSR Windows PowerShell モジュールには、伝達テストを開始し、伝達レポートと正常性レポートを作成するためのコマンドレットが含まれています。 詳しくは、[Windows PowerShell の分散ファイル システム レプリケーション コマンドレット](https://technet.microsoft.com/library/dn296601.aspx)に関するページをご覧ください。  
      
  - Dfsrdiag.exe は、バックログ カウントを生成したり、伝達テストをトリガーしたりできるコマンドライン ツールです。 どちらでもレプリケーションの状態が表示されます。 伝達では、すべてのノードにファイルがレプリケートされているかどうかが示されます。 バックログでは、2 台のコンピューターが同期されるまでにレプリケートする必要があるファイルの数が表示されます。バックログ カウントは、レプリケーション グループ メンバーで処理されていない更新の数です。 Windows Server 2012 R2、Windows Server 2012、または Windows Server 2008 R2 が実行されているコンピューターでは、Dfsrdiag.exe を使って、DFS レプリケーションで現在レプリケートされている更新を表示することもできます。  
      
  - スクリプトでは、WMI を使って、手動または MOM を介して、バックログ情報を収集できます。  
      

## <a name="performance"></a>[パフォーマンス]

### <a name="does-dfs-replication-support-dial-up-connections"></a>DFS レプリケーションではダイヤルアップ接続はサポートされますか?

DFS レプリケーションはダイヤルアップの速度でも動作しますが、レプリケートする変更の数が多い場合は、バックログが発生する可能性があります。 既存のファイルに小さな変更が行われた場合、Remote Differential Compression (RDC) を使用する DFS レプリケーションでは、ファイルの直接コピーよりはるかに高いパフォーマンスが提供されます。

### <a name="does-dfs-replication-perform-bandwidth-sensing"></a>DFS レプリケーションでは帯域幅の検出は実行されますか?

いいえ。 DFS レプリケーションでは帯域幅の検出は行われません。 接続ごとに限られた量の帯域幅を使用するように、DFS レプリケーションを構成することができます (帯域幅調整)。 ただし、DFS レプリケーションでは、ネットワーク インターフェイスが飽和状態になっても帯域幅の使用率がさらに減らされることはなく、DFS レプリケーションによって短時間リンクが飽和状態になる可能性があります。 DFS レプリケーションによる帯域幅調整は、RPC 呼び出しを調整することによって行われるため、完全に正確ではありません。 その結果、ネットワーク スタックの下位レベル (RPC を含む) のさまざまなバッファーが干渉し、ネットワーク トラフィックが急増する可能性があります。

### <a name="does-dfs-replication-throttle-bandwidth-per-schedule-per-server-or-per-connection"></a>DFS レプリケーションによる帯域幅の調整は、スケジュール、サーバー、または接続のどの単位で行われますか?

スケジュールを指定するときに帯域幅の調整を構成すると、そのレプリケーション グループのすべての接続による帯域幅調整に、その設定が使用されます。 帯域幅調整は、DFS 管理を使用して接続レベルの設定として設定することもできます。

### <a name="does-dfs-replication-use-active-directory-domain-services-to-calculate-site-links-and-connection-costs"></a>DFS レプリケーションでは、サイト リンクと接続コストの計算に Active Directory Domain Services が使用されますか?

いいえ。 DFS レプリケーションでは、管理者によって定義されたトポロジが使用され、これは Active Directory Domain Services サイトのコストに依存しません。

### <a name="how-can-i-improve-replication-performance"></a>レプリケーションのパフォーマンスを向上させるにはどうすればよいですか?

レプリケーションのパフォーマンスをチューニングするさまざまな方法については、[ディレクトリ サービス チームへの質問ブログ](https://blogs.technet.com/b/askds/)で、[DFSR でのレプリケーション パフォーマンスのチューニング](https://blogs.technet.com/b/askds/archive/2010/03/31/tuning-replication-performance-in-dfsr-especially-on-win2008-r2.aspx)に関するページをご覧ください。

### <a name="how-does-dfs-replication-avoid-saturating-a-connection"></a>DFS レプリケーションではどのようにすれば接続の飽和を回避できますか?

DFS レプリケーションでは、ユーザーが接続で使用する最大帯域幅を設定すると、サービスによってネットワーク使用率がそのレベルに維持されます。 これはバックグラウンド インテリジェント転送サービス (BITS) とは異なり、設定が適切であれば、DFS レプリケーションによって接続が飽和状態になることはありません。

ただし、帯域幅の調整は 100% 正確ではなく、短時間 DFS レプリケーションによってにリンクが飽和する可能性があります。 これは、DFS レプリケーションによる帯域幅の調整が RPC 呼び出しを制限することで行われるためです。 このプロセスは、RPC など、ネットワーク スタックの下位レベルのさまざまなバッファーに依存しているため、レプリケーション トラフィックが急増し、ネットワーク リンクが飽和状態になることがあります。

Windows Server 2008 の DFS レプリケーションには、いくつかのパフォーマンス強化が含まれます。「[Windows Server 2003 SP1 から Windows Server 2008 への機能の変更](https://technet.microsoft.com/library/cc753208)」で[分散ファイル システム](https://technet.microsoft.com/library/Cc753479)に関するトピックを参照してください。

### <a name="how-does-dfs-replication-performance-compare-with-frs"></a>FRS と比較して DFS レプリケーションのパフォーマンスはどうですか?

DFS レプリケーションは、FRS よりはるかに高速です。大きなファイルに対して小さな変更が行われ、RDC が有効になっている場合は特にそうです。 たとえば、RDC を使用すると、2 MB の PowerPoint® プレゼンテーションに対する小さな変更でのネットワーク経由の送信量が、60 キロバイト (KB) だけになる可能性があり、転送バイト数が 97% 削減されます。

RDC は、64 KB 未満のファイルでは使用されず、ネットワーク帯域幅が競合しない高速 LAN ではメリットがない可能性があります。 RDC は、DFS 管理を使用して、接続ごとに無効にすることができます。

### <a name="how-frequently-does-dfs-replication-replicate-data"></a>DFS レプリケーションではデータはどのくらいの頻度でレプリケートされますか?

データは、ユーザーが設定するスケジュールに従ってレプリケートされます。 たとえば、週 7 日 15 分間隔にスケジュールを設定できます。 これらの間隔の間、レプリケーションが有効になります。 ファイルの変更が検出されるとすぐにレプリケーションが開始されます (通常は数秒以内)。

レプリケーション グループのスケジュールは協定世界時 (UTC) に設定し、接続スケジュールは受信側メンバーのローカル時刻に設定することができます。 レプリケーション グループが複数のタイム ゾーンにまたがる場合は、このことを考慮してください。 ローカル時刻は、受信接続をホストしているメンバーの時刻を意味します。 スケジュールがローカル時刻に設定されている場合、受信接続および対応する送信接続の表示されるスケジュールには、タイム ゾーンの違いが反映されます。

### <a name="how-much-of-my-servers-system-resources-will-dfs-replication-consume"></a>DFS レプリケーションによって消費されるサーバーのシステム リソースはどれくらいですか?

DFS レプリケーションによって使用されるディスク、メモリ、および CPU リソースは、ファイルの数とサイズ、変更率、レプリケーション グループ メンバーの数、レプリケート フォルダーの数など、さまざまな要因によって異なります。 また、リソースによっては、推定が困難なものもあります。 たとえば、DFS レプリケーション データベースに使用される Extensible Storage Engine (ESE) テクノロジでは、使用可能なメモリの大部分が消費され、必要に応じて解放されます。 サーバーの構成によっては、DFS レプリケーション以外のアプリケーションを同じサーバー上でホストできます。 ただし、1 台のサーバーで複数のアプリケーションまたはサーバーの役割をホストする場合は、運用環境で実装する前に、この構成をテストすることが重要です。

### <a name="what-happens-if-a-wan-link-fails-during-replication"></a>レプリケーション中に WAN リンクに障害が発生した場合はどうなりますか?

接続がダウンした場合、DFS レプリケーションは、スケジュールが開いている間はレプリケートを試行し続けます。 また、DFS レプリケーション イベント ログにも接続エラーが記録され、MOM (アラートを通じて自動的に) および DFS レプリケーション正常性レポート (管理者が実行したときなど、手動で) を使用して収集できます。

## <a name="remote-differential-compression-details"></a>Remote Differential Compression の詳細

### <a name="are-changes-compressed-before-being-replicated"></a>変更はレプリケートされる前に圧縮されますか?

はい。 ファイルの変更部分は、すべての種類のファイルに対して送信される前に圧縮されます。ただし、以下のファイルは既に圧縮されているため除きます: .wma、.wmv、.zip、.jpg、.mpg、.mpeg、.m1v、.mp2、.mp3、.mpa、.cab、.wav、.snd、.au、.asf、.wm、.avi、.z、.gz、.tgz、.frx。 これらのファイルの種類の圧縮設定は、Windows Server 2003 R2 では構成できません。

### <a name="can-an-administrator-turn-off-rdc-or-change-the-threshold"></a>管理者は、RDC を無効にしたり、しきい値を変更したりできますか?

はい。 特定の接続のプロパティ ページを使用して、RDC を無効にすることができます。 RDC を無効にすると、帯域幅の制約がない高速ローカル エリア ネットワーク (LAN) リンク、または主に 64 KB 未満のファイルで構成されるレプリケーション グループで、CPU 使用率とレプリケーション待機時間が減少します。 接続で RDC を無効にする場合は、変更前と変更後にレプリケーションの効率をテストして、レプリケーションのパフォーマンスが向上したことを確認してください。

RDC サイズのしきい値を変更するには、**Dfsradmin Connection Set** コマンドまたは DFS レプリケーション WMI プロバイダーを使用するか、構成 XML ファイルを手動で編集します。

### <a name="does-rdc-work-on-all-file-types"></a>RDC はすべてのファイルの種類で動作しますか?

はい。 RDC では、ファイルのデータの種類に関係なく、ブロック レベルで相違が計算されます。 ただし、Word 文書、PST ファイル、VHD イメージなどの特定のファイルの種類では、RDC がより効率的に動作します。

### <a name="how-does-rdc-work-on-a-compressed-file"></a>圧縮されたファイルでは RDC はどのように動作しますか?

DFS レプリケーションで使用されている RDC では、ファイル内の変更されたブロックが計算されて、それらのブロックだけがネットワーク経由で送信されます。 DFS レプリケーションでは、ファイルの内容については何も知る必要がなく、変更されたブロックだけを知る必要があります。

### <a name="is-cross-file-rdc-enabled-when-upgrading-to-windows-server-enterprise-edition-or-datacenter-edition"></a>Windows Server Enterprise Edition または Datacenter Edition にアップグレードすると、ファイル間 RDC は有効になりますか?

Windows Server の Standard Edition では、ファイル間 RDC はサポートされていません。 ただし、ファイル間 RDC がサポートされているエディションにアップグレードすると、またはレプリケーション接続のメンバーでサポートされているエディションが実行されている場合は、自動的に有効になります。 ファイル間 RDC がサポートされているエディションの一覧については、「ファイル間 RDC は Windows オペレーティング システムのどのエディションでサポートされていますか?」をご覧ください。

### <a name="is-rdc-true-block-level-replication"></a>RDC は真のブロックレベル レプリケーションですか?

いいえ。 RDC は、ファイル転送を圧縮するための汎用プロトコルです。 DFS レプリケーションでは、ディスク ブロック レベルではなく、ファイル レベルでブロックに RDC が使用されます。 RDC では、ファイルがブロックに分割されます。 ファイル内のブロックごとに、署名が計算されます。これは、大きなブロックを表すことのできる少数のバイトです。 サーバーからクライアントには、署名のセットが転送されます。 クライアントでは、サーバーの署名とクライアント自体の署名が比較されます。 クライアントは、クライアントにまだ存在しない署名のデータのみを送信するようにサーバーに要求します。

### <a name="what-happens-if-i-rename-a-file"></a>ファイルの名前を変更するとどうなりますか?

次のレプリケーション時に、DFS レプリケーションにより、レプリケーション グループの他のすべてのメンバーでファイルの名前が変更されます。 ファイルは一意の ID を使用して追跡されるので、ファイルの名前を変更したり、レプリカ内でファイルを移動したりしても、ファイルをレプリケートする DFS レプリケーションの機能には影響しません。

### <a name="what-is-cross-file-rdc"></a>ファイル間 RDC とはどのようなものですか?

ファイル間 RDC を使用することで、DFS レプリケーションでは、クライアント側に同じ名前のファイルが存在しない場合でも、RDC を使用できます。 ファイル間 RDC では、ヒューリスティックを使用して、レプリケートする必要があるファイルに似たファイルが特定され、似たファイルに含まれるレプリケート対象ファイルと同一のブロックを使用して、WAN 経由で転送されるデータの量が最小限に抑えられます。 ファイル間 RDC では、このプロセスで最大 5 つの類似ファイルのブロックを使用できます。

ファイル間 RDC を使用するには、レプリケーション接続の 1 つのメンバーで、ファイル間 RDC をサポートする Windows のエディションが実行されている必要があります。 ファイル間 RDC がサポートされているエディションの一覧については、「ファイル間 RDC は Windows オペレーティング システムのどのエディションでサポートされていますか?」をご覧ください。

### <a name="what-is-rdc"></a>RDC とは何ですか?

Remote Differential Compression (RDC) は、帯域幅に制限のあるネットワーク経由で効率的にファイルを更新するために使用できるクライアント サーバー プロトコルです。 RDC ではファイルに対するデータの挿入、削除、配置変更が検出されるので、ファイルが更新されたら、DFS レプリケーションでファイルの変更部分のみをレプリケートすることができます。 RDC は、既定では 64 KB 以上のファイルに対してのみ使用されます。 RDC では、レプリケート フォルダーまたは DfsrPrivate\\ConflictandDeleted フォルダー (レプリケート フォルダーのローカル パスにあります) 内にある同じ名前の古いバージョンのファイルを使用できます。

### <a name="when-is-rdc-used-for-replication"></a>レプリケーションではどのようなときに RDC が使用されますか?

RDC は、ファイルが最小サイズのしきい値を超えた場合に使用されます。 このサイズのしきい値は、既定では 64 KB です。 そのしきい値を超えるファイルがレプリケートされた後は、ファイルの大きな部分が変更されたり、RDC が無効になったりしない限り、ファイルの更新バージョンでは常に RDC が使用されます。

### <a name="which-editions-of-the-windows-operating-system-support-cross-file-rdc"></a>ファイル間 RDC は Windows オペレーティング システムのどのエディションでサポートされていますか?

ファイル間 RDC を使用するには、レプリケーション接続の 1 つのメンバーで、ファイル間 RDC をサポートする Windows オペレーティング システムのエディションが実行されている必要があります。 ファイル間 RDC がサポートされている Windows オペレーティング システムのエディションを次の表に示します。

### <a name="cross-file-rdc-availability-in-editions-of-the-windows-operating-system"></a>ファイル間 RDC を使用できる Windows オペレーティング システムのエディション

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
<td><p>Windows Server 2008 R2</p></td>
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

\* Windows Server 2012 R2 では、必要に応じて、ファイル間 RDC を無効にすることができます。

## <a name="replication-details"></a>レプリケーションの詳細

### <a name="can-i-change-the-path-for-a-replicated-folder-after-it-is-created"></a>レプリケート フォルダーの作成後に、そのパスを変更できますか?

いいえ。 レプリケート フォルダーのパスを変更する必要がある場合は、DFS 管理でそのパスを削除し、新しいレプリケート フォルダーとして追加し直す必要があります。 DFS レプリケーションでは、その後、Remote Differential Compression (RDC) を使用して同期が実行され、送信側メンバーと受信側メンバーでデータが同じかどうかが判断されます。 フォルダー内のすべてのデータが再度レプリケートされることはありません。

### <a name="can-i-configure-which-file-attributes-are-replicated"></a>レプリケートされるファイル属性を構成できますか?

いいえ。DFS レプリケーションでレプリケートされるファイル属性を構成することはできません。

属性値とその説明の一覧については、MSDN の「[ファイル属性](https://go.microsoft.com/fwlink/?linkid=182268)」 (https://go.microsoft.com/fwlink/?LinkId=182268) を参照してください。

次の属性値は、`SetFileAttributes dwFileAttributes` 関数を使用して設定され、DFS レプリケーションによってレプリケートされます。 これらの属性値を変更すると、属性のレプリケーションがトリガーされます。 内容も変更されない限り、ファイルの内容はレプリケートされません。 詳しくは、MSDN ライブラリの「[SetFileAttributes 関数](https://go.microsoft.com/fwlink/?linkid=182269)」 (https://go.microsoft.com/fwlink/?LinkId=182269) をご覧ください。

  - FILE\_ATTRIBUTE\_HIDDEN  
      
  - FILE\_ATTRIBUTE\_READONLY  
      
  - FILE\_ATTRIBUTE\_SYSTEM  
      
  - FILE\_ATTRIBUTE\_NOT\_CONTENT\_INDEXED  
      
  - FILE\_ATTRIBUTE\_OFFLINE  
      

次の属性値は、DFS レプリケーションによってレプリケートされますが、レプリケーションをトリガーすることはありません。

  - FILE\_ATTRIBUTE\_ARCHIVE  
      
  - FILE\_ATTRIBUTE\_NORMAL  
      

次のファイル属性値でもレプリケーションがトリガーされますが、`SetFileAttributes` 関数を使用して設定することはできません (属性値を表示するには `GetFileAttributes` 関数を使用します)。

  - FILE\_ATTRIBUTE\_REPARSE\_POINT  
      

> [!NOTE]
> 再解析タグが IO_REPARSE_TAG_SYMLINK でない場合、DFS レプリケーションでは再解析ポイントの属性値はレプリケートされません。 再解析タグが IO_REPARSE_TAG_DEDUP、IO_REPARSE_TAG_SIS、または IO_REPARSE_TAG_HSM であるファイルは、通常のファイルとしてレプリケートされます。 ただし、再解析ポイントはローカル システムでのみ機能するため、再解析タグと再解析データ バッファーは、他のサーバーにはレプリケートされません。 
<br>

  - FILE\_ATTRIBUTE\_COMPRESSED  
      
  - FILE\_ATTRIBUTE\_ENCRYPTED  
      

> [!NOTE]
> DFS レプリケーションでは、暗号化ファイル システム (EFS) を使用して暗号化されたファイルはレプリケートされません。 DFS レプリケーションでは、Microsoft 以外のソフトウェアを使用して暗号化されたファイルは、ファイルで FILE_ATTRIBUTE_ENCRYPTED 属性値が設定されていない場合にのみ、レプリケートされます。 
<br>

  - FILE\_ATTRIBUTE\_SPARSE\_FILE  
      
  - FILE\_ATTRIBUTE\_DIRECTORY  
      

DFS レプリケーションでは、FILE\_ATTRIBUTE\_TEMPORARY の値はレプリケートされません。

### <a name="can-i-control-which-member-is-replicated"></a>レプリケートされるメンバーを制御できますか?

はい。 レプリケーション グループを作成するときに、トポロジを選択できます。 または、 **[トポロジなし]** を選択し、レプリケーション グループの作成後に手動で接続を構成することもできます。

### <a name="can-i-seed-a-replication-group-member-with-data-prior-to-the-initial-replication"></a>初期レプリケーションの前に、レプリケーション グループ メンバーにデータをシードできますか?

はい。 DFS レプリケーションでは、初期レプリケーションの前に、レプリケーション グループ メンバーにファイルをコピーできます。 この "事前設定" により、初期レプリケーションの間にレプリケートされるデータの量を大幅に削減できます。

ファイルで異なっているのが実際の属性またはタイムスタンプだけの場合、初期レプリケーションで内容をレプリケートする必要はありません。 実際の属性とは、Win32 関数 `SetFileAttributes` によって設定できる属性です。 詳しくは、MSDN ライブラリの「[SetFileAttributes 関数](https://go.microsoft.com/fwlink/?linkid=182269)」 (https://go.microsoft.com/fwlink/?LinkId=182269) をご覧ください。 2 つのファイルの間で圧縮などの他の属性が異なっている場合は、ファイルの内容がレプリケートされます。

レプリケーション グループのメンバーを事前設定するには、レプリケート先サーバーの適切なフォルダーにファイルをコピーし、レプリケーション グループを作成してから、プライマリ メンバーを選択します。 プライマリ メンバーの内容は "権限がある" と見なされるため、レプリケートしたい最新のファイルを持つメンバーを選択します。 つまり、初期レプリケーションの間に、レプリケーション グループの他のメンバーのファイルの他のバージョンは、プライマリ メンバーのファイルによって常に上書きされます。

DFSR データベースの事前シードと複製については、「[Windows Server 2012 R2 での DFS レプリケーションの初期同期: 複製の攻撃](https://blogs.technet.com/b/filecab/archive/2013/08/21/dfs-replication-initial-sync-in-windows-server-2012-r2-attack-of-the-clones.aspx)」をご覧ください。

初期レプリケーションについて詳しくは、「[レプリケーション グループを作成する](https://technet.microsoft.com/library/cc725893)」をご覧ください。

### <a name="does-dfs-replication-overcome-common-file-replication-service-issues"></a>ファイル レプリケーション サービスの一般的な問題は DFS レプリケーションによって解決しますか?

はい。 DFS レプリケーションでは、次の 3 つの一般的な FRS の問題が解決されます。

  - ジャーナルのラップ: DFS レプリケーションを使うと、ジャーナルのラップが即座に回復されます。 レプリケーションが再度有効にされる前に、既存の各ファイルまたはフォルダーは journalWrap としてマークされ、ファイル システムに対して検証されます。 回復の間に、このボリュームはどちらの方向のレプリケーションにも使用できません。  
      
  - 過剰なレプリケーション: 過剰なレプリケーションを防ぐため、DFS レプリケーションではクレジットのシステムが使用されます。  
      
  - フォルダーのモーフィング: フォルダー名のモーフィングを防ぐため、DFS レプリケーションでは、競合するデータが隠し属性の DfsrPrivate\\ConflictandDeleted フォルダー (レプリケート フォルダーのローカル パスの下にあります) に格納されます。 たとえば、FRS を使用してレプリケートされる複数のサーバーに同じ名前を持つ複数のフォルダーが同時に作成されると、FRS によって古いフォルダーの名前が変更されます。 DFS レプリケーションでは、代わりに、古いフォルダーは ConflictandDeleted フォルダーに移動されます。  
      

### <a name="does-dfs-replication-replicate-files-in-chronological-order"></a>DFS レプリケーションではファイルは時系列の順序でレプリケートされますか?

いいえ。 ファイルは、順不同でレプリケートされる可能性があります。

### <a name="does-dfs-replication-replicate-files-that-are-being-used-by-another-application"></a>DFS レプリケーションでは別のアプリケーションによって使用されているファイルがレプリケートされますか?

アプリケーションによってファイルが開かれて、ファイル ロックが作成された場合 (開かれている間、他のアプリケーションではそのファイルを使用できません)、DFS レプリケーションでは、そのファイルは閉じられるまでレプリケートされません。 アプリケーションによってファイルが読み取り共有アクセスでを開かれた場合は、ファイルをレプリケートできます。

### <a name="does-dfs-replication-replicate-ntfs-file-permissions-alternate-data-streams-hard-links-and-reparse-points"></a>DFS レプリケーションでは、NTFS ファイルのアクセス許可、代替データ ストリーム、ハード リンク、再解析ポイントはレプリケートされますか?

  - DFS レプリケーションでは、NTFS ファイルのアクセス許可と代替データ ストリームはレプリケートされます。  
      
  - レプリケート フォルダー内のファイルとの間での NTFS ハード リンクの作成はサポートされていません。それを行うと、影響を受けるファイルでレプリケーションの問題が発生する可能性があります。 ハード リンク ファイルは DFS レプリケーションによって無視され、レプリケートされません。 また、接合ポイントもレプリケートされず、DFS レプリケーションでは検出された各接合ポイントに対してイベント 4406 がログに記録されます。  
      
  - DFS レプリケーションによってレプリケートされる再解析ポイントは、IO\_REPARSE\_TAG\_SYMLINK タグが使用されているものだけです。ただし、DFS レプリケーションでは、シンボリックリンクのターゲットもレプリケートされる保証はありません。 詳しくは、[ディレクトリ サービス チームへの質問ブログ](https://blogs.technet.com/b/askds/archive/2011/09/30/friday-mail-sack-super-slo-mo-edition.aspx)をご覧ください。  
      
  - 再解析タグ IO\_REPARSE\_TAG\_DEDUP、IO\_REPARSE\_TAG\_SIS、または IO\_REPARSE\_TAG\_HSM が設定されたファイルは、通常のファイルとしてレプリケートされます。 再解析ポイントはローカル システムでのみ機能するため、再解析タグと再解析データ バッファーは、他のサーバーにはレプリケートされません。 そのため、DFS レプリケーションでは、Windows Server 2012 のデータ重複除去または単一インスタンス記憶域 (SIS) を使用するボリューム上のフォルダーをレプリケートできますが、データ重複除去情報は、役割サービスが有効になっている各サーバーによって個別に保持されます。  
      

### <a name="does-dfs-replication-replicate-timestamp-changes-if-no-other-changes-are-made-to-the-file"></a>ファイルに対してタイムスタンプ以外の変更が行われていない場合、DFS レプリケーションではタイムスタンプの変更がレプリケートされますか?

いいえ。DFS レプリケーションでは、タイムスタンプだけが変更されているファイルはレプリケートされません。 また、ファイルの変更がタイムスタンプだけの場合、変更されたタイムスタンプは、レプリケーション グループの他のメンバーにレプリケートされません。

### <a name="does-dfs-replication-replicate-updated-permissions-on-a-file-or-folder"></a>DFS レプリケーションでは、ファイルまたはフォルダーで更新されたアクセス許可がレプリケートされますか?

はい。 DFS レプリケーションを使うと、ファイルとフォルダーに対するアクセス許可の変更がレプリケートされます。 アクセス制御リスト (ACL) に関連付けられているファイルの部分のみがレプリケートされますが、DFS レプリケーションではファイル全体をステージング領域に読み取る必要があります。


> [!NOTE]
> 多数のファイルで ACL を変更すると、レプリケーションのパフォーマンスに影響する可能性があります。 ただし、RDC を使用すると、転送されるデータの量は、ファイル全体のサイズではなく、ACL のサイズに比例します。 それでも、ステージング フォルダーとの間でファイルの読み取りを行う必要があるため、ディスク トラフィックの量はファイルのサイズに比例します。 
<br>


### <a name="does-dfs-replication-support-merging-text-files-in-the-event-of-a-conflict"></a>DFS レプリケーションでは、競合が発生した場合のテキスト ファイルのマージがサポートされますか?

DFS レプリケーションでは、競合があってもファイルはマージされません。 ただし、競合が検出されたコンピューターの隠し属性の DfsrPrivate\\ConflictandDeleted フォルダーに、古いバージョンのファイルの保持が試みられます。

### <a name="does-dfs-replication-use-encryption-when-transmitting-data"></a>DFS レプリケーションでは、データの送信時に暗号化が使用されますか?

はい。 DFS レプリケーションでは、リモート プロシージャ コール (RPC) 接続で暗号化が使用されます。

### <a name="is-it-possible-to-disable-the-use-of-encrypted-rpc"></a>暗号化された RPC の使用を無効にすることはできますか?

いいえ。 DFS レプリケーション サービスでは、TCP 経由のリモート プロシージャ コール (RPC) を使用してデータがレプリケートされます。 インターネット経由のデータ転送をセキュリティ保護するため、DFS レプリケーション サービスは、認証レベルの定数 `RPC_C_AUTHN_LEVEL_PKT_PRIVACY` を常に使用するように設計されています。 これにより、インターネット経由の RPC 通信は常に暗号化されます。 したがって、DFS レプリケーション サービスによる暗号化された RPC の使用を無効にすることはできません。

詳細については、次の Microsoft Web サイトを参照してください。

  - [RPC テクニカル リファレンス](https://go.microsoft.com/fwlink/?linkid=182278)  
      
  - [Remote Differential Compression について](https://go.microsoft.com/fwlink/?linkid=182279)  
      
  - [認証レベルの定数](https://go.microsoft.com/fwlink/?linkid=182280)  
      

### <a name="how-are-simultaneous-replications-handled"></a>同時レプリケーションはどのように処理されますか?

レプリケート フォルダーごとに更新マネージャーが 1 つあります。 更新マネージャーは、相互に独立して動作します。

既定では、最大で 16 個 (Windows Server 2003 R2 では 4 個) の同時ダウンロードが、すべての接続とレプリケーション グループで共有されます。 接続とレプリケーション グループの更新はシリアル化されないため、特定の順序で更新が受け取られることはありません。 2 つのスケジュールが開かれている場合、通常、更新は両方の接続から同時に受け取られてインストールされます。

### <a name="how-do-i-force-replication-or-polling"></a>レプリケーションまたはポーリングを強制的に行うにはどうすればよいですか?

DFS 管理を使用することで、直ちにレプリケーションを強制的に実行できます。[レプリケーション スケジュールの編集](https://technet.microsoft.com/library/Cc732278)に関するページをご覧ください。 また、Windows Server 2012 R2 で導入された DFSR PowerShell モジュールに含まれる `Sync-DfsReplicationGroup` コマンドレット、または **Dfsrdiag SyncNow** コマンドを使用して、レプリケーションを強制的に行うこともできます。 強制的なポーリングは、`Update-DfsrConfigurationFromAD` コマンドレットまたは **Dfsrdiag PollAD** コマンドを使用して実行できます。

### <a name="is-it-possible-to-configure-a-quiet-time-between-replications-for-files-that-change-frequently"></a>頻繁に変更されるファイルのレプリケーション間の待ち時間を構成できますか?

いいえ。 スケジュールが開いている場合、DFS レプリケーションで認識された変更はすぐにレプリケートされます。 ファイルの待ち時間を構成する方法はありません。

### <a name="is-it-possible-to-configure-one-way-replication-with-dfs-replication"></a>DFS レプリケーションで一方向のレプリケーションを構成することはできますか?

はい。 Windows Server 2012 または Windows Server 2008 R2 を使用している場合は、一方向の接続を介して内容がレプリケートされる読み取り専用のレプリケート フォルダーを作成できます。 詳しくは、「[特定のメンバーでレプリケート フォルダーを読み取り専用にする](https://go.microsoft.com/fwlink/?linkid=156740)」 (https://go.microsoft.com/fwlink/?LinkId=156740) をご覧ください。

Windows Server 2008 または Windows Server 2003 R2 の DFS レプリケーションでは、一方向のレプリケーション接続の作成はサポートされていません。 それを行うと、正常性チェックのトポロジ エラー、ステージングの問題、DFS レプリケーション データベースに関する問題など、さまざまな問題が発生する可能性があります。

Windows Server 2008 または Windows Server 2003 R2 を使っている場合は、次の操作を実行することで一方向の接続をシミュレートできます。

  - プライマリ サーバーとして指定されたサーバーでのみ変更を行うよう、管理者を訓練します。 その後、変更内容を転送先サーバーにレプリケートします。  
      
  - レプリケート先サーバーで共有アクセス許可を構成し、エンド ユーザーが書き込みアクセス許可を持たないようにします。 ブランチ サーバーでの変更が許可されていない場合、逆方向には何もレプリケートされなくなり、一方向の接続がシミュレートされて、WAN の使用率が低く抑えられます。  
      

### <a name="is-there-a-way-to-force-a-complete-replication-of-all-files-including-unchanged-files"></a>変更されていないファイルを含むすべてのファイルの完全なレプリケーションを強制する方法はありますか?

いいえ。 DFS レプリケーションでは、同一であると見なされたファイルはレプリケートされません。 変更されたファイルがレプリケートされていない場合、自動的にレプリケートするように構成されていると、DFS レプリケーションではそれが実行されます。 構成したスケジュールを上書きするには、WMI のメソッド **ForceReplicate()** を使用します。 ただし、スケジュールが上書きされるだけであり、変更されていないファイルまたは同一のファイルのレプリケーションは強制されません。

### <a name="what-happens-if-the-primary-member-suffers-a-database-loss-during-initial-replication"></a>初期レプリケーションの間にプライマリ メンバーでデータベースの損失が発生するとどうなりますか?

初期レプリケーションのとき、受信側メンバーのプライマリ メンバーに異なるバージョンのファイルがあった場合に発生する競合の解決では、プライマリ メンバーのファイルが常に優先されます。 プライマリ メンバーの指定は Active Directory Domain Services に格納され、プライマリ メンバーのレプリケートの準備ができた後、レプリケーション グループのすべてのメンバーがレプリケートされる前に、その指定はクリアされます。

初期レプリケーションが失敗した場合、またはレプリケーション中に DFS レプリケーション サービスが再起動された場合、プライマリ メンバーにより、ローカル DFS レプリケーション データベース内にプライマリ メンバーの指定が検出されて、初期レプリケーションが再試行されます。 Active Directory Domain Services でプライマリの指定がクリアされた後、レプリケーション グループのすべてのメンバーの初期レプリケーションが完了する前に、プライマリ メンバーの DFS レプリケーション データベースが失われた場合、プライマリ メンバーとして指定されているサーバーがないため、レプリケーション グループのすべてのメンバーでフォルダーのレプリケーションが失敗します。 このような場合は、プライマリ メンバー サーバーで **Dfsradmin membership /set /isprimary:true** コマンドを使用して、プライマリメ ンバーの指定を手動で復元します。

初期レプリケーションについて詳しくは、「[レプリケーション グループを作成する](https://technet.microsoft.com/library/cc725893)」をご覧ください。


> [!WARNING]
> プライマリ メンバーの指定は、初期レプリケーション プロセスの間にのみ使用されます。 レプリケーションの完了後に <STRONG>Dfsradmin</STRONG> コマンドを使用してレプリケート フォルダーのプライマリ メンバーを指定した場合、DFS レプリケーションでは、サーバーが Active Directory Domain Services でプライマリ メンバーとして指定されません。 ただし、その後、サーバー上の DFS レプリケーション データベースで回復不可能な破損またはデータ損失が発生した場合、サーバーでは、レプリケーション グループの別のメンバーからデータを回復するのではなく、プライマリ メンバーとして初期レプリケーションの実行が試みられます。 基本的に、サーバーは非承認のプライマリ サーバーになり、競合が発生する可能性があります。 このため、初期レプリケーションが回復不可能なほど失敗したことが確実である場合にのみ、プライマリ メンバーを手動で指定してください。 
<br>


### <a name="what-happens-if-the-replication-schedule-closes-while-a-file-is-being-replicated"></a>ファイルのレプリケート中にレプリケーション スケジュールが終了するとどうなりますか?

接続で Remote Differential Compression (RDC) が有効になっている場合、スケジュールが終了する直前にレプリケートが開始された (または、**帯域幅なし**に変更された) 64 KB より大きいファイルの受信レプリケーションは、スケジュールが開始すると (または**帯域幅なし**以外に変更されると) 続行されます。 レプリケーションは、レプリケーションが停止したときの状態から続行されます。

RDC がオフになっている場合は、DFS レプリケーションによってファイル転送が完全に最初から再開されます。 受信側メンバーでファイルが使用可能になっていると、これは遅延する可能性があります。

### <a name="what-happens-when-two-users-simultaneously-update-the-same-file-on-different-servers"></a>2 人のユーザーが異なるサーバー上で同じファイルを同時に更新するとどうなりますか?

DFS レプリケーションによって競合が検出されると、最後に保存されたファイルのバージョンが使用されます。 他のファイルは、DfsrPrivate\\ConflictandDeleted フォルダー (競合が解決されたコンピューター上のレプリケート フォルダーのローカル パスの下) に保存されます。 ConflictandDeleted フォルダーがクリーンアップされるまでそこに保持されます。クリーンアップは、ConflictandDeleted フォルダーが構成されたサイズを超えた場合、または DFS レプリケーションでディスク領域不足エラーが発生した場合に行われます。 ConflictandDeleted フォルダーはレプリケートされません。この競合解決方法により、FRS で発生する可能性があったディレクトリのモーフィングの問題が回避されます。

競合が発生すると、DFS レプリケーションにより、情報イベントが DFS レプリケーション イベント ログに記録されます。 次の理由により、ユーザーがこのイベントに対応する必要はありません。

  - ユーザーからは見えません (サーバー管理者だけが見ることができます)。  
      
  - DFS レプリケーションでは、ConflictandDeleted フォルダーはキャッシュとして扱われます。 クォータのしきい値に達すると、それらのファイルの一部はクリーンアップされます。 競合するファイルが保存される保証はありません。  
      
  - 競合は、競合の発生元とは異なるサーバー上に存在する可能性があります。  
      

## <a name="staging"></a>ステージング

### <a name="does-dfs-replication-continue-staging-files-when-replication-is-disabled-by-a-schedule-or-bandwidth-throttling-quota-or-when-a-connection-is-manually-disabled"></a>スケジュールまたは帯域幅調整クォータによってレプリケーションが無効にされたとき、または手動で接続を無効にしたときに、DFS レプリケーションによるファイルのステージングは続行されますか?

いいえ。 スケジュールされているレプリケーション時間の範囲外になったときと、帯域幅調整クォータを超過した場合、または接続が無効になったときは、DFS レプリケーションによるファイルのステージングは続行されません。

### <a name="does-dfs-replication-prevent-other-applications-from-accessing-a-file-during-staging"></a>ステージング中は、DFS レプリケーションにより他のアプリケーションのファイル アクセスが禁止されますか?

いいえ。 DFS レプリケーションでは、ユーザーやアプリケーションがレプリケーション フォルダー内のファイルを開くことがブロックされない方法でファイルが開かれます。 この方法は "便宜的ロック" と呼ばれます。

### <a name="is-it-possible-to-change-the-location-of-the-staging-folder-with-the-dfs-management-tool"></a>DFS 管理ツールを使用して、ステージング フォルダーの場所を変更することはできますか?

はい。 ステージング フォルダーの場所は、レプリケーション グループの各メンバーについて、 **[プロパティ]** ダイアログ ボックスの **[詳細]** タブで構成します。

### <a name="when-are-files-staged"></a>ファイルはどのようなときにステージングされますか?

次の表に示すように、受信側メンバーがファイルを要求したときに、送信側メンバーでファイルがステージングされます (ファイルが 64 KB 以下である場合以外)。 接続で Remote Differential Compression (RDC) が無効になっている場合、ファイルは 256 KB 以下でない限りステージングされます。 また、ファイルは、サイズが 64 KB 未満の場合、転送されるときに受信側メンバーでもステージングされます。ただし、この設定は 16 KB から 1 MB の範囲で構成できます。 スケジュールが終了される場合、ファイルはステージングされません。

### <a name="the-minimum-file-sizes-for-staging-files"></a>ステージング ファイルの最小ファイル サイズ

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
<th>RDC 無効</th>
</tr>
</thead>
<tbody>
<tr class="even">
<td><p>送信側メンバー</p></td>
<td><p>64 KB</p></td>
<td><p>256 KB</p></td>
</tr>
<tr class="odd">
<td><p>受信側メンバー</p></td>
<td><p>64 KB (既定)</p></td>
<td><p>64 KB (既定)</p></td>
</tr>
</tbody>
</table>

### <a name="what-happens-if-a-file-is-changed-after-it-is-staged-but-before-it-is-completely-transmitted-to-the-remote-site"></a>ステージングされた後、リモート サイトに完全に転送される前に、ファイルが変更された場合はどうなりますか?

ファイルのいずれかの部分が既に転送されている場合、DFS レプリケーションでは転送が続けららます。 DFS レプリケーションによるファイルの送信が開始される前にファイルが変更された場合は、ファイルの新しいバージョンが送信されます。

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
<th>原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>2018 年 11 月 15 日</p></td>
<td><p>Windows Server 2019 用に更新されました。</p></td>
<td><p>新しいオペレーティング システム。</p></td>
</tr>
<tr class="even">
<td><p>2013 年 10 月 9 日</p></td>
<td><p>Windows Server 2012 R2でのテスト結果で、「DFS レプリケーションにはどのような制限がありますか?」セクションを更新しました。</p></td>
<td><p>最新バージョンの Windows Server に関する更新</p></td>
</tr>
<tr class="odd">
<td><p>2013 年 1 月 30 日</p></td>
<td><p>「スケジュールまたは帯域幅調整クォータによってレプリケーションが無効にされたとき、または手動で接続を無効にしたときに、DFS レプリケーションによるファイルのステージングは続行されますか?」エントリを追加しました。</p></td>
<td><p>お客様の質問</p></td>
</tr>
<tr class="even">
<td><p>2012 年 10 月 31 日</p></td>
<td><p>「DFS レプリケーションにはどのような制限がありますか?」エントリを編集し、テストされたボリューム上のレプリケート済みファイルの数を増やしました。</p></td>
<td><p>カスタマー フィードバック</p></td>
</tr>
<tr class="odd">
<td><p>2012 年 8 月 15 日</p></td>
<td><p>「DFS レプリケーションでは、NTFS ファイルのアクセス許可、代替データ ストリーム、ハード リンク、再解析ポイントはレプリケートされますか?」エントリを編集し、DFS レプリケーションによるハード リンクと再解析ポイントの処理方法を明確にしました。</p></td>
<td><p>カスタマー サポート サービスからのフィードバック</p></td>
</tr>
<tr class="even">
<td><p>2012 年 6 月 13 日</p></td>
<td><p>「DFS レプリケーションは ReFS ボリュームまたは FAT ボリュームで動作しますか?」エントリを編集し、ReFS の説明を追加しました。</p></td>
<td><p>カスタマー フィードバック</p></td>
</tr>
<tr class="odd">
<td><p>2012 年 4 月 25 日</p></td>
<td><p>「DFS レプリケーションでは、NTFS ファイルのアクセス許可、代替データ ストリーム、ハード リンク、再解析ポイントはレプリケートされますか?」エントリを編集し、DFS レプリケーションによるハード リンクの処理方法を明確にしました。</p></td>
<td><p>混乱の可能性の低減</p></td>
</tr>
<tr class="even">
<td><p>2011 年 3 月 30 日</p></td>
<td><p>「Outlook の .pst ファイルまたは Microsoft Office Access のデータベース ファイルを、DFS レプリケーションでレプリケートできますか?」エントリを編集し、.pst ファイルと Access ファイルで DFS レプリケーションを使用したときに可能性のある影響を修正しました。</p>
<p>「レプリケーションのパフォーマンスを向上させるにはどうすればよいですか?」を追加しました。</p></td>
<td><p>前のエントリに関するお客様の質問 .pst ファイルまたは Access ファイルをレプリケートすると DFS レプリケーション データベースが破損する可能性があると、誤って示されていました。</p></td>
</tr>
<tr class="odd">
<td><p>2011 年 1 月 26 日</p></td>
<td><p>「ConflictAndDeleted または PreExisting フォルダーからファイルを回復するにはどうすればよいですか?」を追加しました。</p></td>
<td><p>カスタマー フィードバック</p></td>
</tr>
<tr class="even">
<td><p>2010 年 10 月 20 日</p></td>
<td><p>「DFS レプリケーション メンバーをアップグレードまたは置換するにはどうすればよいですか?」を追加しました。</p></td>
<td><p>カスタマー フィードバック</p></td>
</tr>
</tbody>
</table>

