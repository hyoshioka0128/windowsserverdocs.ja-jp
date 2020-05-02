---
title: Diskpart のスクリプトと例
description: Diskpart スクリプトのリファレンストピックと、ディスク関連のタスク (ボリュームの作成やダイナミックディスクへのディスクの変換など) を自動化する方法の例を紹介します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 319c0795-11df-47c8-b203-eadb0577ee0d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 74cefe87fbbeaa1f2bacccbe4addeff952b2c432
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719473"
---
# <a name="diskpart-scripts-and-examples"></a>Diskpart のスクリプトと例

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Diskpart `/s`を使用して、ボリュームの作成やダイナミックディスクへのディスクの変換など、ディスク関連のタスクを自動化するスクリプトを実行します。 ブート ボリューム以外のボリュームの作成をサポートしていない無人セットアップや Sysprep を使用して Windows を展開する場合は、これらのタスクをスクリプト化しておくと便利です。  
  
-   Diskpart スクリプトを作成するには、実行する Diskpart コマンドを含むテキストファイルを作成します。1行につき1つのコマンドを使用し、空の行を含めません。 を使用して`rem`行を開始し、行にコメントを作成することができます。  
  
    たとえば、ディスクをワイプして Windows 回復環境用に 300 MB のパーティションを作成するスクリプトを次に示します。  
  
    ```  
    select disk 0  
    clean  
    convert gpt  
    create partition primary size=300  
    format quick fs=ntfs label=Windows RE tools  
    assign letter=T  
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
> **Diskpart**コマンドをスクリプトの一部として使用する場合は、すべての diskpart 操作を1つの diskpart スクリプトの一部として実行することをお勧めします。 連続した DiskPart スクリプトを実行できますが、その後のスクリプトで**diskpart**コマンドを実行する前に、前回の実行を完全にシャットダウンするには、各スクリプトの間に少なくとも15秒かかることが必要です。 このようにしないと、以降のスクリプトが失敗することがあります。 DiskPart スクリプトと共に`timeout /t 15`コマンドをバッチファイルに追加することで、連続する diskpart スクリプトの間に一時停止を追加できます。  
  
DiskPart を起動すると、DiskPart のバージョンとコンピューター名がコマンド プロンプトに表示されます。 既定では、スクリプト化されたタスクの実行中に DiskPart によってエラーが検出された場合、 \(diskpart はスクリプトの処理を\)停止し、 **noerr**パラメーターを指定しない限りエラーコードを表示します。 ただし、 **noerr**パラメーターを使用したかどうかにかかわらず、構文エラーが発生した場合、DiskPart は常にエラーを返します。 **Noerr**パラメーターを使用すると、ディスクの合計数に関係なく、1つのスクリプトを使用してすべてのディスクのすべてのパーティションを削除するなど、便利なタスクを実行できます。  
  
## <a name="additional-references"></a>その他のリファレンス
  
- [サンプル: Windows PE\/と\-DiskPart を使用して UEFI Gpt ベースのハードドライブパーティションを構成する](https://technet.microsoft.com/library/hh825686.aspx)  
- [サンプル: Windows PE\/と\-DiskPart を使用して BIOS MBR ベースのハードディスクパーティションを構成する](https://technet.microsoft.com/library/hh825677.aspx)  
- [Storage Cmdlets in Windows PowerShell (Windows PowerShell の記憶域コマンドレット)](https://technet.microsoft.com/library/hh848705.aspx)  
  

