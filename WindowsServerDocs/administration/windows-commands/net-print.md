---
title: Net print
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f59b2015-4698-415d-9a74-09566c466f40
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 441a61756869442fb91d26bfacc64bbeb8b902f4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826013"
---
# <a name="net-print"></a>Net print

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定された印刷キュー、または指定した印刷ジョブに関する情報を表示または指定した印刷ジョブを制御します。
このコマンドを使用する方法の例については、次を参照してください。、[例](#BKMK_examples)このドキュメントの「します。
> [!NOTE]
> このコマンドは、Windows 7 および Windows Server 2008 R2 で廃止されました。 ただし、さまざまな prnjobs、Windows Management Instrumentation (WMI)、または Windows PowerShell コマンドレットを使用して同じタスクを行うことができます。 詳細については、次を参照してください[prnjobs](prnjobs.md)、 [Windows Management Instrumentation](https://go.microsoft.com/fwlink/?LinkID=29991) (https://go.microsoft.com/fwlink/?LinkID=29991)、 [Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=128426) (https://go.microsoft.com/fwlink/?LinkID=128426)、および、 [。TechNet スクリプト センター ギャラリー](https://go.microsoft.com/fwlink/?LinkId=164635) (https://go.microsoft.com/fwlink/?LinkId=164635)します。
## <a name="syntax"></a>構文
```
Net print {\\<computerName>\<Sharename> | 
\\<computerName> <JobNumber> [/hold | /release | /delete]} [help]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|\\\\<computerName>\\<Sharename>|名前によって、情報を表示するコンピューターと印刷キューを指定します。|
|\\\\<computerName>|(名前) を制御する印刷ジョブをホストするコンピューターを指定します。 コンピューターを指定しない場合、ローカル コンピューターが使用されます。 必要があります、 <JobNumber> パラメーター。|
|<JobNumber>|制御する印刷ジョブの数を指定します。 この数は、印刷ジョブが送信された印刷キューをホストするコンピューターによって割り当てられます。 コンピューター後数がそのコンピュータがホストされている任意のキューにあるその他の印刷ジョブに割り当てられていないこと、印刷ジョブに番号を割り当てます。 使用する場合に必要な\\ \\ <computerName>パラメーター。|
|[/保留と #124;/release & #124;/delete]|印刷ジョブで実行するアクションを指定します。<br /><br />- **保持/** パラメーターが他の印刷ジョブが解放されるまでにバイパスを許可するジョブを遅延します。<br />- **リリース/** パラメーターは、実行が遅れている印刷ジョブを解放します。<br />- **/Delete** パラメーターは、印刷キューから印刷ジョブを削除します。<br /><br />ジョブ番号を指定して、任意のアクションを指定しない場合は、印刷ジョブに関する情報が表示されます。|
|ヘルプ|ヘルプを表示、 **Net print** コマンドです。|
## <a name="remarks"></a>注釈
-   **Net print** \\ \\ <computerName>共有プリンター キューで印刷ジョブに関する情報を表示します。 共有プリンターがレーザーをという名前のキュー内のすべての印刷ジョブのレポートの例を次に示します。
    ```
    printers at \\PRODUCTION
    Name              Job #      Size      Status
    -----------------------------
    LASER Queue       3 jobs               *printer active*
       USER1          84        93844      printing
       USER2          85        12555      Waiting
       USER3          86        10222      Waiting
    ```
-   印刷ジョブに対してレポートの例を次に示します。
    ```
    Job #            35
    Status           Waiting
    Size             3096
    remark
    Submitting user  USER2
    Notify           USER2
    Job data type
    Job parameters
    additional info
    ```
## <a name="BKMK_examples"></a>例
この例では、Dotmatrix 印刷キューの内容を一覧表示、 \\\Production コンピューター。
```
Net print \\Production\Dotmatrix 
```
この例のジョブ番号 35 に関する情報を表示する方法を示しています、 \\\Production コンピューター。
```
Net print \\Production 35 
```
この例では、上のジョブ番号 263 を遅延させる、 \\\Production コンピューター。
```
Net print \\Production 263 /hold 
```
この例では、ジョブ番号 263 をリリースして、 \\\Production コンピューター。
```
Net print \\Production 263 /release 
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[印刷コマンドのリファレンス](print-command-reference.md)
