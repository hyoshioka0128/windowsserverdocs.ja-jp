---
ms.assetid: 01c8cece-66ce-4a83-a81e-aa6cc98e51fc
title: "高度なデータ重複除去の設定"
ms.prod: windows-server-threshold
ms.technology: storage-deduplication
ms.topic: article
author: wmgries
manager: klaasl
ms.author: wgries
ms.date: 09/15/2016
ms.openlocfilehash: 15cfc054810a2cab85aae9a04d6195c3ae6fe0b9
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="advanced-data-deduplication-settings"></a>高度なデータ重複除去の設定

> 適用対象: Windows Server (半期チャネル)、Windows Server 2016

このドキュメントでは、高度な[データ重複除去](overview.md)の設定を変更する方法について説明します。 [推奨されるワークロード](install-enable.md#enable-dedup-candidate-workloads)については、既定の設定で十分です。 これらの設定を変更する主な理由は、その他の種類のワークロードでのデータ重複除去のパフォーマンス向上です。

## <a id="modifying-job-schedules"></a>データ重複除去ジョブ スケジュールの変更
[既定のデータ重複除去ジョブ スケジュール](understand.md#job-info)は、([**バックアップ**使用法の種類](understand.md#usage-type-backup)に対して有効な*優先順位最適化*ジョブを除いて) 推奨されるワークロードで適切に動作し、可能な限り悪影響を及ぼさないように設計されています。 ワークロードには、サイズの大きいリソース要件がある場合、ジョブがアイドル状態の時間内にのみ実行されるようにしたり、データ重複除去ジョブが使用できるシステム リソースの量を増減したりできます。

### <a id="modifying-job-schedules-change-schedule"></a>データ重複除去のスケジュールの変更
データ重複除去ジョブは、Windows タスク スケジューラを使用してスケジュールされ、パス Microsoft\Windows\Deduplication で表示および編集できます。 データ重複除去には、スケジュールを簡単にするいくつかのコマンドレットが含まれます。
* [`Get-DedupSchedule`](https://technet.microsoft.com/library/hh848446.aspx) は現在スケジュールされているジョブを表示します。
* [`New-DedupSchedule`](https://technet.microsoft.com/library/hh848445.aspx) は新しくスケジュールされたジョブを作成します。
* [`Set-DedupSchedule`](https://technet.microsoft.com/library/hh848447.aspx) は既存のスケジュールされたジョブを変更します。
* [`Remove-DedupSchedule`](https://technet.microsoft.com/library/hh848451.aspx) はスケジュールされたジョブを削除します。

データ重複除去ジョブを実行する時間を変更する最も一般的な理由は、ジョブが業務時間外に実行されるようにするためです。 次の手順の例は、週末と平日の午後 7:00 にアイドル状態となるハイパーコンバージド Hyper-V ホストの、*晴れた日*のシナリオでデータ重複除去スケジュールを変更する方法を示しています。 スケジュールを変更するには、管理者コンテキストで次の PowerShell コマンドレットを実行します。

1. スケジュールされた時間単位の[最適化](understand.md#job-info-optimization)ジョブを無効にします。  
    ```PowerShell
    Set-DedupSchedule -Name BackgroundOptimization -Enabled $false
    Set-DedupSchedule -Name PriorityOptimization -Enabled $false
    ```

2. 現在スケジュールされている[ガベージ コレクション](understand.md#job-info-gc)ジョブおよび[整合性スクラブ](understand.md#job-info-scrubbing)ジョブを削除します。
    ```PowerShell
    Get-DedupSchedule -Type GarbageCollection | ForEach-Object { Remove-DedupSchedule -InputObject $_ }
    Get-DedupSchedule -Type Scrubbing | ForEach-Object { Remove-DedupSchedule -InputObject $_ }
    ```

3. 高優先順位で、システム上のすべての CPU と使用可能なメモリを使用して午後 7時 00分に実行される、夜間の最適化ジョブを作成します。
    ```PowerShell
    New-DedupSchedule -Name "NightlyOptimization" -Type Optimization -DurationHours 11 -Memory 100 -Cores 100 -Priority High -Days @(1,2,3,4,5) -Start (Get-Date "2016-08-08 19:00:00")
    ```

    >[!NOTE]  
    > `-Start` に提供される `System.Datetime` の*日付*部分は (過去日付である限り) 使用されませんが、*時間*部分はジョブを開始する時間を指定します。
4. 高優先順位で、システム上のすべての CPU と使用可能なメモリを使用して土曜日の午前 7時 00分に実行される、週単位のガベージ コレクション ジョブを作成します。
    ```PowerShell
    New-DedupSchedule -Name "WeeklyGarbageCollection" -Type GarbageCollection -DurationHours 23 -Memory 100 -Cores 100 -Priority High -Days @(6) -Start (Get-Date "2016-08-13 07:00:00")
    ```

5. 高優先順位で、システム上のすべての CPU と使用可能なメモリを使用して日曜日の午前 7時 00分に実行される、週単位の整合性スクラブ ジョブを作成します。
    ```PowerShell
    New-DedupSchedule -Name "WeeklyIntegrityScrubbing" -Type Scrubbing -DurationHours 23 -Memory 100 -Cores 100 -Priority High -Days @(0) -Start (Get-Date "2016-08-14 07:00:00")
    ```

### <a id="modifying-job-schedules-available-settings"></a>使用可能なジョブ全体の設定
新規またはスケジュールされたデータ重複除去ジョブの、次の設定を切り替えることができます。

<table>
    <thead>
        <tr>
            <th style="min-width:125px">パラメーター名</th>
            <th>定義</th>
            <th>使用可能な値</th>
            <th>この値を設定する理由</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>種類</td>
            <td>スケジュールする必要があるジョブの種類</td>
            <td>
                <ul>
                    <li>最適化</li>
                    <li>ガベージ コレクション</li>
                    <li>スクラブ</li>
                </ul>
            </td>
            <td>この値は、スケジュールされている必要があるジョブの種類であるため、必要です。 タスクをスケジュールした後は、この値を変更できません。</td>
        </tr>
        <tr>
            <td>優先順位</td>
            <td>スケジュールされたジョブのシステム優先順位</td>
            <td>
                <ul>
                    <li>高</li>
                    <li>中間</li>
                    <li>低</li>
                </ul>
            </td>
            <td>この値は、CPU 時間が割り当てられる方法を決定するのに役立ちます。 *[高]* は多くの CPU 時間を使用し、*[低]* は使用する CPU 時間がそれより少なくなります。</td>
        </tr>
        <tr>
            <td>Days</td>
            <td>ジョブがスケジュールされる曜日</td>
            <td>週の曜日を表す 0 ~ 6 の整数の配列。<ul>
                <li>0 = 日曜日</li>
                <li>1 = 月曜日</li>
                <li>2 = 火曜日</li>
                <li>3 = 水曜日</li>
                <li>4 = 木曜日</li>
                <li>5 = 金曜日</li>
                <li>6 = 土曜日</li>
            </ul></td>
            <td>スケジュールされたタスクは、少なくともいずれかの曜日に実行する必要があります。</td>
        </tr>
        <tr>
            <td>Cores</td>
            <td>ジョブが使用するシステム上のコアの割合</td>
            <td>(パーセントを示す) 整数 0 ~ 100</td>
            <td>ジョブがシステム上のコンピューティング リソースに与える影響のレベルを制御するため</td>
        </tr>
        <tr>
            <td>DurationHours</td>
            <td>ジョブの実行が許容される最大時間数。</td>
            <td>正の整数</td>
            <td>ワークロードの非アイドル時間にジョブが実行されるのを阻止するため</td>
        </tr>
        <tr>
            <td>Enabled</td>
            <td>ジョブが実行されるかどうか</td>
            <td>true または false</td>
            <td>ジョブを削除せずに無効にするため</td>
        </tr>
        <tr>
            <td>フル</td>
            <td>フル ガベージ コレクション ジョブのスケジュール</td>
            <td>スイッチ (true または false)</td>
            <td>既定では、4 番目のジョブはすべてガベージ コレクション ジョブです。 このスイッチを使用して、より頻繁に実行されるフル ガベージ コレクションをスケジュールできます。</td>
        </tr>
        <tr>
            <td>InputOutputThrottle</td>
            <td>ジョブに適用される入力/出力の調整の量の指定</td>
            <td>(パーセントを示す) 整数 0 ~ 100</td>
            <td>調整により、ジョブが他の I/O 集中型のプロセスに干渉しなくなります。</td>
        </tr>
        <tr>
            <td>メモリ</td>
            <td>ジョブが使用するシステム上のメモリの割合</td>
            <td>(パーセントを示す) 整数 0 ~ 100</td>
            <td>ジョブがシステム上のコンピューティング リソースに与える影響のレベルを制御するため</td>
        </tr>
        <tr>
            <td>名前</td>
            <td>スケジュールされたジョブの名前</td>
            <td>String</td>
            <td>ジョブには一意に識別できる名前が必要であるため。</td>
        </tr>
        <tr>
            <td>ReadOnly</td>
            <td>スクラブ ジョブが検出された破損を処理およびレポートしますが、修復アクションは実行しないことを示します。</td>
            <td>スイッチ (true または false)</td>
            <td>ディスクの不適切なセクションに配置されているファイルを手動で復元する必要があります。</td>
        </tr>
        <tr>
            <td>管理者として</td>
            <td>ジョブを開始する時刻の指定</td>
            <td>`System.DateTime`</td>
            <td>*Start* に提供される `System.Datetime` の*日付*部分は (過去日付である限り) 使用されませんが、*時間*部分はジョブを開始する時間を指定します。</td>
        </tr>
        <tr>
            <td>StopWhenSystemBusy</td>
            <td>システムがビジー状態の場合にデータ重複除去が実行を停止するかどうかの指定</td>
            <td>スイッチ (true または false)</td>
            <td>このスイッチを使用して、データ重複除去の動作を制御することができます。これは、ワークロードがアイドル状態でない場合にデータ重複除去を実行する場合に特に重要です。</td>
        </tr>
    </tbody>
</table>

## <a id="modifying-volume-settings"></a>データ重複除去ボリューム全体の設定の変更
### <a id="modifying-volume-settings-how-to-toggle"></a>ボリュームの設定の切り替え
ボリュームに対して重複除去を有効にするときに選択する[使用法の種類](understand.md#usage-type)から、ボリューム全体についてのデータ重複除去の既定の設定を行うことができます。 データ重複除去には、ボリューム全体の設定を簡単に編集できるようにするコマンドレットが含まれています。

* [`Get-DedupVolume`](https://technet.microsoft.com/library/hh848448.aspx)
* [`Set-DedupVolume`](https://technet.microsoft.com/library/hh848438.aspx)

選択した使用法の種類からボリュームの設定を変更する主な理由は、特定のファイル (既に圧縮されているマルチメディアまたはほかのファイルの種類など) の読み込みのパフォーマンス向上、またはデータ重複除去の微調整による特定のワークロードの最適化です。 次の例は、汎用ファイル サーバーのワークロードに最も類似している一方で、頻繁に変更される大きなファイルを使用するワークロードのデータ重複除去設定を変更する方法を示します。

1. クラスター共有ボリューム 1 の現在のボリュームの設定を確認します。
    ```PowerShell
    Get-DedupVolume -Volume C:\ClusterStorage\Volume1 | Select *
    ```

2. クラスター共有ボリューム 1 の OptimizePartialFiles を有効にして、MinimumFileAge ポリシーが、ファイル全体ではなくファイルのセクションに適用されるようにします。 これにより、ファイルのセクションが定期的に変更されても、ファイルの大部分が最適化されます。
    ```PowerShell
    Set-DedupVolume -Volume C:\ClusterStorage\Volume1 -OptimizePartialFiles
    ```

### <a id="modifying-volume-settings-available-settings"></a>利用可能なボリューム全体の設定
<table>
    <thead>
        <tr>
            <th style="min-width:125px">設定名</th>
            <th>定義</th>
            <th>使用可能な値</th>
            <th>この値を変更する理由</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>ChunkRedundancyThreshold</td>
            <td>チャンクがチャンク ストアのホット スポット セクションに複製される前に参照される回数。 ホット スポット セクションの値は、頻繁に参照され、アクセス時間を向上させるために複数のアクセス パスを持つ、いわゆる "ホット" チャンクの値です。</td>
            <td>正の整数</td>
            <td>この数を変更する主な理由は、重複率の高いボリュームの削減率を上げることです。 一般に、既定値 (100) が推奨設定であり、この値を変更する必要はありません。</td>
        </tr>
        <tr>
            <td>ExcludeFileType</td>
            <td>最適化から除外されるファイルの種類</td>
            <td>ファイル拡張子の配列</td>
            <td>一部のファイルの種類、特にマルチ メディアまたは既に圧縮されているファイルには、最適化はあまり有効ではありません。 この設定では、どの種類を除外するかを構成できます。</td>
        </tr>
        <tr>
            <td>ExcludeFolder</td>
            <td>最適化の対象としないフォルダーのパスの指定</td>
            <td>フォルダーのパスの配列</td>
            <td>パフォーマンスを向上させたり、特定のパスが最適化されないようにしたりする場合は、ボリューム上の特定のパスを最適化の対象から除外できます。</td>
        </tr>
        <tr>
            <td>InputOutputScale</td>
            <td>後処理ジョブ中にボリュームに使用するデータの重複除去の IO の並列化 (IO キュー) のレベルの指定</td>
            <td>1~36 の正の整数</td>
            <td>この値を変更する主な理由は、データ重複除去がボリュームに使用できる IO キューの数を制限して、高い IO ワークロードのパフォーマンスへの影響を軽減することです。 既定からこの設定を変更すると、データ重複除去の後処理ジョブの速度が遅くなることがあります。</td>
        </tr>
        <tr>
            <td>MinimumFileAgeDays</td>
            <td>ファイルが最適化のポリシー内であるとみなされる前にファイルが作成されてから経過した日数</td>
            <td>正の整数 (0 を含む)</td>
            <td>**Default** と **HyperV** 使用法の種類はこの値を 3 に設定して、ホットまたは最近作成されたファイルのパフォーマンスを最大化します。 データ重複除去がより積極的に行われるようにする場合、または重複除去に関連してさらに待機時間が増えるのを避ける場合は、この値を変更しても構いません。</td>
        </tr>
        <tr>
            <td>MinimumFileSize</td>
            <td>ファイルが最適化のポリシー内であるとみなされる必要がある最小ファイル サイズ</td>
            <td>32 KB より大きい正の整数 (バイト) </td>
            <td>この値を変更する主な理由は、最適化の値が限られている可能性のある小さなファイルを除外することによって、コンピューティング時間を節約することです。</td>
        </tr>
        <tr>
            <td>NoCompress</td>
            <td>チャンクがチャンク ストアに移される前に、チャンクを圧縮するかどうか</td>
            <td>true または false</td>
            <td>ある種のファイル、特にマルチ メディア ファイルと既に圧縮済みのファイルの種類は、適切に圧縮されない可能性があります。 この設定では、ボリューム上のすべてのファイルの圧縮をオフにすることができます。 既に圧縮されているファイルが多数含まれるデータセットを最適化しているのが理想です。</td>
        </tr>
        <tr>
            <td>NoCompressionFileType</td>
            <td>チャンクがチャンク ストアに移される前に、チャンクを圧縮しないファイルの種類</td>
            <td>ファイル拡張子の配列</td>
            <td>ある種のファイル、特にマルチ メディア ファイルと既に圧縮済みのファイルの種類は、適切に圧縮されない可能性があります。 この設定では、そのようなファイルの圧縮をオフにして、CPU リソースを節約できます。</td>
        </tr>
        <tr>
            <td>OptimizeInUseFiles</td>
            <td>有効な場合は、最適化のためのポリシーとしてこれらに対してアクティブなハンドルを持つファイルと見なされます。</td>
            <td>true または false</td>
            <td>ワークロードによってファイルが長期間開かれたままとなっている場合、この設定を有効にします。 この設定が有効でない場合、ワークロードに開いているハンドルがある場合は、このハンドルがまれにデータを最後に追加するだけであっても、ファイルが最適化されません。</td>
        </tr>
        <tr>
            <td>OptimizePartialFiles</td>
            <td>有効にすると、ファイル全体ではなく、ファイルのセグメントに MinimumFileAge 値が適用されます。</td>
            <td>true または false</td>
            <td>ワークロードが大容量で頻繁に編集される、内容はほとんどがそのままのファイルを処理する場合は、この設定を有効にします。 この設定が有効でない場合、これらのファイルは常に変更され続けるため、ファイルの内容は最適化される準備ができているにもかかわらず、ファイルが最適化されません。</td>
        </tr>
        <tr>
            <td>検証</td>
            <td>有効にすると、チャンク ストア内に既にあるチャンクがチャンクのハッシュに一致する場合、これらのチャンクが等しいことが、バイトで確認されます。</td>
            <td>true または false</td>
            <td>これは、実際には同一ではないもののハッシュ値が同じである 2 つのデータのチャンクを比較することによって、チャンクを比較するハッシュ アルゴリズムが誤りを起こさないようにする整合性機能です。 実際には、このようなことが起きる可能性は極めて低くなります。 検証機能を有効にすると、最適化ジョブに大きなオーバーヘッドが追加されます。</td>
        </tr>
    </tbody>
</table>

## <a id="modifying-dedup-system-settings"></a>データ重複除去システム全体の設定の変更
データ重複除去には、[レジストリ](https://technet.microsoft.com/library/cc755256(v=ws.11).aspx)から構成できる追加のシステム全体の設定があります。 これらの設定は、システム上で実行されるすべてのジョブとボリュームに適用されます。 レジストリを編集するときは、細心の注意を払ってください。

たとえば、フル ガベージ コレクションを無効にするとします。 これがお使いのシナリオに役立つ理由の詳細は、「[よく寄せられる質問](#faq-why-disable-full-gc)」に記載されています。 PowerShell を使用してレジストリを編集するには、次のとおりコマンドを使用します。

* データ重複除去がクラスターで実行されている場合:
    ```PowerShell
    Set-ItemProperty -Path HKLM:\System\CurrentControlSet\Services\ddpsvc\Settings -Name DeepGCInterval -Type DWord -Value 0xFFFFFFFF
    Set-ItemProperty -Path HKLM:\CLUSTER\Dedup -Name DeepGCInterval -Type DWord -Value 0xFFFFFFFF
    ```

* データ重複除去がクラスターで実行されていない場合:
    ```PowerShell
    Set-ItemProperty -Path HKLM:\System\CurrentControlSet\Services\ddpsvc\Settings -Name DeepGCInterval -Type DWord -Value 0xFFFFFFFF
    ```

### <a id="modifying-dedup-system-settings-available-settings"></a>使用可能なシステム全体の設定
<table>
    <thead>
        <tr>
            <th style="min-width:125px">設定名</th>
            <th>定義</th>
            <th>使用可能な値</th>
            <th>変更する理由</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>WlmMemoryOverPercentThreshold</td>
            <td>この設定により、データ重複除去が実際に利用可能であると判断したよりも多くのメモリをジョブが使用できます。 たとえば設定が 300 の場合、ジョブがキャンセルされるには、ジョブは割り当てられたメモリの 3 倍のメモリを使用する必要があることを意味します。</td>
            <td>正の整数 (300 の値は 300% または 3 倍を意味します)</td>
            <td>データ重複除去でより多くのメモリが使用されると停止する別のタスクがある場合</td>
        </tr>
        <tr>
            <td>DeepGCInterval</td>
            <td>この設定により、通常のガベージ コレクション ジョブが[完全なガベージ コレクション ジョブ](advanced-settings.md#faq-full-v-regular-gc)になる間隔が構成されます。 設定が n の場合、n <sup>回</sup>ごとにジョブがフル ガベージ コレクション ジョブになります。 [バックアップ使用法の種類](understand.md#usage-type-backup)を含むボリュームでは、常にフル ガベージ コレクションが無効になる (レジストリ値に関係なく) 点に注意してください。 `Start-DedupJob -Type GarbageCollection -Full` バックアップ ボリュームにフル ガベージ コレクションが必要な場合に使うことができます。</td>
            <td>整数 (-1 は無効を示します)</td>
            <td>[このよく寄せられる質問](advanced-settings.md#faq-why-disable-full-gc)を参照してください。</td>
        </tr>
    </tbody>
</table>

## <a id="faq"></a>よく寄せられる質問
<a id="faq-use-responsibly"></a>**データ重複除去設定を変更すると、ジョブの速度が低下して終わらないか、ワークロードのパフォーマンスが低下しました。なぜでしょうか?**  
これらの設定では、データ重複除去を制御するのに多くの労力が費やされます。 設定は責任を持って使用し、[パフォーマンスを監視](run.md#monitoring-dedup)してください。

<a id="faq-running-dedup-jobs-manually"></a>**データ重複除去ジョブを今すぐ実行したいのですが、新しいスケジュールを作成すしたくありません。これは可能ですか。**  
はい、[すべてのジョブは手動で実行することができます](run.md#running-dedup-jobs-manually)。

<a id="faq-full-v-regular-gc"></a>**フルと通常のガベージ コレクションの違いはなんですか。**  
[ガベージ コレクション](understand.md#job-info-gc)には、次の 2 つの種類があります。

- *通常のガベージ コレクション*は統計アルゴリズムを使用して、特定の基準 (メモリと IOPS が少ない) に適合する大きな参照されていないチャンクを検索します。 通常のガベージ コレクションでは、チャンクの最小の割合が参照されていない場合にのみ、チャンク格納コンテナーが圧縮されます。 この種類のガベージ コレクションは、フル ガベージ コレクションより実行が速く、使用されるリソースはより少なくなります。 通常のガベージ コレクション ジョブの既定のスケジュールでは、実行は毎週 1 回です。
- *フル ガベージ コレクション*は、参照されていないチャンクをより綿密に検索し、より多くのディスク領域を解放します。 フル ガベージ コレクションでは、コンテナー内の単一のチャンクだけが参照されていない場合でも、すべてのコンテナーが圧縮されます。 フル ガベージ コレクションでは、最適化ジョブ中にクラッシュや電源障害があった場合に使用されていた可能性のある領域も解放されます。 フル ガベージ コレクション ジョブは、通常のガベージ コレクションジョブと比較してより多くの時間とシステム リソースを費やして、重複解除されたボリューム上で回復できる利用可能な領域を 100% 回復します。 フル ガベージ コレクション ジョブは一般的に、通常のガベージ コレクション ジョブより最大 5% 多くの参照されていないデータを検出して解放します。 既定のスケジュールでは、フル ガベージ コレクション ジョブは通常のガベージ コレクションのスケジュールの 4 回目ごとに実行されます。

<a id="faq-why-disable-full-gc"></a>**フル ガベージ コレクションを無効にする場合の利点はなんですか。**  
- ガベージ コレクションは、ボリュームの有効期間のシャドウ コピーと増分バックアップのサイズに悪影響を与える可能性があります。 頻繁に変化する、または I/O 集中型のワークロードは、フル ガベージ コレクション ジョブによってパフォーマンスが低下する可能性があります。           
- システムがクラッシュしたことがわかっている場合は、PowerShell からフル ガベージ コレクション ジョブを手動で実行して、リークをクリーンアップすることができます。
