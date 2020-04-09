---
title: bootcfg debug
description: Windows コマンドに関するトピックでは、指定されたオペレーティングシステムエントリのデバッグ設定を追加または変更する bootcfg debug について説明しています。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 28afa5fb-a236-46e2-b1a4-a3c43a49c437
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: de225e1bd0f8406a0b28e5af28fd29bceb8e713c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848635"
---
# <a name="bootcfg-debug"></a>bootcfg debug

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定したオペレーティングシステムエントリのデバッグ設定を追加または変更します。

## <a name="syntax"></a>構文
```
bootcfg /debug {ON | OFF | edit}[/s <computer> [/u <Domain>\<User> /p <Password>]] [/port {COM1 | COM2 | COM3 | COM4}] [/baud {9600 | 19200 | 38400 | 57600 | 115200}] [/id <OSEntryLineNum>]
```
### <a name="parameters"></a>パラメーター

|                           パラメーター                           |                                                                                                                                                                                                                    説明                                                                                                                                                                                                                    |
|---------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                  {ON &#124; OFF&#124; edit}                   | デバッグ用の値を指定します。<p>**ON** -指定した <OSEntryLineNum>に/debug オプションを追加することにより、リモートデバッグのサポートを有効にします。<p>**OFF** -指定された <OSEntryLineNum>から/debug オプションを削除することによって、リモートデバッグのサポートを無効にします。<p>**[編集]** -指定された <OSEntryLineNum>の/debug オプションに関連付けられている値を変更することにより、ポートとボーレートの設定を変更できます。 |
|                         /s <computer>                         |                                                                                                                                                                名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。                                                                                                                                                                 |
|                      /u <Domain>\\<User>                      |                                                                                                                       <User> または <Domain>\\<User>によって指定されたユーザーのアカウントアクセス許可を使用してコマンドを実行します。 既定値は、コマンドを実行しているコンピューターの現在のログオンユーザーのアクセス許可です。                                                                                                                        |
|                         /p <Password>                         |                                                                                                                                                                               指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。                                                                                                                                                                               |
|       /port {COM1 &#124; COM2 &#124; COM3 &#124; COM4}        |                                                                                                                                                                デバッグに使用する COM ポートを指定します。 デバッグを無効にする場合は、 **/port**パラメーターを使用しないでください。                                                                                                                                                                |
| /baud {9600&#124; 19200&#124; 38400&#124; 57600&#124; 115200} |                                                                                                                                                               デバッグに使用するボーレートを指定します。 デバッグを無効にする場合は、 **/baud**パラメーターを使用しないでください。                                                                                                                                                                |
|                     /id <OSEntryLineNum>                      |                                                                                                               デバッグオプションを追加する Boot.ini ファイルの [オペレーティングシステム] セクションのオペレーティングシステムエントリの行番号を指定します。 [オペレーティングシステム] セクションヘッダーの後の最初の行は1です。                                                                                                                |
|                              /?                               |                                                                                                                                                                                                       コマンド プロンプトでヘルプを表示します。                                                                                                                                                                                                        |

##### <a name="remarks"></a>コメント
- 1394ポートのデバッグが必要な場合は、 [bootcfg dbg1394](bootcfg-dbg1394.md)を使用します。
  ## <a name="examples"></a><a name=BKMK_examples></a>例
  次の例は、 **bootcfg/debug**コマンドを使用する方法を示しています。
  ```
  bootcfg /debug on /port com1 /id 2 
  bootcfg /debug edit /port com2 /baud 19200 /id 2 
  bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /debug off /id 2
  ```
  ## <a name="additional-references"></a>その他の参照情報
  - [コマンド ライン構文の記号](command-line-syntax-key.md)
