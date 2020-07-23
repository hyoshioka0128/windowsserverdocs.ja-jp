---
title: diskpart のスクリプトと例
description: Diskpart スクリプトのリファレンス記事と、ディスク関連のタスク (ボリュームの作成やダイナミックディスクへのディスクの変換など) を自動化する方法の例を紹介します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 319c0795-11df-47c8-b203-eadb0577ee0d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 64355bd452934909d0600fa791e7a4c2d2066b6f
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86958294"
---
# <a name="diskpart-scripts-and-examples"></a>diskpart のスクリプトと例

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

`diskpart /s`ボリュームの作成やダイナミックディスクへのディスクの変換など、ディスク関連のタスクを自動化するスクリプトを実行するには、を使用します。 ブート ボリューム以外のボリュームの作成をサポートしていない無人セットアップや Sysprep を使用して Windows を展開する場合は、これらのタスクをスクリプト化しておくと便利です。

Diskpart スクリプトを作成するには、実行する Diskpart コマンドを含むテキストファイルを作成します。1行につき1つのコマンドを使用し、空の行を含めません。 を使用して行を開始し `rem` 、行にコメントを作成することができます。 たとえば、ディスクをワイプした後、Windows 回復環境用に 300 MB のパーティションを作成するスクリプトを次に示します。

    ```
    select disk 0
    clean
    convert gpt
    create partition primary size=300
    format quick fs=ntfs label=Windows RE tools
    assign letter=T
    ```

## <a name="examples"></a>例

- Diskpart スクリプトを実行するには、コマンドプロンプトで次のコマンドを入力します。ここで、 *scriptname*は、スクリプトが含まれているテキストファイルの名前です。

    ```
    diskpart /s scriptname.txt
    ```

- Diskpart のスクリプト出力をファイルにリダイレクトするには、次のコマンドを入力します。ここで、 *logfile*は、diskpart によって出力が書き込まれるテキストファイルの名前です。

    ```
    diskpart /s scriptname.txt > logfile.txt
    ```

### <a name="remarks"></a>注釈

- **Diskpart**コマンドをスクリプトの一部として使用する場合は、すべての diskpart 操作を1つの diskpart スクリプトの一部として実行することをお勧めします。 連続した diskpart スクリプトを実行できますが、その後のスクリプトで**diskpart**コマンドを実行する前に、前回の実行を完全にシャットダウンするには、各スクリプトの間に少なくとも15秒かかることが必要です。 このようにしないと、以降のスクリプトが失敗することがあります。 `timeout /t 15`Diskpart スクリプトと共にコマンドをバッチファイルに追加することで、連続する diskpart スクリプトの間に一時停止を追加できます。

- Diskpart の起動時に、diskpart のバージョンとコンピューター名がコマンドプロンプトに表示されます。 既定では、スクリプト化されたタスクの実行中に diskpart によってエラーが検出された場合、diskpart はスクリプトの処理を停止し、エラーコードを表示します ( **noerr**パラメーターを指定していない場合)。 ただし、 **noerr**パラメーターを使用したかどうかにかかわらず、構文エラーが発生した場合、diskpart は常にエラーを返します。 **Noerr**パラメーターを使用すると、ディスクの合計数に関係なく、1つのスクリプトを使用してすべてのディスクのすべてのパーティションを削除するなど、便利なタスクを実行できます。

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [サンプル: Windows PE と DiskPart を使用して UEFI/GPT ベースのハードドライブパーティションを構成する](/previous-versions/windows/it-pro/windows-8.1-and-8/hh825686(v=win.10))

- [サンプル: Windows PE と DiskPart を使用して BIOS/MBR ベースのハードディスクパーティションを構成する](/previous-versions/windows/it-pro/windows-8.1-and-8/hh825677(v=win.10))

- [Storage Cmdlets in Windows PowerShell (Windows PowerShell の記憶域コマンドレット)](/powershell/module/storage/?view=win10-ps)
