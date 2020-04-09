---
title: Net print (英語の可能性あり)
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f59b2015-4698-415d-9a74-09566c466f40
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ad631788a59c24dcb92d180330de25a5be320154
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839055"
---
# <a name="net-print"></a>Net print (英語の可能性あり)

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定された印刷キュー、または指定した印刷ジョブに関する情報を表示または指定した印刷ジョブを制御します。
このコマンドの使用方法の例については、このドキュメントの「[例](#BKMK_examples)」を参照してください。
> [!NOTE]
> このコマンドは、Windows 7 および Windows Server 2008 R2 で廃止されました。 ただし、prnjobs.vbs、Windows Management Instrumentation (WMI)、または Windows PowerShell コマンドレットを使用して、同じタスクの多くを実行することができます。 詳細については、「 [prnjobs.vbs](prnjobs.md)、 [Windows Management Instrumentation](https://go.microsoft.com/fwlink/?LinkID=29991) (https://go.microsoft.com/fwlink/?LinkID=29991)」、「 [Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=128426) (https://go.microsoft.com/fwlink/?LinkID=128426)」、および「 [TechNet スクリプトセンターギャラリー](https://go.microsoft.com/fwlink/?LinkId=164635) (https://go.microsoft.com/fwlink/?LinkId=164635)」を参照してください。
> ## <a name="syntax"></a>構文
> ```
> Net print {\\<computerName>\<Sharename> | 
> \\<computerName> <JobNumber> [/hold | /release | /delete]} [help]
> ```
> ### <a name="parameters"></a>パラメーター
> 
> |               パラメーター               |                                                                                                                                                                                                                     説明                                                                                                                                                                                                                      |
> |----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
> |    \\\\<computerName>\\<Sharename>     |                                                                                                                                                                            名前によって、情報を表示するコンピューターと印刷キューを指定します。                                                                                                                                                                             |
> |           \\\\<computerName>           |                                                                                                                                 (名前) を制御する印刷ジョブをホストするコンピューターを指定します。 コンピューターを指定しない場合、ローカル コンピューターが使用されます。 必要があります、 <JobNumber> パラメーター。                                                                                                                                  |
> |              <JobNumber>               |                                             制御する印刷ジョブの数を指定します。 この数は、印刷ジョブが送信された印刷キューをホストするコンピューターによって割り当てられます。 コンピューター後数がそのコンピュータがホストされている任意のキューにあるその他の印刷ジョブに割り当てられていないこと、印刷ジョブに番号を割り当てます。 \\\\<computerName> パラメーターを使用する場合に必要です。                                             |
> | [/保留と #124;/release & #124;/delete] | 印刷ジョブで実行するアクションを指定します。<p>- **保持/** パラメーターが他の印刷ジョブが解放されるまでにバイパスを許可するジョブを遅延します。<br />- **リリース/** パラメーターは、実行が遅れている印刷ジョブを解放します。<br />- **/Delete** パラメーターは、印刷キューから印刷ジョブを削除します。<p>ジョブ番号を指定しても、何も指定しない場合は、印刷ジョブに関する情報が表示されます。 |
> |                  ヘルプ                  |                                                                                                                                                                                                     ヘルプを表示、 **Net print** コマンドです。                                                                                                                                                                                                     |
> 
> ## <a name="remarks"></a>コメント
> - **Net print** \\\\<computerName> では、印刷ジョブに関する情報が共有プリンターキューに表示されます。 共有プリンターがレーザーをという名前のキュー内のすべての印刷ジョブのレポートの例を次に示します。
>   ```
>   printers at \\PRODUCTION
>   Name              Job #      Size      Status
>   -----------------------------
>   LASER Queue       3 jobs               *printer active*
>      USER1          84        93844      printing
>      USER2          85        12555      Waiting
>      USER3          86        10222      Waiting
>   ```
> - 印刷ジョブに対してレポートの例を次に示します。
>   ```
>   Job #            35
>   Status           Waiting
>   Size             3096
>   remark
>   Submitting user  USER2
>   Notify           USER2
>   Job data type
>   Job parameters
>   additional info
>   ```
>   ## <a name="examples"></a><a name=BKMK_examples></a>例
>   この例では、Dotmatrix 印刷キューの内容を一覧表示、 \\\Production コンピューター。
>   ```
>   Net print \\Production\Dotmatrix 
>   ```
>   この例のジョブ番号 35 に関する情報を表示する方法を示しています、 \\\Production コンピューター。
>   ```
>   Net print \\Production 35 
>   ```
>   この例では、上のジョブ番号 263 を遅延させる、 \\\Production コンピューター。
>   ```
>   Net print \\Production 263 /hold 
>   ```
>   この例では、ジョブ番号 263 をリリースして、 \\\Production コンピューター。
>   ```
>   Net print \\Production 263 /release 
>   ```
>   ## <a name="additional-references"></a>その他の参照情報
>   - [コマンドライン構文のキー](command-line-syntax-key.md)
>   [印刷コマンドリファレンス](print-command-reference.md)
