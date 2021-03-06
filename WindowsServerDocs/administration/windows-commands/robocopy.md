---
title: robocopy
description: Windows および Windows Server での robocopy コマンドを使用してファイルをコピーする方法について説明します
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d4c6e8e9-fcb3-4a4a-9d04-2d8c367b6354
author: coreyp-at-msft
ms.author: coreyp
manager: lizapo
ms.date: 07/25/2018
ms.openlocfilehash: 7ab2eff32b105916d979a954275e9c9122a06903
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441725"
---
# <a name="robocopy"></a>robocopy

ファイルのデータをコピーします。

## <a name="syntax"></a>構文

```
robocopy <Source> <Destination> [<File>[ ...]] [<Options>]
```

## <a name="parameters"></a>パラメーター

|   パラメーター    |                                                                                            説明                                                                                             |
|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   \<ソース >    |                                                                            ソース ディレクトリへのパスを指定します。                                                                             |
| \<宛先 > |                                                                          インストール先ディレクトリへのパスを指定します。                                                                          |
|    \<File>     | ファイルをコピーするファイルを指定します。 ワイルドカード文字を使用することができます ( **&#42;** または **?** ) する場合は、します。 場合、**ファイル**パラメーターが指定されていない **\*.\\** \*既定値として使用されます。 |
|   \<オプション >   |                                                                    使用するオプションを指定します、 **robocopy**コマンド。                                                                     |

### <a name="copy-options"></a>オプションをコピーします。

|オプション|説明|
|------|-----------|
|/s|コピーのサブディレクトリです。 このオプションが空のディレクトリを除外することに注意してください。|
|/e|コピーのサブディレクトリです。 このオプションが空のディレクトリが含まれることに注意してください。 詳細については、次を参照してください。 [解説](#remarks)します。|
|/lev:\<N>|上位のみをコピー *N* ソース ディレクトリ ツリーのレベルです。|
|/z|再起動可能モードでファイルをコピーします。|
|/b|Backup モードでファイルをコピーします。|
|/zb|再起動可能モードを使用します。 アクセスが拒否された場合、このオプションは、Backup モードを使用します。|
|/efsraw|EFS の RAW モードでは、すべての暗号化されたファイルをコピーします。|
|/copy:\<CopyFlags>|コピーされるファイルのプロパティを指定します。 このオプションの有効な値を次に示します。</br>**D** データ</br>**A** 属性</br>**T** タイムスタンプ</br>**S** NTFS アクセス制御リスト (ACL)</br>**O** 所有者情報</br>**U** の監査情報</br>既定値 **CopyFlags** は **DAT** (データ、属性、およびタイムスタンプ) です。|
|/dcopy:\<copyflags\>|ディレクトリのコピーを定義します。 既定値は DA. オプション D は、データ、=、A = 属性と T = タイムスタンプ。|
|数/秒|セキュリティでのファイルのコピー (に相当 **/copy:DATS**)。|
|/copyall|すべてのファイル情報のコピー (に相当 **/copy:DATSOU**)。|
|/nocopy|コピー ファイルの情報はありません (で役に立ちます **パージ/** )。|
|/secfix|でも、すべてのファイルに修正プログラム ファイルのセキュリティには、ものがスキップされます。|
|/timfix|でも、すべてのファイルに修正プログラム ファイルの時間には、ものがスキップされます。|
|/purge|リンク先のファイルとソースに存在しなくなったディレクトリを削除します。 詳細については、次を参照してください。 [解説](#remarks)します。|
|/mir|ディレクトリ ツリーをミラー化 (に相当 **/e** plus **パージ/** )。 詳細については、次を参照してください。 [解説](#remarks)します。|
|/mov|ファイルを移動し、コピーした後に、ソースからも削除します。|
|/move|ファイルとディレクトリを移動し、コピーした後に、ソースからも削除します。|
|/a +: [RASHCNET]|コピーしたファイルに指定された属性を追加します。|
|/a -: [RASHCNET]|コピーしたファイルから、指定された属性を削除します。|
|作成します|ディレクトリ ツリー、長さゼロのファイルのみを作成します。|
|fat/|8.3 形式の文字長 FAT ファイル名のみを使用して、リンク先のファイルを作成します。|
|/256|非常に長いパス (256 文字より長い) のサポートをオフにします。|
|/月:\<N >|ソースを監視し、コンテキストを再実行 *N* 変更が検出されました。|
|/mot:\<M >|ソースを監視し、再度実行 *M* 分に変更が検出された場合。|
|/MT [: N]|マルチ スレッドのコピーを作成 *N* スレッドです。 *N* 1 ~ 128 の範囲の整数でなければなりません。 既定値 *N* は 8 です。</br>**/MT** でパラメーターは使用できません、 **/IPG** と **/EFSRAW** パラメーター。</br>使用して出力をリダイレクト **/log** パフォーマンス向上のためのオプションです。</br>注:/MT パラメーターは、Windows Server 2008 R2 および Windows 7 に適用されます。|
|/rh:hhmm-hhmm|新しいコピーを起動するときに実行時間を指定します。|
|/pf|チェックは、ファイル (ごとに渡されない) ごとに時間を実行します。|
|/ipg:n|低速回線の帯域幅を解放する間のパケットの間隔を指定します。|
|/sl|シンボリック リンクを追跡して、代わりに、リンクのコピーを作成しないでください。|

> [!IMPORTANT]
> 使用する場合、 **/SECFIX** コピー オプションでもこれらの追加コピー オプションのいずれかを使用してコピーするセキュリティ情報の種類を指定します。
>- **/COPYALL**
>- **/COPY:O**
>- **/COPY:S**
>- **/COPY:U**
>- **/SEC**

### <a name="file-selection-options"></a>ファイルの選択オプション

|オプション|説明|
|------|-----------|
|/a|対象のファイルのみをコピー、 **アーカイブ** 属性を設定します。|
|/m|対象のファイルのみをコピー、 **アーカイブ** 属性が設定されているし、リセット、 **アーカイブ** 属性です。|
|/ia: [RASHCNETO]|指定した属性のいずれかが設定する対象のファイルのみが含まれます。|
|/xa: [RASHCNETO]|指定した属性のいずれかが設定する対象のファイルを除外します。|
|/xf \<FileName>[ ...]|指定した名前またはパスに一致するファイルを除外します。 なお*FileName*ワイルドカード文字を含めることができます ( **&#42;** と**でしょうか。** )。|
|/xd\<ディレクトリ > [...]|指定した名前とパスに一致するディレクトリを除外します。|
|/xc|変更されたファイルを除外します。|
|/xn|新しいファイルを除外します。|
|/xo|古いファイルを除外します。|
|/xx|余分なファイルやディレクトリを除外します。|
|指定.|「今」ファイルとディレクトリを除外します。|
|/is|同じファイルが含まれます。|
|/it|ファイル「調整」にはが含まれます。|
|最大:\<N >|ファイルの最大サイズを指定します (より大きいファイルを除外する *N* バイト)。|
|/min:\<N>|最小ファイル サイズを指定します (よりも小さいファイルを除外する *N* バイト)。|
|/maxage:\<N >|ファイルの最大経過時間を指定します (よりも古いファイルを除外する *N* 日または日付)。|
|/minage:\<N >|最小のファイルの経過時間を指定します (除外するファイルより新しい *N* 日または日付)。|
|/maxlad:\<N >|最終アクセス日の最大数は指定 (除外するファイルから未使用 *N*)。|
|/minlad:\<N >|前回アクセスした日付の最小値を指定します (以来使用されているファイルを除外 *N*) 場合 *N* 未満の 1900 *N* 、日数を指定します。 それ以外の場合、 *N* YYYYMMDD 形式で日付を指定します。|
|/xj|通常は既定で含まの接合ポイントは含まれません。|
|/fft|FAT ファイル (有効桁数は 2 秒間) 時間を想定しています。|
|/dst|1 時間 DST 時刻の違いを補正します。|
|/xjd|ディレクトリの接合ポイントは含まれません。|
|/xjf|ファイルの接合ポイントは含まれません。|

### <a name="retry-options"></a>再試行オプション

|オプション|説明|
|------|-----------|
|/r:\<N>|失敗したコピーを再試行の回数を指定します。 既定値の *N* 1,000,000 (100万再試行)。|
|/w:\<N >|秒単位での再試行までの待機時間を指定します。 既定値の *N* 30 (待機時間 30 秒)。|
|/reg|指定された値を保存、 **/r** と **/w** レジストリの既定の設定とオプションです。|
|/tbd|システムが定義する共有名を待つことを指定します (エラー 67 を再試行してください)。|

### <a name="logging-options"></a>ログ オプション

|オプション|説明|
|------|-----------|
|/l|ファイルのみリストに表示されることを指定 (およびコピーされず、削除、またはタイムスタンプ) です。|
|/x|選択されているものだけでなく、すべての余分なファイルを報告します。|
|/v|詳細出力を生成し、すべてのスキップしたファイルを示します。|
|/ts|出力には、ソース ファイルのタイムスタンプが含まれています。|
|/fp|出力にはファイルの完全パス名が含まれます。|
|/bytes|バイトとして、サイズを印刷します。|
|/ns|ファイルのサイズを記録しないことを指定します。|
|/nc|ファイル クラスがないログに記録することを指定します。|
|/nfl|ファイル名ではないログに記録することを指定します。|
|/ndl|ディレクトリ名がないログに記録することを指定します。|
|/np|コピー操作 (ファイルまたはディレクトリがこれまでコピーの数) の進行状況が表示されないことを指定します。|
|/eta|コピーしたファイルの到着 (予定) の推定時間を示します。|
|/log:\<LogFile>|状態の出力を (既存のログ ファイルを上書きする)、ログ ファイルに書き込みます。|
|/log+:\<LogFile>|状態の出力を (既存のログ ファイルに出力を追加する)、ログ ファイルに書き込みます。|
|/unicode|Unicode テキストとして状態の出力を表示します。|
|/unilog:\<LogFile>|(既存のログ ファイルを上書きする) の Unicode 文字としてログ ファイルに出力のステータスを書き込みます。|
|/unilog+:\<LogFile>|(出力を既存のログ ファイルに追加する) の Unicode 文字としてログ ファイルに出力のステータスを書き込みます。|
|/tee|ログ ファイルだけでなく、コンソール ウィンドウには、状態の出力を書き込みます。|
|/njh|ジョブのヘッダーがないことを指定します。|
|/njs|ジョブの概要がないことを指定します。|

### <a name="job-options"></a>ジョブのオプション

|オプション|説明|
|------|-----------|
|/job:\<JobName>|パラメーターをジョブの名前付きのファイルから派生するように指定します。|
|/save:\<JobName>|パラメーターを名前付きのジョブのファイルに保存するように指定します。|
|/quit|(パラメーターを表示する) のコマンドラインの処理の後に終了します。|
|/nosd|ソース ディレクトリが指定されていないことを示します。|
|/nodd|インストール先ディレクトリが指定されていないことを示します。|
|/if|指定したファイルが含まれます。|

### <a name="exit-return-codes"></a>(戻り値) の終了コード

Value | 説明
-- | --
0 | ファイルがコピーされません。 エラーは発生しませんでした。  ファイルは一致しませんでした。 変換先ディレクトリにファイルが既に存在します。そのため、コピー操作はスキップされました。
1 | すべてのファイルがコピーされました。
2 | 保存先ディレクトリには、一部には、ソース ディレクトリに存在しない追加ファイルがあります。 ファイルがコピーされません。
3 | いくつかのファイルがコピーされました。 追加のファイルが存在していた。 エラーは発生しませんでした。
5 | いくつかのファイルがコピーされました。 いくつかのファイルが一致していません。 エラーは発生しませんでした。
6 | 追加のファイルと一致しないファイルが存在します。 ファイルはコピーされませんし、エラーが発生したことはありません。 つまり、保存先ディレクトリにファイルが既に存在します。
7 | ファイルがコピーされた、ファイルの不一致が存在する場合は、および追加のファイルが存在します。
8 | 複数のファイルをコピーできませんでした。

> [!NOTE]
> 8 より大きい値では、コピー操作中に少なくとも 1 つのエラーがあったことを示します。

### <a name="remarks"></a>注釈

-   **/Mir** オプションに相当、 **/e** plus **パージ/** 動作の小さな違いの 1 つのオプション。  
    -   **/E** plus **パージ/** オプションでは、インストール先ディレクトリが存在する場合は、移行先ディレクトリのセキュリティ設定は、上書きができます。
    -   **/Mir** オプションでは、インストール先ディレクトリが存在する場合は、移行先のディレクトリのセキュリティ設定が上書きされます。

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)
