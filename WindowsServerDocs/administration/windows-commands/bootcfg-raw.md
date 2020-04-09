---
title: bootcfg raw
description: Bootcfg raw の Windows コマンドに関するトピック。文字列として指定されたオペレーティングシステムの読み込みオプションを、boot.ini ファイルのオペレーティングシステムセクションのオペレーティングシステムエントリに追加します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e3458749-b0a0-460f-a022-3ff199a71f27
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fd5137187c5ba1dc1b410d728f1c2930ddcbc3cc
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848515"
---
# <a name="bootcfg-raw"></a>bootcfg raw

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Boot.ini ファイルの **[オペレーティングシステム]** セクションのオペレーティングシステムエントリに、文字列として指定されたオペレーティングシステムの読み込みオプションを追加します。

## <a name="syntax"></a>構文
```
bootcfg /raw [/s <computer> [/u <Domain>\<User> /p <Password>]] <OSLoadOptionsString> [/id <OSEntryLineNum>] [/a]
```
### <a name="parameters"></a>パラメーター

|         用語          |                                                                                                            Definition                                                                                                             |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     /s <computer>     |                                                        名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。                                                         |
| /u <Domain> \\<User>  |               <User> または <Domain>\\<User>によって指定されたユーザーのアカウントアクセス許可を使用してコマンドを実行します。 既定値は、コマンドを実行しているコンピューターの現在のログオンユーザーのアクセス許可です。                |
|     /p <Password>     |                                                                       指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。                                                                       |
| <OSLoadOptionsString> | オペレーティングシステムエントリに追加するオペレーティングシステムの読み込みオプションを指定します。 これらの読み込みオプションは、オペレーティングシステムエントリに関連付けられている既存の読み込みオプションを置き換えます。 <OSLoadOptions> の検証は行われません。 |
| /id <OSEntryLineNum>  |                       更新する Boot.ini ファイルの [オペレーティングシステム] セクションにあるオペレーティングシステムエントリの行番号を指定します。 [オペレーティングシステム] セクションヘッダーの後の最初の行は1です。                       |
|          /a           |                                                       追加するオペレーティングシステムオプションを既存のオペレーティングシステムオプションに追加することを指定します。                                                        |
|          /?           |                                                                                               コマンド プロンプトでヘルプを表示します。                                                                                                |

##### <a name="remarks"></a>コメント
- **bootcfg raw**は、オペレーティングシステムエントリの末尾にテキストを追加し、既存のオペレーティングシステムの入力オプションを上書きするために使用されます。 このテキストに**は、有効**な OS 読み込みオプション ( **/debug**、 **/fastdetect**、 **/nodebug**、 **/crashdebug**、 **/sos**など) が含まれている必要があります。 たとえば、次のコマンドは、最初のオペレーティングシステムエントリの最後に **/debug/fastdetect**を追加して、以前のオペレーティングシステムエントリのオプションを置き換えます。
  ```
  bootcfg /raw /debug /fastdetect /id 1
  ```
  ## <a name="examples"></a><a name=BKMK_examples></a>例
  次の例は、 **bootcfg/raw**コマンドを使用する方法を示しています。
  ```
  bootcfg /raw /debug /sos /id 2
  bootcfg /raw /s srvmain /u maindom\hiropln /p p@ssW23 /crashdebug  /id 2
  ```
  ## <a name="additional-references"></a>その他の参照情報
  - [コマンド ライン構文の記号](command-line-syntax-key.md)
