---
title: Diskpart スクリプトと例
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: a8bd0dfab98ca705cf64766d66285c69bd3d3129
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862793"
---
# <a name="diskpart-scripts-and-examples"></a>Diskpart スクリプトと例

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Diskpart を使用して、`/s`ディスクを自動化するスクリプトを実行する\-ボリュームの作成や、ディスクをダイナミック ディスクに変換するなどのタスクに関連します。 これらのタスクのスクリプトは、ブート ボリューム以外のボリュームの作成がサポートされていない無人セットアップまたは Sysprep ツールを使用して Windows を展開する場合に便利です。  
  
-   Diskpart のスクリプトを作成するには、1 行、1 つのコマンドとなしの空白行を実行する目的の Diskpart コマンドを含むテキスト ファイルを作成します。 行を開始する`rem`行をコメントにします。  
  
    たとえば、ここでは s、ディスクを消去し、Windows 回復環境用に 300 MB、パーティションを作成するスクリプト:  
  
    ```  
    select disk 0  
    clean  
    convert gpt  
    create partition primary size=300  
    format quick fs=ntfs label="Windows RE tools"  
    assign letter="T"  
    ```  
  
-   コマンド プロンプトで DiskPart のスクリプトを実行するには、次のコマンドを入力、 *scriptname*スクリプトを含むテキスト ファイルの名前を指定します。  
  
    ```  
    diskpart /s scriptname.txt  
    ```  
  
-   DiskPart のスクリプトの出力結果をファイルにリダイレクトするには、次のコマンドを入力、 *logfile* DiskPart がその出力を書き込むテキスト ファイルの名前を指定します。  
  
    ```  
    diskpart /s scriptname.txt > logfile.txt  
    ```  
  
> [!IMPORTANT]  
> 使用する場合、 **DiskPart**スクリプトの一部としてコマンドを完了することによる操作はすべて 1 つの DiskPart スクリプトの一部として 1 つをお勧めします。 連続した DiskPart スクリプトを実行することができますが、各スクリプトを実行する前に前回の実行の完全にシャット ダウンの間には少なくとも 15 秒を許可する必要があります、 **DiskPart**以降のスクリプトでもう一度コマンド。 それ以外の場合、以降のスクリプトが失敗する可能性があります。 追加することで連続した DiskPart スクリプト間一時停止を追加することができます、 `timeout /t 15` DiskPart スクリプトと共にバッチ ファイル コマンド。  
  
DiskPart を起動すると、コマンド プロンプトで DiskPart バージョンおよびコンピューター名の表示します。 既定では、DiskPart スクリプト化されたタスクを実行しているときにエラーが発生した場合 DiskPart スクリプトの処理を停止し、エラー コードを表示します\(を指定しない限り、 **noerr**パラメーター\)します。 ただし、DiskPart 常にエラーを返します使用するかどうかに関係なく、構文エラーが発生したときに、 **noerr**パラメーター。 **Noerr**パラメーターでは、1 つのスクリプトを使用して、ディスクの合計数に関係なくすべてのディスク上のすべてのパーティションを削除するなどの便利なタスクを実行することができます。  
  
## <a name="see-also"></a>関連項目  
[サンプル: UEFI の構成\/gpt\-ベースのハード ドライブ パーティションを使用して Windows PE と DiskPart](https://technet.microsoft.com/library/hh825686.aspx)  
[サンプル: BIOS を構成する\/MBR\-ベースの Windows PE と DiskPart を使用してハード ディスク パーティション](https://technet.microsoft.com/library/hh825677.aspx)  
[Windows PowerShell の記憶域コマンドレット](https://technet.microsoft.com/library/hh848705.aspx)  
  

