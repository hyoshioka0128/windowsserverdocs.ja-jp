---
title: bootcfg raw
description: Windows コマンド」のトピック**生 bootcfg** -オペレーティング システムのエントリを文字列として指定するオペレーティング システムの読み込みオプションを追加します、 **[オペレーティング システム]** Boot.ini ファイルのセクション。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3458749-b0a0-460f-a022-3ff199a71f27
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a68c59eb3a7018ba8a7c0c96b594f0ed68d914b9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841603"
---
# <a name="bootcfg-raw"></a>bootcfg raw

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

オペレーティング システムのエントリを文字列として指定するオペレーティング システムの読み込みオプションを追加します、 **[オペレーティング システム]** Boot.ini ファイルのセクション。

## <a name="syntax"></a>構文
```
bootcfg /raw [/s <computer> [/u <Domain>\<User> /p <Password>]] <OSLoadOptionsString> [/id <OSEntryLineNum>] [/a]
```
## <a name="parameters"></a>パラメーター
|用語|定義|
|----|-------|
|/s <computer>|名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。|
|/u <Domain> \\<User>|指定されたユーザーのアカウント権限でコマンドを実行<User>または<Domain> \\<User>します。 既定では現在のコマンドを実行するコンピューターのユーザー ログオンのアクセス許可です。|
|/p <Password>|指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。|
|<OSLoadOptionsString>|オペレーティング システム エントリに追加するオペレーティング システムの読み込みオプションを指定します。 これらのロード オプション、オペレーティング システム エントリに関連付けられている既存のロード オプションに置き換えられます。 検証なし<OSLoadOptions>は行われます。|
|/id <OSEntryLineNum>|更新する Boot.ini ファイルの [operating systems] セクションでは、オペレーティング システム エントリの行番号を指定します。 [オペレーティング システム] セクション ヘッダーの後の最初の行には 1 です。|
|/a|オペレーティング システムのオプションが追加されているが、既存のオペレーティング システムのオプションを追加することを指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|
##### <a name="remarks"></a>注釈
-   **bootcfg 生**既存のオペレーティング システム エントリのオプションを上書きする、オペレーティング システム エントリの末尾にテキストを追加するために使用します。 このテキストはなど、有効な OS ロード オプションを含める必要があります **/debug**、 **/fastdetect**、 **/nodebug**、 **/baudrate**、 **/なりません**、および **/sos**します。 たとえば、次のコマンドを追加します"**/debug/fastdetect**"最初のオペレーティング システム エントリのために、置換、以前のオペレーティング システム エントリのオプション。
    ```
    bootcfg /raw "/debug /fastdetect" /id 1
    ```
## <a name="BKMK_examples"></a>例
次の例を使用する方法、 **bootcfg/生**コマンド。
```
bootcfg /raw "/debug /sos" /id 2
bootcfg /raw /s srvmain /u maindom\hiropln /p p@ssW23 "/crashdebug " /id 2
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文キー](command-line-syntax-key.md)
