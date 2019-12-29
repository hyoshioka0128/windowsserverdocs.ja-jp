---
title: Diskpart のスクリプトと例
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 319c0795-11df-47c8-b203-eadb0577ee0d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9c40ce79664795297af4369e35cbda7422617e6e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377855"
---
# <a name="diskpart-scripts-and-examples"></a>Diskpart のスクリプトと例

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Diskpart `/s` を使用して、ディスク\-関連タスク (ボリュームの作成やダイナミックディスクへのディスクの変換など) を自動化するスクリプトを実行します。 これらのタスクのスクリプト作成は、無人セットアップまたは Sysprep ツールを使用して Windows を展開する場合に便利です。ブートボリューム以外のボリュームの作成はサポートしていません。  
  
-   Diskpart スクリプトを作成するには、実行する Diskpart コマンドを含むテキストファイルを作成します。1行につき1つのコマンドを使用し、空の行を含めません。 `rem` の行を開始して、行をコメントにすることができます。  
  
    たとえば、ディスクをワイプして Windows 回復環境用に 300 MB のパーティションを作成するスクリプトを次に示します。  
  
    ```  
    select disk 0  
    clean  
    convert gpt  
    create partition primary size=300  
    format quick fs=ntfs label="Windows RE tools"  
    assign letter="T"  
    ```  
  
-   DiskPart スクリプトを実行するには、コマンドプロンプトで次のコマンドを入力します。ここで、 *scriptname*は、スクリプトが含まれているテキストファイルの名前です。  
  
    ```  
    diskpart /s scriptname.txt  
    ```  
  
-   DiskPart のスクリプト出力をファイルにリダイレクトするには、次のコマンドを入力します。ここで、 *logfile*は、diskpart によって出力が書き込まれるテキストファイルの名前です。  
  
    ```  
    diskpart /s scriptname.txt > logfile.txt  
    ```  
  
> [!IMPORTANT]  
> **Diskpart**コマンドをスクリプトの一部として使用する場合は、すべての diskpart 操作を1つの diskpart スクリプトの一部として実行することをお勧めします。 連続した DiskPart スクリプトを実行できますが、その後のスクリプトで**diskpart**コマンドを実行する前に、前回の実行を完全にシャットダウンするには、各スクリプトの間に少なくとも15秒かかることが必要です。 そうしないと、後続のスクリプトが失敗する可能性があります。 DiskPart スクリプトと共にバッチファイルに `timeout /t 15` コマンドを追加することで、連続する DiskPart スクリプトの間に一時停止を追加できます。  
  
DiskPart の起動時に、DiskPart のバージョンとコンピューター名がコマンドプロンプトに表示されます。 既定では、スクリプト化されたタスクの実行中に DiskPart でエラーが発生すると、DiskPart はスクリプトの処理を停止し、 **noerr**パラメーター\)を指定していない限り、エラーコード \(を表示します。 ただし、 **noerr**パラメーターを使用したかどうかにかかわらず、構文エラーが発生した場合、DiskPart は常にエラーを返します。 **Noerr**パラメーターを使用すると、ディスクの合計数に関係なく、1つのスクリプトを使用してすべてのディスクのすべてのパーティションを削除するなど、便利なタスクを実行できます。  
  
## <a name="see-also"></a>参照  
[サンプル: Windows PE と DiskPart を使用して、UEFI\/gpt\-ベースのハードドライブパーティションを構成する](https://technet.microsoft.com/library/hh825686.aspx)  
[サンプル: Windows PE と DiskPart を使用して BIOS\/MBR\-ベースのハードディスクパーティションを構成する](https://technet.microsoft.com/library/hh825677.aspx)  
[Windows PowerShell の記憶域コマンドレット](https://technet.microsoft.com/library/hh848705.aspx)  
  

