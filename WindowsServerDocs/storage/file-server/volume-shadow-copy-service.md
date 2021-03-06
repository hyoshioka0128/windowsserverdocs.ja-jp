---
Title: ボリューム シャドウ コピー サービス
ms.date: 01/30/2019
ms.prod: windows-server-threshold
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 0a4af25723c6d1e796cd3255875c15faf21fb8be
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284380"
---
# <a name="volume-shadow-copy-service"></a>ボリューム シャドウ コピー サービス

適用対象:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、および Windows Server 2008 R2、Windows Server 2008、Windows 10、Windows 8.1、Windows 8、Windows 7

バックアップと復元の重要なビジネス データは、次の問題が非常に複雑なできます。

  - 通常、データは、データを生成するアプリケーションの実行中にバックアップする必要があります。 つまり、一部のデータ ファイルが開いて可能性がありますまたは不整合な状態である可能性があります。  
      
  - データ セットが大きい場合、一度に 1 つをバックアップするすべての難しいことができます。  
      

バックアップと復元の操作を正しく実行するには、バックアップのアプリケーションがバックアップされている、基幹業務アプリケーションと記憶域管理のハードウェアおよびソフトウェアとの間の密接な調整が必要です。 ボリューム シャドウ コピー サービス (VSS)、Windows Server® 2003 で導入されたには、適切に共同作業できるように、これらのコンポーネント間のメッセージ交換が容易になります。 VSS をサポートするすべてのコンポーネント、ときに、アプリケーションをオフラインにせずアプリケーション データのバックアップを使用できます。

VSS は、バックアップされるデータの一貫性のあるシャドウ コピー (スナップショットまたは特定の時点のコピーとも呼ばれます) を作成するために必要なアクションを調整します。 シャドウ コピーとして使用できるは、または、次のようなシナリオで使用できます。

  - アプリケーション データとシステム状態については、別のハード ディスク ドライブ、テープ、またはその他のリムーバブル メディアのデータのアーカイブを含むバックアップするには。  
      
  - データ マイニングとしています。  
      
  - ディスクからディスクへのバックアップを実行しています。  
      
  - 元の LUN に、または失敗した元の LUN を置換するまったく新しい LUN には、データを復元することによってデータの損失から迅速に回復する必要があります。  
      

Windows の機能と VSS を使用するアプリケーションを次に示します。

  - [Windows Server バックアップ](http://go.microsoft.com/fwlink/?linkid=180891)(http://go.microsoft.com/fwlink/?LinkId=180891)  
      
  - [共有フォルダーのシャドウ コピー](http://go.microsoft.com/fwlink/?linkid=142874) (http://go.microsoft.com/fwlink/?LinkId=142874)  
      
  - [System Center Data Protection Manager](http://go.microsoft.com/fwlink/?linkid=180892) (http://go.microsoft.com/fwlink/?LinkId=180892)  
      
  - [システムの復元](http://go.microsoft.com/fwlink/?linkid=180893)(http://go.microsoft.com/fwlink/?LinkId=180893)  
      

## <a name="how-volume-shadow-copy-service-works"></a>ボリューム シャドウ コピー サービスのしくみ

VSS の完全なソリューションでは、次の基本的な部分すべてが必要です。

**VSS サービス**   他のコンポーネントに確実に Windows オペレーティング システムの一部が適切に相互通信および連携します。

**VSS リクエスター**   シャドウ コピー (または他の高度な操作をインポートまたは削除するなど) の実際の作成を要求するソフトウェア。 通常、これは、バックアップ アプリケーションです。 Windows Server バックアップ ユーティリティと System Center Data Protection Manager のアプリケーションは、VSS の依頼者です。 非 Microsoft® VSS 依頼者には、Windows で実行されているほぼすべてのバックアップ ソフトウェアが含まれます。

**VSS ライター**   をバックアップする一貫性のあるデータ セットがあることを保証するコンポーネント。 これは通常、SQL Server® または Exchange Server などの基幹業務アプリケーションの一部として提供します。 レジストリなどのさまざまな Windows コンポーネントの VSS ライターは、Windows オペレーティング システムに含まれています。 Microsoft 以外の VSS ライターは、バックアップ時にデータの整合性を保証する必要がある Windows の多くのアプリケーションに含まれています。

**VSS プロバイダー**   作成して、シャドウ コピーを維持するコンポーネント。 これは、エラーは、ソフトウェアまたはハードウェアに発生することができます。 Windows オペレーティング システムには、コピー オン ライトを使用する VSS プロバイダーが含まれています。 記憶域エリア ネットワーク (SAN) を使用すると、提供されている場合が、SAN の VSS ハードウェア プロバイダーをインストールすることが重要です。 ハードウェア プロバイダーの作成と、ホスト オペレーティング システムからシャドウ コピーの保守タスクをオフロードします。

次の図は、VSS サービスのボリュームのシャドウ コピーを作成するには、依頼者、ライター、およびプロバイダーと連携を示しています。

![](media/volume-shadow-copy-service/Ee923636.94dfb91e-8fc9-47c6-abc6-b96077196741(WS.10).jpg)

**図 1**   ボリューム シャドウ コピー サービスのアーキテクチャ図

### <a name="how-a-shadow-copy-is-created"></a>シャドウ コピーを作成する方法

このセクションでは、シャドウ コピーを作成するために必要な手順を一覧表示して、コンテキストに、依頼者、ライター、およびプロバイダーのさまざまな役割を設定します。 次の図は、ボリューム シャドウ コピー サービスが要求元、ライター、およびプロバイダーの全体的な調整を制御する方法を示します。

![](media/volume-shadow-copy-service/Ee923636.1c481a14-d6bc-4796-a3ff-8c6e2174749b(WS.10).jpg)

**図 2**シャドウ コピーの作成プロセス

シャドウ コピーを作成するには、依頼者、ライター、およびプロバイダーは、次の操作を実行します。

1.  依頼者は、ライターを列挙し、ライターのメタデータの情報を収集し、シャドウ コピーの作成を準備するには、ボリューム シャドウ コピー サービスを確認します。  
      
2.  各ライターでは、バックアップする必要があるコンポーネントとデータ ストアの XML 記述を作成し、ボリューム シャドウ コピー サービスに提供します。 ライターでは、すべてのコンポーネントに使用される復元メソッドも定義します。 ボリューム シャドウ コピー サービスがバックアップされるコンポーネントを選択します。 要求元に、ライターの説明を提供します。  
      
3.  ボリューム シャドウ コピー サービスでは、シャドウ コピーを行うためのデータを準備するすべてのライターに通知します。  
      
4.  各ライターは、適切なデータを準備は、すべての完了など、トランザクション、トランザクション ログ、ロール、およびキャッシュのフラッシュを開きます。 データのシャドウ コピーする準備ができたら、ライターは、ボリューム シャドウ コピー サービスに通知します。  
      
5.  ボリューム シャドウ コピー サービス アプリケーションの書き込み I/O 要求 (I/O 要求は引き続き可能読み取り) を一時的に固定するのには、ライターに指示のボリュームまたはボリュームのシャドウ コピーを作成するために必要ないくつかの秒。 60 秒より長くかかるは、アプリケーションのフリーズすることはできません。 ボリューム シャドウ コピー サービスは、ファイル システムのバッファーをフラッシュし、し、これによって、ファイル システムのメタデータが正しく記録られ、シャドウ コピーするデータが一貫性のある順序で記述されたファイル システムがフリーズします。  
      
6.  ボリューム シャドウ コピー サービスは、シャドウ コピーを作成するプロバイダーに指示します。 シャドウ コピーの作成期間では、10 秒以内、ファイル システムへの I/O 要求が固定すべて書き込みをする時に継続します。  
      
7.  ボリューム シャドウ コピー サービスは、ファイル システム書き込み I/O 要求を解放します。  
      
8.  VSS は、ライターではアプリケーション書き込み I/O 要求を再開するように指示します。 この時点でアプリケーションはシャドウ コピーをディスクにデータを書き込むを再開する無料です。  
      

> [!NOTE]
> ライターが 60 秒またはプロバイダーがシャドウ コピーをコミットする 10 秒より長くかかるかどうかよりも長く保持状態に保持した場合は、シャドウ コピーの作成を中止することができます。 
<br>

9. 依頼者は、プロセス (手順 1 に戻す移動) を再試行できますか、後で再試行するには、管理者に通知します。  
      
10. シャドウ コピーが正常に作成すると、ボリューム シャドウ コピー サービスは、要求元にシャドウ コピーの場所の情報を返します。 場合によっては、シャドウ コピー一時的に使用できる読み取り/書き込みボリュームとしてので、シャドウ コピーが完了する前に、その VSS と 1 つまたは複数のアプリケーションからシャドウ コピーの内容に変更することができます。 VSS と、アプリケーションは、その変更を行った後、シャドウ コピーは、読み取り専用に作成されます。 このフェーズは、自動復旧と呼ばれ、ファイル システムまたはアプリケーション トランザクションのシャドウ コピー ボリューム シャドウ コピーを作成する前に完了しなかったを元に戻すために使用されます。  
      

### <a name="how-the-provider-creates-a-shadow-copy"></a>プロバイダーがシャドウ コピーを作成する方法

ハードウェアまたはソフトウェアのシャドウ コピー プロバイダーは、シャドウ コピーを作成するため、次のメソッドのいずれかを使用します。

**コピーの完了**   このメソッドは、元のボリュームの完全なコピー (「完全なコピー」や「複製」と呼ばれます) を特定の時点で、します。 このコピーは読み取り専用です。

**コピー オン ライト**   このメソッドでは、元のボリュームはコピーされません。 代わりに、時間でボリュームには特定の時点の後に行われたすべての変更 (完了した書き込み I/O 要求) をコピーして差分コピーを作成します。

**書き込み時のリダイレクト**   このメソッドは、元のボリュームをコピーしていないは変更しないように、元のボリュームを特定の時点より後にします。 代わりに、すべての変更を別のボリュームにリダイレクトすることで、差分コピーを作成します。

## <a name="complete-copy"></a>完全なコピー

完全なコピーは通常、次のように「分割ミラー」を作成します。

1.  元のボリュームおよびシャドウ コピー ボリュームは、ミラー化されたボリュームのセットです。  
      
2.  シャドウ コピー ボリュームが元のボリュームから区切られます。 これには、ミラー接続が中断されます。  
      

ミラー接続が切断された後、元のボリュームおよびシャドウ コピー ボリュームは依存しません。 シャドウ コピー中に (書き込み I/O 要求) のすべての変更を受け入れるように、元のボリュームが引き続きボリューム、中断時に、元のデータの正確な読み取り専用コピーの状態します。

### <a name="copy-on-write-method"></a>コピー オン ライト メソッド

書き込み時コピー メソッドで元のボリュームに変更が発生した (ただし、書き込みの前に、I/O 要求が完了しました)、変更するには、各ブロックの読み取りし、が (その「差分領域」とも呼ばれます)、ボリュームのシャドウ コピーの記憶域に書き込まれます。 シャドウ コピーの記憶域は、同じボリュームまたは別のボリュームに配置できます。 変更は、それを上書きする前に、元のボリュームのデータ ブロックのコピーが保持されます。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>時間</th>
<th>ソース データ (状態とデータ)</th>
<th>シャドウ コピー (状態とデータ)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>T0</p></td>
<td><p>元のデータ:1 2 3 4 5</p></td>
<td><p>No copy: —</p></td>
</tr>
<tr class="even">
<td><p>T1</p></td>
<td><p>キャッシュにデータが変更されました。3 ' 3</p></td>
<td><p>シャドウ コピーを作成 (違いのみ):3</p></td>
</tr>
<tr class="odd">
<td><p>T2</p></td>
<td><p>元のデータが上書きされます。1 2 3’ 4 5</p></td>
<td><p>相違点とシャドウ コピーに格納されているインデックス:3</p></td>
</tr>
</tbody>
</table>

**表 1.**    シャドウ コピーを作成するコピー オン ライト メソッド

コピー オン ライト メソッドが変更されたデータのみをコピーするためのシャドウ コピーを作成するためのクイック方法です。 差分領域で、コピーした要素は、前に、変更のいずれかの状態にボリュームを復元する元のボリュームに変更されたデータと組み合わせることができます。 多くの変更がある場合は、コピー オン ライト メソッドは高価になります。

### <a name="redirect-on-write-method"></a>書き込み時のリダイレクト メソッド

書き込み時のリダイレクトの方法では、元のボリュームが変更 (書き込み I/O 要求) を受け取るたびに、変更は、元のボリュームに適用されません。 代わりに、変更は、別のボリュームのシャドウ コピー記憶域に書き込まれます。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>時間</th>
<th>ソース データ (状態とデータ)</th>
<th>シャドウ コピー (状態とデータ)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>T0</p></td>
<td><p>元のデータ:1 2 3 4 5</p></td>
<td><p>No copy: —</p></td>
</tr>
<tr class="even">
<td><p>T1</p></td>
<td><p>キャッシュにデータが変更されました。3 ' 3</p></td>
<td><p>シャドウ コピーを作成 (違いのみ):3’</p></td>
</tr>
<tr class="odd">
<td><p>T2</p></td>
<td><p>元のデータは変更しません。1 2 3 4 5</p></td>
<td><p>相違点とシャドウ コピーに格納されているインデックス:3’</p></td>
</tr>
</tbody>
</table>

**表 2.**    シャドウ コピーの作成の書き込み時のリダイレクト メソッド

データへの変更のみをコピーするため、コピー オン ライトのメソッドと同様は、書き込み時のリダイレクト メソッドは、シャドウ コピーを作成するためクイック メソッドです。 差分領域で、コピーした要素は、データの最新の完全なコピーを作成する元のボリュームに変更されていないデータと組み合わせることができます。 多くの読み取り I/O 要求がある場合は、書き込み時のリダイレクト メソッドは高価になります。

## <a name="shadow-copy-providers"></a>シャドウ コピー プロバイダー

シャドウ コピー プロバイダーの 2 種類があります: ハードウェア ベースのプロバイダー、およびソフトウェア ベースのプロバイダー。 Windows オペレーティング システムに組み込まれているソフトウェア プロバイダーは、システムのプロバイダーもあります。

### <a name="hardware-based-providers"></a>ハードウェア ベースのプロバイダー

ハードウェア ベースのシャドウ コピーは、ボリューム シャドウ コピー サービスと記憶域のハードウェア アダプターまたはコント ローラーとの連携作業によって、ハードウェア レベル間のインターフェイスとしての機能をプロバイダー。 作成とシャドウ コピーを保守作業は、記憶域配列によって実行されます。

ハードウェア プロバイダーは常に、LUN 全体のシャドウ コピーを受け取りますが、ボリューム シャドウ コピー サービスでは、要求されたボリュームのボリュームのシャドウ コピーのみを公開します。

ハードウェア ベースのシャドウ コピー プロバイダーは、ボリューム シャドウ コピー サービスの利用時間で、ポイントを定義する機能のデータを同期できるように、シャドウ コピーを管理、およびバックアップ アプリケーションで共通のインターフェイスを提供します。 ただし、ボリューム シャドウ コピー サービスは、ハードウェア ベースのプロバイダーが生成され、シャドウ コピーを保持する、基になるメカニズムを指定しません。

### <a name="software-based-providers"></a>ソフトウェア ベースのプロバイダー

ソフトウェア ベースのシャドウ コピー プロバイダー通常インターセプトとプロセス読み取りおよび書き込みの I/O 要求のファイル システムと、ボリューム マネージャー ソフトウェアのソフトウェア レイヤーに。

これらのプロバイダーは、少なくとも 1 つのカーネル モード デバイス ドライバー、記憶域フィルター ドライバーでは通常、ユーザー モード DLL コンポーネントとして実装されます。 ハードウェア ベースのプロバイダーとは異なり、ソフトウェア ベースのプロバイダーは、ハードウェア レベルではなく、ソフトウェア レベルでシャドウ コピーを作成します。

ソフトウェア ベースのシャドウ コピー プロバイダーでは、シャドウ コピーの作成時の前に、ボリュームの状態を再作成に使用できるデータ セットにアクセスすることで、ボリュームの「ポイント イン タイム」ビューを維持する必要があります。 例は、システム プロバイダーのコピー オン ライト手法です。 ただし、ボリューム シャドウ コピー サービスはない制限を作成し、シャドウ コピーを保持する、ソフトウェア ベースのプロバイダーを使用して、どのような手法で。

ソフトウェア プロバイダーは、ハードウェア ベースのプロバイダーよりも広範なストレージ プラットフォームに適用され、ベーシック ディスク/論理ボリュームと共にも同様に適切に動作する必要があります。 (論理ボリュームとは、2 つ以上のディスクの空き領域を組み合わせることによって作成されるボリュームです)。ハードウェアのシャドウ コピーとは異なりは、ソフトウェア プロバイダーは、シャドウ コピーを維持するためにオペレーティング システムのリソースを消費します。

ベーシック ディスクの詳細については、次を参照してください[ベーシック ディスクとボリュームには何ですか?。](http://go.microsoft.com/fwlink/?linkid=180894) (http://go.microsoft.com/fwlink/?LinkId=180894) technet。

### <a name="system-provider"></a>システム プロバイダー

シャドウ コピー プロバイダー、1 つのシステム プロバイダーは、Windows オペレーティング システムで提供されます。 既定のプロバイダーは、Windows で指定したその他のベンダーは自由に、記憶域のハードウェアとソフトウェア アプリケーション用に最適化された実装を提供します。

シャドウ コピーに含まれているボリュームの「ポイント イン タイム」ビューを維持するには、システム プロバイダーは、コピー オン ライト手法を使用します。 ボリューム上のシャドウ コピーの作成の開始以降に変更されたブロックのコピーは、シャドウ コピーの記憶域に格納されます。

システム プロバイダーに書き込まれ、通常から読み取ることができますが、実稼働ボリュームを公開できます。 シャドウ コピーが必要なときに論理的に、完全なシャドウ コピーを公開する実稼働ボリュームにデータとの違いを適用します。

システム プロバイダーの NTFS ボリュームのシャドウ コピーの記憶域があります。 シャドウ コピー ボリュームが NTFS ボリュームにする必要はありませんが、システムにマウントされた少なくとも 1 つのボリュームは NTFS ボリュームである必要があります。

コンポーネントのファイル システム プロバイダーを構成するには、swprv.dll および volsnap.sys です。

### <a name="in-box-vss-writers"></a>ボックスの VSS ライター

Windows オペレーティング システムには、さまざまな Windows 機能で必要とされるデータを列挙する責任を持っている VSS ライターのセットが含まれています。

これらのライターの詳細については、次の Microsoft Web サイトを参照してください。

  - [ボックスの VSS ライター](http://go.microsoft.com/fwlink/?linkid=180895) (http://go.microsoft.com/fwlink/?LinkId=180895)  
      
  - [Windows Server 2008 および Windows Vista SP1 の新しいインボックス VSS ライター](http://go.microsoft.com/fwlink/?linkid=180896) (http://go.microsoft.com/fwlink/?LinkId=180896)  
      
  - [Windows Server 2008 R2 および Windows 7 の新しいボックスで VSS ライター](http://go.microsoft.com/fwlink/?linkid=180897) (http://go.microsoft.com/fwlink/?LinkId=180897)  
      

## <a name="how-shadow-copies-are-used"></a>シャドウ コピーの使用方法

アプリケーション データとシステム状態の情報のバックアップに加えて、さまざまな目的で、次のようにシャドウ コピーを使用できます。

  - Lun (LUN の再同期し、LUN のスワップ) を復元します。  
      
  - 個々 のファイル (共有フォルダーのシャドウ コピー) を復元します。  
      
  - 移動可能なシャドウ コピーを使用してデータ マイニング  
      

### <a name="restoring-luns-lun-resynchronization-and-lun-swapping"></a>Lun (LUN の再同期し、LUN のスワップ) を復元します。

Windows Server 2008 R2 および Windows 7 では、VSS の依頼者は、LUN の再同期 (または「再同期の LUN」) と呼ばれるハードウェア シャドウ コピー プロバイダー機能を使用できます。 これは、アプリケーション管理者が元の LUN にまたは新しい LUN は、シャドウ コピーからデータを復元できるようにする高速回復スキームです。

シャドウ コピーには、完全な複製をまたは差分のシャドウ コピーを指定できます。 どちらの場合、再同期操作の最後には、LUN のシャドウ コピーと同じ内容がターゲット LUN になります。 再同期操作中には、配列は、シャドウ コピーからターゲット LUN にブロック レベルのコピーを実行します。


> [!NOTE]
> シャドウ コピーは、ハードウェアの移動可能なシャドウ コピーである必要があります。 
<br>


ほとんどの配列では、運用環境の I/O 操作を再同期操作の開始後すぐに再開を許可します。 再同期操作の進行中は、読み取り要求は、シャドウ コピーの LUN にリダイレクトし、ターゲット LUN に書き込み要求。 これには、非常に大きなデータ セットを回復し、数秒で通常の操作を再開して配列が使用できます。

LUN の再同期は、LUN のスワップと異なります。 LUN のスワップは、Windows Server 2003 SP1 以降で VSS がサポートする高速復旧シナリオです。 LUN スワップでは、シャドウ コピーはインポートされ、読み取り/書き込みボリュームに変換します。 変換は、元に戻せない操作であり、ボリューム、基になる LUN はその後の VSS Api を使用した制御できません。 次の一覧では、LUN の再同期が LUN のスワップと比較する方法について説明します。

  - LUN の再同期で、シャドウ コピーは変更されません、ため何度も使用できます。 LUN がスワップでシャドウ コピーできます 1 回だけな復旧。 最も安全性を意識した管理者では、これは重要です。 LUN の再同期を使用する場合、依頼者は、初めてが生じた場合、全体の復元操作を再試行できます。  
      
  - LUN スワップの末尾には、LUN のシャドウ コピーは、運用環境の I/O 要求に使用されます。 このため、LUN のシャドウ コピーする必要があります同じ記憶域の品質として使用元の運用環境の LUN 回復操作の完了後、パフォーマンスが影響を受けないことを確認します。 LUN の再同期を代わりに使用する場合、ハードウェア プロバイダーが実稼働品質のストレージよりも低コスト ストレージ上のシャドウ コピーを維持できます。  
      
  - 場合、変換先 LUN は使用できません再作成する必要があります、LUN のスワップあります方が経済的ターゲット LUN をする必要がないためです。  
      


> [!WARNING]
> すべての操作を一覧表示は、LUN レベルの操作です。 LUN の再同期を使用して、特定のボリュームを回復しようとした場合、LUN を共有する他のすべてのボリュームを元に戻すには無意識こと。 
<br>


### <a name="restoring-individual-files-shadow-copies-for-shared-folders"></a>個々 のファイル (共有フォルダーのシャドウ コピー) を復元します。

共有フォルダーのシャドウ コピーは、ボリューム シャドウ コピー サービスを使用して、ファイル サーバーなどの共有ネットワーク リソースで配置されているファイルの特定時点のコピーを提供します。 共有フォルダーのシャドウ コピーとに、ユーザーは、ネットワークに格納されているファイルを削除または変更されたにすばやく回復できます。 管理者の支援なしすればできます、ため、共有フォルダーのシャドウ コピーは生産性の向上し、管理コストを削減できます。

共有フォルダーのシャドウ コピーの詳細については、次を参照してください。[共有フォルダーのシャドウ コピー](http://go.microsoft.com/fwlink/?linkid=180898) (http://go.microsoft.com/fwlink/?LinkId=180898) technet。

### <a name="data-mining-by-using-transportable-shadow-copies"></a>移動可能なシャドウ コピーを使用してデータ マイニング

ボリューム シャドウ コピー サービスで使用するために設計されていますが、ハードウェア プロバイダーが同じサブシステム (たとえば、SAN) 内のサーバーにインポートできる移植可能なシャドウ コピーを作成できます。 これらのシャドウ コピーは、実稼働のシードまたはデータ マイニング用の読み取り専用のデータを使用してインストールをテスト使用できます。

1 つのサーバーでは、ソースのデータ ボリュームのシャドウ コピーを作成し、シャドウ コピーを別のサーバーにインポートすることは、ボリューム シャドウ コピー サービスと、ボリューム シャドウ コピー サービスで使用するために設計されたハードウェア プロバイダーでの記憶域配列では、 (または同じサーバーに戻す)。 このプロセスは、データのサイズに関係なく、少し後で実施されます。 トランスポートのプロセスは、一連の移動可能なシャドウ コピーをサポートする、シャドウ コピー リクエスター (記憶域管理アプリケーション) を使用して、ステップによって実行されます。

## <a name="to-transport-a-shadow-copy"></a>シャドウ コピーを転送するには

1.  サーバーで、ソース データの移動可能なシャドウ コピーを作成します。

2.  シャドウ コピーを SAN に接続されているサーバーにインポートする (別のサーバーまたは同じサーバーにインポートすることができます)。

3.  データは、使用する準備ができました。

![](media/volume-shadow-copy-service/Ee923636.633752e0-92f6-49a7-9348-f451b1dc0ed7(WS.10).jpg)

**図 3**   シャドウ コピーの作成と 2 つのサーバー間のトランスポート


> [!NOTE]
> Windows Server 2008 を実行しているサーバーまたは Windows Server 2008 R2 には、Windows Server 2003 で作成される移動可能なシャドウ コピーをインポートできません。 Windows Server 2008 または Windows Server 2008 R2 で作成された移植可能なシャドウ コピーは、Windows Server 2003 を実行しているサーバーにインポートできません。 ただし、Windows Server 2008 上に作成されたシャドウ コピーは、Windows Server 2008 R2、またはその逆を実行しているサーバーにインポートできます。 
<br>


シャドウ コピーは読み取り専用です。 シャドウ コピーを読み取り/書き込みが可能な LUN に変換する場合は、ボリューム シャドウ コピー サービスだけでなく仮想ディスク サービス ベースの記憶域管理アプリケーション (一部の依頼者を含む) を使用できます。 このアプリケーションを使用すると、シャドウ コピー ボリューム シャドウ コピー サービスの管理から削除し、読み取り/書き込みが可能な LUN に変換できます。

ボリューム シャドウ コピー サービスのトランスポートは、Windows Server 2003 Enterprise Edition、Windows Server 2003 Datacenter Edition、Windows Server 2008、または Windows Server 2008 R2 を実行するコンピューターで高度なソリューションです。 記憶域配列にハードウェア プロバイダーがある場合にのみ機能します。 さまざまな目的で、テープ バックアップ、データ マイニング、およびテストを含む、シャドウ コピーのトランスポートを使用できます。

## <a name="frequently-asked-questions"></a>よく寄せられる質問

この FAQ は、システム管理者のボリューム シャドウ コピー サービス (VSS) についての質問に回答します。 VSS アプリケーション プログラミング インターフェイスについては、次を参照してください。[ボリューム シャドウ コピー サービス](http://go.microsoft.com/fwlink/?linkid=180899)(http://go.microsoft.com/fwlink/?LinkId=180899) Windows Developer Center のライブラリでします。

### <a name="when-was-volume-shadow-copy-service-introduced-on-which-windows-operating-system-versions-is-it-available"></a>ボリューム シャドウ コピー サービスが導入されたとき どの Windows オペレーティング システムのバージョンでは使用可能なでしょうか。

VSS は、Windows XP で導入されました。 Windows XP、Windows Server 2003、Windows Vista®、Windows Server 2008、Windows 7、および Windows Server 2008 R2 で使用可能になります。

### <a name="what-is-the-difference-between-a-shadow-copy-and-a-backup"></a>シャドウ コピーとバックアップの違いは何ですか。

ハード ディスク ドライブ バックアップの場合は、作成されたシャドウ コピーと、バックアップではも。 復元のシャドウ コピーをデータをコピーできますまたはシャドウ コピーを高速復旧シナリオに使用できる-たとえば、LUN の再同期または LUN をスワップします。

データは、シャドウ コピーからテープまたはその他のリムーバブル メディアにコピーが、メディアに格納されているコンテンツは、バックアップを構成します。 そこからデータをコピーした後、シャドウ コピー自体を削除できます。

### <a name="what-is-the-largest-size-volume-that-volume-shadow-copy-service-supports"></a>ボリューム シャドウ コピー サービスをサポートする最大サイズのボリュームとは何ですか。

ボリューム シャドウ コピー サービスは、最大 64 TB のボリュームのサイズをサポートします。

### <a name="i-made-a-backup-on-windows-server2008-can-i-restore-it-on-windows-server2008r2"></a>Windows Server 2008 でバックアップを行いました。 復元できますが Windows Server 2008 R2 のでしょうか。

使用しているバックアップ ソフトウェアによって異なります。 ほとんどのバックアップ プログラムは、データ、システム状態のバックアップではなく、このシナリオをサポートします。

これらのバージョンの Windows のいずれかで作成されたシャドウ コピーは、他で使用できます。

### <a name="i-made-a-backup-on-windows-server2003-can-i-restore-it-on-windows-server2008"></a>Windows Server 2003 のバックアップを行いました。 復元できますが Windows Server 2008 のでしょうか。

使用して、バックアップ ソフトウェアによって異なります。 Windows Server 2003 のシャドウ コピーを作成する場合は、Windows Server 2008 で使用することはできません。 また、Windows Server 2008 でシャドウ コピーを作成する場合は、Windows Server 2003 で復元できません。

### <a name="how-can-i-disable-vss"></a>VSS を無効にする方法は?

Microsoft 管理コンソールを使用して、ボリューム シャドウ コピー サービスを無効にすることになります。 ただし、これを行う必要があります。 VSS を悪影響を無効にすると、使用するシステムの復元、および Windows Server バックアップなど、依存するソフトウェアに影響します。

詳細については、次の Microsoft TechNet Web サイトを参照してください。

  - [システムの復元](http://go.microsoft.com/fwlink/?linkid=157113)(http://go.microsoft.com/fwlink/?LinkID=157113)  
      
  - [Windows Server バックアップ](http://go.microsoft.com/fwlink/?linkid=180891)(http://go.microsoft.com/fwlink/?LinkID=180891)  
      

### <a name="can-i-exclude-files-from-a-shadow-copy-to-save-space"></a>領域を節約するシャドウ コピーからファイルを除外することができますですか。

VSS はボリューム全体のシャドウ コピーを作成する設計されています。 ページング ファイルなどの一時ファイルは、領域を節約するシャドウ コピーから自動的に省略されます。

シャドウ コピーから、特定のファイルを除外するには、次のレジストリ キーを使用します。**FilesNotToSnapshot**します。


> [!NOTE]
> <STRONG>FilesNotToSnapshot</STRONG>レジストリ キーは、アプリケーションでのみ使用するためのものです。 これを使用しようとするユーザーには、次の制限事項が発生します。
> <br>
> <UL>
> <LI>Windows Server の以前のバージョンの機能を使用して作成されたシャドウ コピーからファイルを削除できません。<BR><BR>
> <LI>共有フォルダーのシャドウ コピーからファイルを削除できません。<BR><BR>
> <LI>使用して作成されたシャドウ コピーからファイルを削除できますが、 <a href="https://docs.microsoft.com/windows-server/administration/windows-commands/diskshadow" data-raw-source="[Diskshadow](https://docs.microsoft.com/windows-server/administration/windows-commands/diskshadow)">Diskshadow</a>ユーティリティを使用して作成されたシャドウ コピーからファイルを削除できません、 <a href="https://docs.microsoft.com/windows-server/administration/windows-commands/vssadmin" data-raw-source="[Vssadmin](https://docs.microsoft.com/windows-server/administration/windows-commands/vssadmin)">Vssadmin</a>ユーティリティ。<BR><BR>
> <LI>ベスト エフォートでシャドウ コピーからファイルが削除されます。 つまり、削除するのには保証されません。<BR><BR></LI></UL>


詳細については、次を参照してください。[シャドウ コピーからファイルの除外](http://go.microsoft.com/fwlink/?linkid=180904)(http://go.microsoft.com/fwlink/?LinkId=180904) msdn です。

### <a name="my-non-microsoft-backup-program-failed-with-a-vss-error-what-can-i-do"></a>自分の Microsoft 以外のバックアップ プログラムは、VSS のエラーで失敗しました。 どうすればいいんでしょうか。

バックアップ プログラムを作成した会社の Web サイトの製品のサポート セクションを確認します。 製品の更新プログラムをダウンロードしてインストール、問題を解決する可能性があります。 それ以外の場合は、会社の製品のサポート部門にお問い合わせください。

システム管理者は、Microsoft TechNet ライブラリ Web サイトに、VSS のトラブルシューティング情報を使用して、VSS 関連の問題に関する診断情報を収集します。

詳細については、次を参照してください。[ボリューム シャドウ コピー サービス](http://go.microsoft.com/fwlink/?linkid=180905)(http://go.microsoft.com/fwlink/?LinkId=180905) technet。

### <a name="what-is-the-diff-area"></a>「差分領域」とは何ですか。

シャドウ コピー記憶域 (または「差分領域」) は、システム ソフトウェア プロバイダーによって作成されたシャドウ コピーのデータが格納されている場所です。

### <a name="where-is-the-diff-area-located"></a>差分領域の場所

差分領域は、すべてのローカル ボリューム上に配置できます。 ただしを保存するための十分な領域を持つ NTFS ボリューム上に配置する必要があります。

### <a name="how-is-the-diff-area-location-determined"></a>決定差分領域の場所ですか。

次の条件は、差分領域の場所を特定するこの順序で評価されます。

  - ボリュームは、既存のシャドウ コピーを既に持っている場合は、その場所が使用されます。  
      
  - 元のボリュームおよびシャドウ コピー ボリュームの場所の間で手動構成済みの関連付けがある場合は、その場所が使用されます。  
      
  - 前の 2 つの条件は、場所を指定しない場合、シャドウ コピー サービスは使用可能な空き領域に基づく場所を選択します。 1 つ以上のボリュームでシャドウ コピーがある場合、シャドウ コピー サービスは、降順での空き領域のサイズに基づいて、可能なスナップショットの場所の一覧を作成します。 指定された場所の数はボリューム シャドウ コピーされている数です。  
      
  - シャドウ コピーされているボリュームが使用可能な場所のいずれかの場合は、ローカルの関連付けが作成されます。 それ以外の場合、最も空き領域があるボリュームの関連付けが作成されます。  
      

### <a name="can-vss-create-shadow-copies-of-non-ntfs-volumes"></a>VSS は非 NTFS ボリュームのシャドウ コピーを作成できますか。

[はい]。 ただし、永続的なシャドウ コピーは、NTFS ボリュームに対してのみ作成できます。 さらに、システムにマウントされた少なくとも 1 つのボリュームは NTFS ボリュームにある必要があります。

### <a name="whats-the-maximum-number-of-shadow-copies-i-can-create-at-one-time"></a>一度に 1 つを作成できるシャドウ コピーの最大数は何ですか。

1 つのシャドウ コピー セットでのシャドウ コピー ボリュームの最大数は、64 です。 ないシャドウ コピーの数と同じに注意してください。

### <a name="whats-the-maximum-number-of-software-shadow-copies-created-by-the-system-provider-that-i-can-maintain-for-a-volume"></a>ボリュームを維持したシステム プロバイダーによってはソフトウェア シャドウ コピーの最大数は何を作成しますか。

最大数は、512 の各ボリュームには、ソフトウェア シャドウ コピーのです。 ただし、既定では、共有フォルダーのシャドウ コピー機能で使用される 64 のシャドウ コピーをのみ管理できます。 共有フォルダーのシャドウ コピー機能の制限を変更するには、次のレジストリ キーを使用します。**MaxShadowCopies**します。

### <a name="how-can-i-control-the-space-that-is-used-for-shadow-copy-storage-space"></a>シャドウ コピー記憶域スペースの使用されている領域を制御する方法は?

型、 **vssadmin shadowstorage のサイズを変更**コマンド。

詳細については、次を参照してください。 [Vssadmin shadowstorage のサイズを変更](http://go.microsoft.com/fwlink/?linkid=180906)(http://go.microsoft.com/fwlink/?LinkId=180906) technet。

### <a name="what-happens-when-i-run-out-of-space"></a>領域が不足すると起こりますか。

以降では、最も古いシャドウ コピー ボリュームのシャドウ コピーが削除されます。

## <a name="volume-shadow-copy-service-tools"></a>ボリューム シャドウ コピー サービス ツール

Windows オペレーティング システムには、VSS を使用するための次のツールが用意されています。

  - [DiskShadow](http://go.microsoft.com/fwlink/?linkid=180907) (http://go.microsoft.com/fwlink/?LinkId=180907)  
      
  - [VssAdmin](http://go.microsoft.com/fwlink/?linkid=84008) (http://go.microsoft.com/fwlink/?LinkId=84008)  
      

### <a name="diskshadow"></a>DiskShadow

DiskShadow では、ハードウェアとソフトウェア スナップショットをすべて、システム上にあることを管理するのに使用できる VSS リクエスターです。 DiskShadow には、次のコマンドが含まれています。

  - **リスト**:VSS ライター、VSS プロバイダー、およびシャドウ コピーを一覧表示します。  
      
  - **作成**:新しいシャドウ コピーを作成します。  
      
  - **インポート**:移動可能なシャドウ コピーをインポートします。  
      
  - **公開**:(たとえばのドライブ文字) として永続的なシャドウ コピーを公開します。  
      
  - **元に戻す**:指定したシャドウ コピーにボリュームを元に戻します。  
      

このツールは、IT 担当者が使用するためものですが、開発者もこれに役に立つ VSS ライターまたは VSS プロバイダーをテストするときに。

DiskShadow は Windows Server オペレーティング システムでのみ使用できます。 Windows クライアント オペレーティング システムでご利用いただけません。

### <a name="vssadmin"></a>VssAdmin

VssAdmin は、作成、削除、およびシャドウ コピーに関する情報を一覧に使用されます。 シャドウ コピー記憶域 (「差分領域」) のサイズを変更することにも使用できます。

VssAdmin には、次のコマンドが含まれています。

  - **シャドウを付ける**:新しいシャドウ コピーを作成します。  
      
  - **影の削除**:シャドウ コピーを削除します  
      
  - **プロバイダーの一覧表示**:登録されているすべての VSS プロバイダーを一覧表示されます。  
      
  - **list**:サブスクライブして VSS ライターをすべて一覧表示します  
      
  - **shadowstorage のサイズを変更**:シャドウ コピーの記憶域の最大サイズを変更します。  
      

VssAdmin は、システム ソフトウェア プロバイダーによって作成されたシャドウ コピーを管理する場合にのみ使用できます。

VssAdmin は Windows クライアントおよび Windows Server オペレーティング システムのバージョンで利用できます。

## <a name="volume-shadow-copy-service-registry-keys"></a>ボリューム シャドウ コピー サービスのレジストリ キー

次のレジストリ キーは、VSS で使用できます。

  - **VssAccessControl**  
      
  - **MaxShadowCopies**  
      
  - **MinDiffAreaFileSize**  
      

### <a name="vssaccesscontrol"></a>VssAccessControl

このキーは、シャドウ コピーへのアクセスを持つユーザーを指定に使用されます。

詳細については、MSDN Web サイトで、次のエントリを参照してください。

  - [作成者のセキュリティに関する考慮事項](http://go.microsoft.com/fwlink/?linkid=157739)(http://go.microsoft.com/fwlink/?LinkId=157739)  
      
  - [要求者のセキュリティに関する考慮事項](http://go.microsoft.com/fwlink/?linkid=180908)(http://go.microsoft.com/fwlink/?LinkId=180908)  
      

### <a name="maxshadowcopies"></a>MaxShadowCopies

このキーは、コンピューターの各ボリュームに格納できるクライアントからアクセス可能なシャドウ コピーの最大数を指定します。 クライアントがアクセスできるシャドウ コピーは、共有フォルダーのシャドウ コピーによって使用されます。

詳細については、MSDN Web サイトで、次のエントリを参照してください。

**MaxShadowCopies** [レジストリ キーのバックアップと復元の](http://go.microsoft.com/fwlink/?linkid=180909)(http://go.microsoft.com/fwlink/?LinkId=180909)

### <a name="mindiffareafilesize"></a>MinDiffAreaFileSize

このキーは、mb、シャドウ コピーの記憶域の最小の初期サイズを指定します。

詳細については、MSDN Web サイトで、次のエントリを参照してください。

**MinDiffAreaFileSize** [レジストリ キーのバックアップと復元の](http://go.microsoft.com/fwlink/?linkid=180910)(http://go.microsoft.com/fwlink/?LinkId=180910)

`##`#' オペレーティング システムのバージョンのサポート

次の表は、VSS 機能のサポートされているオペレーティング システムの最小バージョンを一覧表示します。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>VSS 機能</th>
<th>サポートされている最小のクライアント</th>
<th>サポートされている最小のサーバー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>LUN の再同期</p></td>
<td><p>サポートなし</p></td>
<td><p>Windows Server 2008 R2</p></td>
</tr>
<tr class="even">
<td><p><strong>FilesNotToSnapshot</strong>レジストリ キー</p></td>
<td><p>Windows Vista</p></td>
<td><p>Windows Server 2008</p></td>
</tr>
<tr class="odd">
<td><p>移動可能なシャドウ コピー</p></td>
<td><p>サポートなし</p></td>
<td><p>Windows Server 2003 SP1</p></td>
</tr>
<tr class="even">
<td><p>ハードウェアのシャドウ コピー</p></td>
<td><p>サポートなし</p></td>
<td><p>Windows Server 2003</p></td>
</tr>
<tr class="odd">
<td><p>Windows Server の以前のバージョン</p></td>
<td><p>Windows Vista</p></td>
<td><p>Windows Server 2003</p></td>
</tr>
<tr class="even">
<td><p>LUN のスワップを使用して高速復旧</p></td>
<td><p>サポートなし</p></td>
<td><p>Windows Server 2003 SP1</p></td>
</tr>
<tr class="odd">
<td><p>ハードウェアのシャドウ コピーの複数をインポートします。</p>
<div class="alert">
<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="media/volume-shadow-copy-service/Dd560667.note(WS.10).gif" />注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>これは、シャドウ コピーを複数回インポートする機能です。 一度に 1 つだけインポート操作を実行できます。
<p></p></td>
</tr>
</tbody>
</table>
<p></p>
</div></td>
<td><p>サポートなし</p></td>
<td><p>Windows Server 2008</p></td>
</tr>
<tr class="even">
<td><p>共有フォルダーのシャドウ コピー</p></td>
<td><p>サポートなし</p></td>
<td><p>Windows Server 2003</p></td>
</tr>
<tr class="odd">
<td><p>移動可能な自動回復のシャドウ コピー</p></td>
<td><p>サポートなし</p></td>
<td><p>Windows Server 2008</p></td>
</tr>
<tr class="even">
<td><p>同時のバックアップ セッション (最大 64)</p></td>
<td><p>Windows XP</p></td>
<td><p>Windows Server 2003</p></td>
</tr>
<tr class="odd">
<td><p>単一の復元セッションと同時にバックアップ</p></td>
<td><p>Windows Vista</p></td>
<td><p>Windows Server 2003 SP2</p></td>
</tr>
<tr class="even">
<td><p>バックアップと同時実行最大 8 個の復元のセッション</p></td>
<td><p>Windows 7</p></td>
<td><p>Windows Server 2003 R2</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目

[Windows デベロッパー センターでボリューム シャドウ コピー サービス](https://docs.microsoft.com/windows/desktop/vss/volume-shadow-copy-service-overview)