---
title: ReFSUtil
description: ReFSUtil ツールの参照記事。大量の ReFS ボリュームの診断、残りのファイルの特定、およびそれらのファイルの別のボリュームへのコピーを試行します。
author: laknight5
ms.author: laknight
ms.date: 6/29/2020
ms.topic: article
ms.openlocfilehash: d40faa165666a5836dc6e87589d27f8eb643479e
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87884215"
---
# <a name="refsutil"></a>ReFSUtil

> 適用先:Windows Server 2019、Windows 10

ReFSUtil は、Windows および Windows Server に含まれているツールであり、大量の参照ボリュームを診断し、残りのファイルを特定し、それらのファイルを別のボリュームにコピーしようとします。 これは、フォルダー内の Windows 10 `%SystemRoot%\Windows\System32` またはフォルダー内の Windows Server に `%SystemRoot%\System32` あります。

ReFS salvage は ReFSUtil の主な機能であり、ディスク管理で RAW と表示されるボリュームからデータを回復する場合に便利です。 ReFS Salvage には、スキャンフェーズとコピーフェーズという2つのフェーズがあります。 自動モードでは、スキャンフェーズとコピーフェーズが連続して実行されます。 手動モードでは、各フェーズを個別に実行できます。 進行状況とログは作業ディレクトリに保存されるため、フェーズを個別に実行できるだけでなく、スキャンフェーズを一時停止および再開することもできます。 ボリュームが未加工でない限り、ReFSutil ツールを使用する必要はありません。 読み取り専用の場合、データには引き続きアクセスできます。

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| `<source volume>` | 処理する ReFS ボリュームを指定します。 ドライブ文字は "L:" の形式にする必要があります。または、ボリュームマウントポイントへのパスを指定する必要があります。 |
| `<working directory>` | 一時情報とログを格納する場所を指定します。 に配置さ**れていない**必要があり `<source volume>` ます。 |
| `<target directory>` | 識別されたファイルのコピー先の場所を指定します。 に配置さ**れていない**必要があり `<source volume>` ます。 |
| \-m | 削除されたファイルも含めて、可能なすべてのファイルを回復します。<p>**警告:** このパラメーターによってプロセスの実行時間が長くなるだけでなく、予期しない結果が生じる可能性もあります。 |
| \-画像 | 詳細モードを使用するように指定します。 |
| \-閉じる | 必要に応じて、最初にボリュームを強制的にマウント解除します。 その後、ボリュームに対して開いているハンドルはすべて無効になります。 たとえば、`refsutil salvage -QA R: N:\WORKING N:\DATA -x` のようにします。 |

## <a name="usage-and-available-options"></a>使用法と使用可能なオプション

### <a name="quick-automatic-mode-command-line-usage"></a>クイック自動モードのコマンドラインの使用

クイックスキャンフェーズの後にコピーフェーズを実行します。 このモードは、ボリュームの一部の重要な構造が破損していないと想定しているため、より短時間で実行されるため、ボリューム全体をスキャンしてそれらを特定する必要はありません。 これにより、古いファイル/ディレクトリ/ボリュームの回復も軽減されます。

```
refsutil salvage -QA <source volume> <working directory> <target directory> <options>
```

### <a name="full-automatic-mode-command-line-usage"></a>フル自動モードのコマンドラインの使用法

フルスキャンフェーズの後にコピーフェーズを実行します。 このモードでは、回復可能なファイル/ディレクトリ/ボリュームのボリューム全体がスキャンされるため、時間がかかることがあります。

```
refsutil salvage -FA <source volume> <working directory> <target directory> <options>
```

### <a name="diagnose-phase-command-line-usage-manual-mode"></a>診断フェーズのコマンドラインの使用法 (手動モード)

まず、が ReFS ボリュームであるかどうかを判断し、ボリュームがマウント可能かどうかを `<source volume>` 判断します。 ボリュームがマウント可能でない場合は、理由が提供されます。 これはスタンドアロンフェーズです。

```
refsutil salvage -D <source volume> <working directory> <options>
```

### <a name="quick-scan-phase-command-line-usage"></a>クイックスキャンフェーズのコマンドラインの使用状況

`<source volume>`回復可能なすべてのファイルについて、のクイックスキャンを実行します。 このモードは、ボリュームの一部の重要な構造が破損していないと想定しているため、短時間で実行されます。そのため、ボリューム全体をスキャンしてそれらを特定する必要はありません。 これにより、古いファイル/ディレクトリ/ボリュームの回復も軽減されます。 検出されたファイルは、にあるファイルに記録され `foundfiles.<volume signature>.txt` `<working directory>` ます。 スキャンフェーズが既に停止していた場合、 **-QS**フラグを指定して実行すると、中断した場所からスキャンが再開されます。

```
refsutil salvage -QS <source volume> <working directory> <options>
```

### <a name="full-scan-phase-command-line-usage"></a>フルスキャンフェーズのコマンドラインの使用

すべて `<source volume>` の回復可能なファイルをスキャンします。 このモードでは、回復可能なファイルのボリューム全体がスキャンされるため、時間がかかることがあります。 検出されたファイルは、にあるファイルにログ記録され `foundfiles.<volume signature>.txt` `<working directory>` ます。 スキャンフェーズが既に停止していた場合、 **-FS**フラグを指定して実行すると、中断した場所からスキャンが再開されます。

```
refsutil salvage -FS <source volume> <working directory> <options>
```

### <a name="copy-phase-command-line-usage"></a>コピーフェーズのコマンドラインの使用状況

ファイルに記述さ `foundfiles.<volume signature>.txt` れているすべてのファイルをにコピー `<target directory>` します。 スキャンフェーズを早めに停止した場合は、 `foundfiles.<volume signature>.txt` ファイルがまだ存在していない可能性があるため、ファイルはにコピーされません `<target directory>` 。

```
refsutil salvage -C <source volume> <working directory> <target directory> <options>
```

### <a name="copy-phase-with-list-command-line-usage"></a>リストコマンドラインを使用したコピーフェーズ

内のすべてのファイルを `<file list>` から `<source volume>` にコピーし `<target directory>` ます。 スキャンが `<file list>` 完了するまで実行されていない必要がある場合でも、のファイルは、最初にスキャンフェーズで識別されている必要があります。 を `<file list>` 生成するには、 `foundfiles.<volume signature>.txt` 新しいファイルにコピーして、復元する必要のないファイルを参照している行を削除し、復元する必要があるファイルを保持します。 PowerShell コマンドレットの**選択文字列**は、 `foundfiles.<volume signature>.txt` 目的のパス、拡張子、またはファイル名のみを含めるようにフィルター処理する場合に役立ちます。

```
refsutil salvage -SL <source volume> <working directory> <target directory> <file list> <options>
```

### <a name="copy-phase-with-interactive-console"></a>対話型コンソールを使用したコピーフェーズ

上級ユーザーは、対話型コンソールを使用してファイルを回復できます。 また、このモードでは、いずれかのスキャンフェーズから生成されたファイルも必要です。

```
refsutil salvage -IC <source volume> <working directory> <options>
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
