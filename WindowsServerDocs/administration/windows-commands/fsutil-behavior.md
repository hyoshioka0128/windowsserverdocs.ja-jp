---
title: fsutil behavior
description: NTFS ボリュームの動作を照会または設定する、fsutil behavior コマンドのリファレンス記事です。
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.topic: article
ms.date: 10/16/2017
ms.assetid: 84eaba2c-c0af-49e1-bbbd-2ed2928e5e4b
ms.openlocfilehash: 74a974bcb7f8138d28e563db35bbde7ae689e110
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931837"
---
# <a name="fsutil-behavior"></a>fsutil behavior

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8

次のような NTFS ボリュームの動作を照会または設定します。

- 8.3 文字の長さのファイル名を作成します。

- 文字使用を拡張する、8.3 文字長の短いファイル名を NTFS ボリューム上にします。

- ディレクトリが NTFS ボリュームにリストされている場合の**最後のアクセスタイム**スタンプの更新。

- クォータイベントがシステムログ、NTFS ページプール、および NTFS 非ページプールメモリキャッシュレベルに書き込まれる頻度。

- マスターファイルテーブルゾーン (MFT ゾーン) のサイズ。

- システムで NTFS ボリュームの破損が検出された場合のデータのサイレント削除。

- ファイル削除通知 (トリムまたはアンマップとも呼ばれます)。

## <a name="syntax"></a>構文

```
fsutil behavior query {allowextchar | bugcheckoncorrupt | disable8dot3 [<volumepath>] | disablecompression | disablecompressionlimit | disableencryption | disablefilemetadataoptimization | disablelastaccess | disablespotcorruptionhandling | disabletxf | disablewriteautotiering | encryptpagingfile | mftzone | memoryusage | quotanotify | symlinkevaluation | disabledeletenotify}

fsutil behavior set {allowextchar {1|0} | bugcheckoncorrupt {1|0} | disable8dot3 [ <value> | [<volumepath> {1|0}] ] | disablecompression {1|0} | disablecompressionlimit {1|0} | disableencryption {1|0} | disablefilemetadataoptimization {1|0} | disablelastaccess {1|0} | disablespotcorruptionhandling {1|0} | disabletxf {1|0} | disablewriteautotiering {1|0} | encryptpagingfile {1|0} | mftzone <Value> | memoryusage <Value> | quotanotify <frequency> | symlinkevaluation <symboliclinktype> | disabledeletenotify {1|0}}
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- |------------ |
| query | ファイルシステムの動作パラメーターを照会します。 |
| set | ファイルシステムの動作パラメーターを変更します。 |
| allowextchar`{1|0}` | NTFS ボリューム上の長さが8.3 文字の短いファイル名で、拡張文字セット (発音区別文字を含む) の文字を使用できるようにし**ます (****0**)。<p>このパラメーターを有効にするには、コンピューターを再起動する必要があります。 |
| バグチェッカーが破損しています`{1|0}` | NTFS ボリュームに破損がある場合に、(**1**) または (**0**) バグチェックの生成を許可しません。 この機能を使用すると、自己修復 NTFS 機能で使用したときに、NTFS によってデータが自動的に削除されないようにすることができます。<p>このパラメーターを有効にするには、コンピューターを再起動する必要があります。 |
| disable8dot3 [ <volumepath> ]`{1|0}` | (**1**) を無効にするか、(**0**) FAT 形式のボリュームと NTFS でフォーマットされたボリュームに8.3 文字の長さのファイル名を作成します。 必要に応じて、 *volumepath*をドライブ名として指定し、その後にコロンまたは GUID を指定します。 |
| disablecompression`{1|0}` | ( **1)** を**無効にする**か、NTFS 圧縮を有効にします。<p>このパラメーターを有効にするには、コンピューターを再起動する必要があります。 |
| disablecompresの制限`{1|0}` | NTFS ボリューム**の ntfs 圧縮**制限を無効にします **(1)** 。 圧縮されたファイルがファイルの拡張に失敗するのではなく、特定のレベルの断片化に達した場合、NTFS はファイルのエクステントの追加圧縮を停止します。 これは、圧縮ファイルが通常よりも大きくなることを許可するために行われました。 この値を**TRUE**に設定すると、システム上の圧縮されたファイルのサイズを制限するこの機能が無効になります。 この機能を無効にすることはお勧めしません。<p>このパラメーターを有効にするには、コンピューターを再起動する必要があります。 |
| disableencryption`{1|0}` | NTFS ボリューム上のフォルダーとファイルの暗号化を無効 **(1)** または有効 **(0)** にします。<p>このパラメーターを有効にするには、コンピューターを再起動する必要があります。 |
| disablefilemetadataoptimization`{1|0}` | ( **1)** を無効にするか、 **(0)** ファイルメタデータの最適化を有効にします。 NTFS では、特定のファイルが持つことができるエクステントの数に制限があります。 圧縮ファイルとスパースファイルは非常に断片化される可能性があります。 既定では、NTFS は内部メタデータ構造を定期的に圧縮して、断片化されたファイルを追加できるようにします。 この値を**TRUE**に設定すると、この内部最適化は無効になります。 この機能を無効にすることはお勧めしません。<p>このパラメーターを有効にするには、コンピューターを再起動する必要があります。 |
| disablelastaccess`{1|0}` | ディレクトリが NTFS ボリュームに一覧表示されている場合は、(**1**) または (**0**) 更新を有効にします。<p>このパラメーターを有効にするには、コンピューターを再起動する必要があります。 |
| disablespotcorruptionhandling`{1|0}` | **(1)** を無効にするか、 **(0)** スポット破損処理を有効にします。 また、システム管理者は CHKDSK を実行して、ボリュームをオフラインにすることなくボリュームの状態を分析することもできます。 この機能を無効にすることはお勧めしません。<p>このパラメーターを有効にするには、コンピューターを再起動する必要があります。 |
| disab・ xf`{1|0}` | 指定した NTFS ボリュームで ( **1)** または **(0)** の txf を有効にします。 TxF は、ファイルシステム操作に対するセマンティクスのようなトランザクションを提供する NTFS 機能です。 TxF は現在非推奨とされていますが、この機能は引き続き利用できます。 C: ボリュームではこの機能を無効にしないことをお勧めします。<p>このパラメーターを有効にするには、コンピューターを再起動する必要があります。 |
| disablewriteautotiering`{1|0}` | 階層化ボリュームの ReFS v2 自動階層化ロジックを無効にします。<p>このパラメーターを有効にするには、コンピューターを再起動する必要があります。 |
| encryptpagingfile`{1|0}` | (**1**) を暗号化するか、**0**Windows オペレーティングシステムのメモリページングファイルを暗号化しません。<p>このパラメーターを有効にするには、コンピューターを再起動する必要があります。 |
| mftzone`<value>` | MFT ゾーンのサイズを設定します。これは200MB 単位の倍数として表されます。 *値*を**1** (既定値は 200 mb) から**4** (最大 800 MB) の数値に設定します。<p>このパラメーターを有効にするには、コンピューターを再起動する必要があります。 |
| memoryusage`<value>` | NTFS ページプールメモリおよび NTFS 非ページプールメモリの内部キャッシュレベルを構成します。 を**1**または**2**に設定します。 **1** (既定値) に設定すると、NTFS では既定のサイズのページプールメモリが使用されます。 **2**に設定すると、NTFS によって、ルックアサイドリストとメモリのしきい値のサイズが大きくなります。 (ルックアサイドリストは、カーネルおよびデバイスドライバーがファイルシステム操作 (ファイルの読み取りなど) のためにプライベートメモリキャッシュとして作成する固定サイズのメモリバッファーのプールです。<p>このパラメーターを有効にするには、コンピューターを再起動する必要があります。 |
| quotanotify`<frequency>` | NTFS クォータ違反がシステムログでどの程度の頻度で報告されるかを構成します。 の有効な値は**0 ~ 4294967295**の範囲です。 既定の頻度は**3600**秒 (1 時間) です。<p>このパラメーターを有効にするには、コンピューターを再起動する必要があります。 |
| symlinkevaluation`<symboliclinktype>` | コンピューター上に作成できるシンボリックリンクの種類を制御します。 有効な選択肢は次のとおりです。<ul><li>**1** -ローカルシンボリックリンクに対してローカル`L2L:{0|1}`</li><li>**2** -リモートシンボリックリンクに対してローカル`L2R:{1|0}`</li><li>**3** -リモートからローカルへのシンボリックリンク`R2R:{1|0}`</li><li>**4** -リモートシンボリックリンクへのリモートシンボリックリンク`R2L:{1|0}`</li></ul> |
| disabledeletenotify | (**1**) を無効にするか、(**0**) 削除通知を有効にします。 削除通知 (トリムまたはマップ解除とも呼ばれます) は、ファイルの削除操作によって解放されたクラスターの基になる記憶装置を通知する機能です。 さらに:<ul><li>ReFS v2 を使用するシステムでは、trim は既定で無効になっています。</li><li>ReFS v1 を使用するシステムでは、trim は既定で有効になっています。</li><li>NTFS を使用するシステムでは、管理者が無効にしない限り、既定で trim が有効になります。</li><li>ハードディスクドライブまたは SAN で trim がサポートされていないと報告された場合、ハードディスクドライブと San はトリム通知を受け取りません。</li><li>有効または無効にしても、再起動は必要ありません。</li><li>Trim は、次のマップ解除コマンドが発行されるときに有効になります。</li><li>既存の配信 IO は、レジストリの変更による影響を受けません。</li><li>Trim を有効または無効にしても、サービスの再起動は必要ありません。</li></ul> |

#### <a name="remarks"></a>注釈

- MFT ゾーンは、MFT の断片化を防ぐためにマスターファイルテーブル (MFT) を必要に応じて拡張できるようにするための予約領域です。 ボリューム上のファイルの平均サイズが 2 KB 以下の場合は、 **mftzone**値を**2**に設定すると便利です。 ボリューム上のファイルの平均サイズが 1 KB 以下の場合は、 **mftzone**の値を**4**に設定すると便利です。

- **Disable8dot3**が**0**に設定されている場合、長いファイル名でファイルを作成するたびに、NTFS によって2つ目のファイルエントリが作成され、そのファイルには8.3 文字の長さのファイル名が付けられます。 NTFS でディレクトリにファイルを作成する場合は、長いファイル名に関連付けられている長さが8.3 文字のファイル名を検索する必要があります。 このパラメーターは、 **HKLM\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsDisable8dot3NameCreation**レジストリキーを更新します。

- **Allowextchar**パラメーターを指定すると、 **HKLM\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsAllowExtendedCharacterIn8dot3Name**レジストリキーが更新されます。

- **Disablelastaccess**パラメーターを使用すると、ファイルおよびディレクトリの**最終アクセスタイム**スタンプへのログ更新の影響が軽減されます。 **最終アクセス時刻**機能を無効にすると、ファイルとディレクトリへのアクセス速度が向上します。 このパラメーターは、 **HKLM\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsDisableLastAccessUpdate**レジストリキーを更新します。

    **注:**

    - ディスク上のすべての値が最新でない場合でも、ファイルベースの**最終アクセス時間**のクエリは正確です。 正確な値はメモリに格納されるので、NTFS はクエリの正しい値を返します。

    - 1時間は、NTFS がディスク上の**最終アクセス時刻**の更新を延期できる最長時間です。 NTFS が**最後の変更時刻**などの他のファイル属性を更新し、**最後のアクセス時刻**の更新が保留になっている場合、ntfs は、パフォーマンスに影響を与えることなく、他の更新で**最後のアクセス時刻**を更新します。

    - **Disablelastaccess**パラメータは、この機能に依存するバックアップやリモートストレージなどのプログラムに影響を与える可能性があります。

- 物理メモリを増やすと、常に NTFS で使用できるページプールメモリの量が増加するわけではありません。 **Memoryusage**を**2**に設定すると、ページプールメモリの制限が発生します。 これにより、システムが同じファイルセット内の多数のファイルを開いたり閉じたりしているときに、他のアプリやキャッシュメモリ用に大量のシステムメモリを使用していない場合に、パフォーマンスが向上する可能性があります。 コンピューターで既に他のアプリやキャッシュメモリに大量のシステムメモリを使用している場合は、NTFS ページと非ページプールメモリの制限を引き上げると、他のプロセスで使用可能なプールメモリが減少します。 これにより、システム全体のパフォーマンスが低下する可能性があります。 このパラメーターは、 **HKLM\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsMemoryUsage**レジストリキーを更新します。

- **Mftzone**パラメーターで指定した値は、mft の初期サイズと新しいボリュームの mft ゾーンの概数になり、各ファイルシステムのマウント時に設定されます。 ボリューム上の領域が使用されると、NTFS によって、将来の MFT 拡張用に予約された領域が調整されます。 MFT ゾーンが既に大きい場合、完全な MFT ゾーンサイズは予約されていません。 MFT ゾーンは、MFT の末尾を越えた連続した範囲に基づいているため、領域が使用されると縮小されます。

    現在の MFT ゾーンが完全に使用されるまで、ファイルシステムは新しい MFT ゾーンの場所を判断しません。 これは、一般的なシステムでは発生しないことに注意してください。

- 一部のデバイスでは、削除通知機能が有効になっていると、パフォーマンスの低下が発生する場合があります。 この場合は、 **disabledeletenotify**オプションを使用して通知機能をオフにします。

### <a name="examples"></a>例

GUID で指定されたディスクボリュームの8dot3 名の無効化動作を照会するには、次のように入力します。 {92884 2df-5a01-11e6f6e6963},、次のように入力します。

```
fsutil behavior query disable8dot3 volume{928842df-5a01-11de-a85c-806e6f6e6963}
```

また、 **8dot3name**サブコマンドを使用して、8dot3 名の動作を照会することもできます。

システムに対してクエリを実行し、TRIM が有効かどうかを確認するには、次のように入力します。

```
fsutil behavior query DisableDeleteNotify
```

これにより、次のような出力が生成されます。

```
NTFS DisableDeleteNotify = 1
ReFS DisableDeleteNotify is not currently set
```

ReFS v2 の TRIM (disabledeletenotify) の既定の動作をオーバーライドするには、次のように入力します。

```
fsutil behavior set disabledeletenotify ReFS 0
```

NTFS および ReFS v1 の TRIM (disabledeletenotify) の既定の動作を上書きするには、次のように入力します。

```
fsutil behavior set disabledeletenotify 1
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [fsutil](fsutil.md)

- [fsutil 8dot3name](fsutil-8dot3name.md)
