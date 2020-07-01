---
title: ReFSUtil
description: ReFSUtil は、Windows および Windows Server に含まれているツールであり、大量の参照ボリュームを診断し、残りのファイルを特定し、それらのファイルを別のボリュームにコピーしようとします。
author: laknight5
ms.author: laknight
ms.date: 6/29/2020
ms.prod: windows-server
ms.technology: storage-file-systems
ms.topic: article
ms.openlocfilehash: 0d7c1bf79695c2ddd03943744ebf1df4827d365c
ms.sourcegitcommit: 457e88e5aa6be13a2bffdb8e434a8efc3698678f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85549167"
---
# <a name="refsutil"></a>ReFSUtil

>適用先:Windows Server 2019、Windows 10

ReFSUtil は、Windows および Windows Server に含まれているツールであり、大量の参照ボリュームを診断し、残りのファイルを特定し、それらのファイルを別のボリュームにコピーしようとします。 これは、Windows 10 の%SystemRoot%\Windows\System32 フォルダーまたは% SystemRoot% System32 フォルダー内の Windows Server に \\ あります。

ReFS salvage は、現在の ReFSUtil の主な機能であり、ディスク管理に RAW と表示されるボリュームからデータを回復する場合に便利です。 ReFS Salvage には、スキャンフェーズとコピーフェーズという2つのフェーズがあります。 自動モードでは、スキャンフェーズとコピーフェーズが連続して実行されます。 手動モードでは、各フェーズを個別に実行できます。 進行状況とログは作業ディレクトリに保存されるため、フェーズを個別に実行できるだけでなく、スキャンフェーズを一時停止および再開することもできます。 ボリュームが RAW でない限り、ReFSutil を使用する必要はありません。 読み取り専用の場合、データには引き続きアクセスできます。

## <a name="automatic-mode-command-line-usage"></a>自動モードのコマンドラインの使用

### <a name="quick-automatic-mode-command-line-usage"></a>クイック自動モードのコマンドラインの使用

```dos
refsutil salvage -QA <source volume> <working directory> <target directory> <options>
```
クイックスキャンフェーズの後にコピーフェーズが実行されます。 このモードは、ボリュームの一部の重要な構造が破損していないと想定しているため、短時間で実行されるため、ボリューム全体をスキャンしてそれらを特定する必要はありません。 これにより、古いファイル/ディレクトリ/ボリュームの回復も軽減されます。

### <a name="full-automatic-mode-command-line-usage"></a>フル自動モードのコマンドラインの使用法

```dos
refsutil salvage -FA <source volume> <working directory> <target directory> <options>
```

フルスキャンフェーズの後にコピーフェーズが実行されます。 このモードでは、回復可能なファイル/ディレクトリ/ボリュームのボリューム全体がスキャンされるため、時間がかかることがあります。

## <a name="manual-mode-command-line-usage"></a>手動モードのコマンドラインの使用法

### <a name="diagnose-phase-command-line-usage"></a>診断フェーズのコマンドラインの使用状況

```dos
refsutil salvage -D <source volume> <working directory> <options>
```

まず、が ReFS ボリュームであるかどうかを判断し、ボリュームがマウント可能かどうかを \<source volume\> 判断します。 ボリュームがマウントされていない場合は、reason が決定されます。 これはスタンドアロンフェーズです。

### <a name="quick-scan-phase-command-line-usage"></a>クイックスキャンフェーズのコマンドラインの使用状況

```dos
refsutil salvage -QS <source volume> <working directory> <options>
```

\<source volume\>回復可能なファイルのクイックスキャン。 このモードは、ボリュームの一部の重要な構造が破損していないと想定しているため、短時間で実行されるため、ボリューム全体をスキャンしてそれらを特定する必要はありません。 これにより、古いファイル/ディレクトリ/ボリュームの回復も軽減されます。 検出されたファイルは "foundfiles" に記録さ \<volume signature\> れます。txt "に \<working directory\> あります。 スキャンフェーズが既に停止していた場合、-QS フラグを再度指定して実行すると、中断した場所からスキャンが再開されます。

### <a name="full-scan-phase-command-line-usage"></a>フルスキャンフェーズのコマンドラインの使用

```dos
refsutil salvage -FS <source volume> <working directory> <options>
```

\<source volume\>すべての回復可能なファイルをスキャンします。 このモードでは、回復可能なファイルのボリューム全体がスキャンされるため、時間がかかることがあります。
検出されたファイルは "foundfiles" に記録さ \<volume signature\> れます。txt "に \<working directory\> あります。 スキャンフェーズが既に停止していた場合は、-FS フラグを指定して実行すると、中断した場所からスキャンが再開されます。

### <a name="copy-phase-command-line-usage"></a>コピーフェーズのコマンドラインの使用状況

```dos
refsutil salvage -C <source volume> <working directory> <target directory>
<options>
```

「Foundfiles.」で説明されているすべてのファイルをコピーし \<volume signature\> ます。txt "to \<target
directory\> . スキャンフェーズが早すぎると、"foundfiles. \<volume
signature\> .txt "がまだ書き込まれていない可能性があるため、ファイルはにコピーされません \<target directory\> 。

### <a name="copy-phase-with-list-command-line-usage"></a>リストコマンドラインを使用したコピーフェーズ

```dos
refsutil salvage -SL <source volume> <working directory> <target
directory> <file list> <options>
```

のすべてのファイルを \<file list\> から \<source volume\> にコピーし \<target
directory\> ます。 スキャンが \<file list\> 完了するまで実行されていない必要がありますが、スキャンフェーズでは、のファイルが最初に特定されている必要があります。 \<file list\>"foundfiles. をコピーすることによって生成 \<volume signature\> できます.txt "を新しいファイルに保存し、復元する必要のないファイルを参照している行を削除し、復元するファイルを保持します。 PowerShell コマンドレットの選択文字列は、"foundfiles. \<volume signature\> .txt "を指定すると、必要なパス、拡張子、またはファイル名のみを含めることができます。

### <a name="copy-phase-with-interactive-console"></a>対話型コンソールを使用したコピーフェーズ

```dos
refsutil salvage -IC <source volume> <working directory> <options>
```

上級ユーザー向けの対話型コンソールでファイルを回復します。 また、このモードでは、いずれかのスキャンフェーズから生成されたファイルも必要です。

## <a name="parameters"></a>パラメーター

| パラメーター             | Description                                                                     |
| --------------------- | --------------------------------------------------------------------------------------- |
| \<source volume\>     | 処理する ReFS ボリューム。 "L:" 形式のドライブ文字、またはボリュームマウントポイントへのパス。           |
| \<working directory\> | 一時情報とログを格納する場所。 に配置さ**れていない**必要があり \<source volume\> ます。  |
| \<target directory\>  | 特定されたファイルのコピー先の場所。 に配置さ**れていない**必要があり \<source volume\> ます。 |
| \-m         | 削除されたファイルも含めて、可能なすべてのファイルを回復します。 このオプションは、refsutil salvage v1 では無視されます。 警告: 実行に時間がかかるだけでなく、予期しない結果になる可能性があります。 |
| \-画像         | 詳細モード                                                                                           |
| \-閉じる         | 必要に応じて、最初にボリュームを強制的にマウント解除します。 その後、ボリュームに対して開いているハンドルはすべて無効になります。 例: refsutil salvage-QA R: N: \\ WORKING N: \\ DATA-x                                  |
