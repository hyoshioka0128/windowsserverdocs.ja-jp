---
title: tasklist
description: ローカルコンピューターまたはリモートコンピューターで実行されているプロセスの一覧を表示する方法について説明します。
ms.topic: article
ms.assetid: 8dbe30ee-1484-46be-917b-5ca3ff4fdc9c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a4f87c4cc2dc80c67e2004c929fa23aea8791fb9
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87881814"
---
# <a name="tasklist"></a>tasklist

ローカル コンピューターまたはリモート コンピューター上で現在実行中のプロセスの一覧を表示します。 **Tasklist** 置き換えます、 **tlist** ツールです。



## <a name="syntax"></a>構文

```
tasklist [/s <Computer> [/u [<Domain>\]<UserName> [/p <Password>]]] [{/m <Module> | /svc | /v}] [/fo {table | list | csv}] [/nh] [/fi <Filter> [/fi <Filter> [ ... ]]]
```

### <a name="parameters"></a>パラメーター

|          パラメーター           |                                                                                                                                            説明                                                                                                                                             |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|        /s\<Computer>        |                                                                                         名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定値はローカル コンピューターです。                                                                                         |
| u\<Domain>\\\]\<UserName> | ユーザー*名*または*ドメイン*ユーザー名で指定されたユーザーのアカウントアクセス許可を使用してコマンドを実行し \* <em>ます。 \* \*/u</em>は \* 、 **/s**が指定されている場合にのみ指定できます。 既定では、コマンドを発行しているコンピューターに現在ログオンしているユーザーのアクセス許可です。 |
|        /p\<Password>        |                                                                                                       指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。                                                                                                        |
|         /m\<Module>         |                                                               読み込まれた DLL モジュールを指定したパターンの名前に一致するすべてのタスクを一覧表示します。 モジュール名が指定されていない場合、このオプションは、各タスクによって読み込まれたすべてのモジュールを表示します。                                                                |
|             /svc             |                                                                                    切り捨てることがなく、各プロセスのすべてのサービス情報を一覧表示します。 有効な場合に、 **/fo** にパラメーターが設定されている **テーブル**します。                                                                                    |
|              /v              |                                                                                 出力に詳細なタスクの情報を表示します。 切り捨てることがなく完全な詳細な出力を使用して **/v** と **/svc** 化します。                                                                                 |
|  /fo {テーブル \| 一覧の \| csv}  |                                                                             使用して、出力形式を指定します。 有効な値は **テーブル**, 、**リスト**, 、および **csv**します。 出力の既定の形式は**table**です。                                                                             |
|             /nh              |                                                                                             出力に列ヘッダーを抑制します。 **/Fo**パラメーターが**table**または**csv**に設定されている場合に有効です。                                                                                              |
|        /fi\<Filter>         |                                                                          含めることも、クエリから除外するプロセスの種類を指定します。 有効なフィルター名、演算子、および値については、次の表を参照してください。                                                                          |
|              /?              |                                                                                                                                コマンド プロンプトにヘルプを表示します。                                                                                                                                |

### <a name="filter-names-operators-and-values"></a>フィルター名、演算子、および値

| フィルター名 |    有効な演算子     |                                                                 有効な値                                                                 |
|-------------|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|   状態    |         eq、ne         |                                                                   RUNNING                                                                    |
|  IMAGENAME  |         eq、ne         |                                                                  イメージ名                                                                  |
|     PID     | eq、ne、gt、lt、ge、le |                                                                  PID 値                                                                   |
|   SESSION   | eq、ne、gt、lt、ge、le |                                                                セッション番号                                                                |
| セッション名 |         eq、ne         |                                                                 [セッション名]                                                                 |
|   CPU 時間] 値   | eq、ne、gt、lt、ge、le | CPU 時間の形式で <em>HH</em>**:**<em>MM</em>**:**<em>SS</em>, ここで、 *MM* と *SS* 0 ~ 59 の間、および *HH* 符号なしのいずれかの数は、 |
|  MEMUSAGE   | eq、ne、gt、lt、ge、le |                                                              メモリの使用量 (KB 単位)                                                              |
|  USERNAME   |         eq、ne         |                                                             任意の有効なユーザー名                                                              |
|  サービス   |         eq、ne         |                                                                 サービス名                                                                 |
| WINDOWTITLE |         eq、ne         |                                                                 ウィンドウのタイトル                                                                 |
|   モジュール   |         eq、ne         |                                                                   DLL 名                                                                   |

## <a name="remarks"></a>Remarks

リモート システムが指定されているときに、WINDOWTITLE と状態のフィルターはサポートされていません。

## <a name="examples"></a><a name="BKMK_examples"></a>例

プロセス id が 1000 を超えるすべてのタスクの一覧を CSV 形式で表示するには、次のように入力します。
```
tasklist /v /fi "PID gt 1000" /fo csv
```
現在実行されているシステム プロセスを一覧表示するには、次のように入力します。
```
tasklist /fi "USERNAME ne NT AUTHORITY\SYSTEM" /fi "STATUS eq running"
```
現在実行されているすべてのプロセスの詳細情報を一覧表示するには、次のように入力します。
```
tasklist /v /fi "STATUS eq running"
```
"Srvmain"を"ntdll"で始まるを DLL 名を持つリモート コンピューター上のプロセスのすべてのサービス情報を一覧表示するには、次のように入力します。
```
tasklist /s srvmain /svc /fi "MODULES eq ntdll*"
```
"Srvmain、"、現在ログオンしているユーザー アカウントの資格情報を使用してリモート コンピューター上のプロセスを一覧表示するには、次のように入力します。
```
tasklist /s srvmain
```
"Srvmain、"Hiropln、ユーザー アカウントの資格情報を使用してリモート コンピューター上のプロセスを一覧表示するには、次のように入力します。
```
tasklist /s srvmain /u maindom\hiropln /p p@ssW23
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)