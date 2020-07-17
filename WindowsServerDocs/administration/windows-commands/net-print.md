---
title: net print
description: Net print コマンドの参照記事です。 このコマンドは非推奨とされており、Windows の将来のリリースでサポートされるとは限りません。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f59b2015-4698-415d-9a74-09566c466f40
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: af02ca14156c8a85ee54700983e2af6807752f91
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85934822"
---
# <a name="net-print"></a>net print

> [!IMPORTANT]
> このコマンドは非推奨とされました。 ただし、同じタスクの多くは、 [prnjobs.vbs コマンド](prnjobs.md)、 [Windows Management Instrumentation (WMI)](https://docs.microsoft.com/windows/win32/wmisdk/wmi-start-page)、 [Powershell での PRINTMANAGEMENT](https://docs.microsoft.com/powershell/module/printmanagement)、または[IT プロフェッショナル向けのスクリプトリソース](https://gallery.technet.microsoft.com/ScriptCenter/site/search?f%5B0%5D.Type=RootCategory&f%5B0%5D.Value=printing&f%5B0%5D.Text=Printing)を使用して実行できます。

指定された印刷キュー、または指定した印刷ジョブに関する情報を表示または指定した印刷ジョブを制御します。

## <a name="syntax"></a>構文

```
net print {\\<computername>\<sharename> | \\<computername> <jobnumber> [/hold | /release | /delete]} [help]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------- | ----------- |
| `\\<computername>\<sharename>` | 名前によって、情報を表示するコンピューターと印刷キューを指定します。 |
| `\\<computername>` | (名前) を制御する印刷ジョブをホストするコンピューターを指定します。 コンピューターを指定しない場合、ローカル コンピューターが使用されます。 必要があります、 `<jobnumber>` パラメーター。 |
| `<jobnumber>` | 制御する印刷ジョブの数を指定します。 この数は、印刷ジョブが送信された印刷キューをホストするコンピューターによって割り当てられます。 コンピューター後数がそのコンピュータがホストされている任意のキューにあるその他の印刷ジョブに割り当てられていないこと、印刷ジョブに番号を割り当てます。 使用する場合に必要な `\\<computername>` パラメーター。 |
| `[/hold | /release | /delete]` | 印刷ジョブで実行するアクションを指定します。 ジョブ番号を指定しても、何も指定しない場合は、印刷ジョブに関する情報が表示されます。<ul><li>**/hold**は、ジョブを遅延させ、他の印刷ジョブが解放されるまでそのジョブをバイパスできるようにします。</li><li>**/release** -遅延された印刷ジョブを解放します。</li><li>**/delete** -印刷キューから印刷ジョブを削除します。</li></ul> |
| help | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>注釈

- コマンドを実行すると、 `net print\\<computername>` 印刷ジョブに関する情報が共有プリンターキューに表示されます。 次に示すのは、*レーザー*という名前の共有プリンターのキューにあるすべての印刷ジョブのレポートの例です。

    ```
    printers at \\PRODUCTION
    Name              Job #      Size      Status
    -----------------------------
    LASER Queue       3 jobs               *printer active*
    USER1          84        93844      printing
    USER2          85        12555      Waiting
    USER3          86        10222      Waiting
    ```

- 印刷ジョブに対してレポートの例を次に示します。

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

### <a name="examples"></a>例

* \\ 実稼働*コンピューター上の*dotmatrix*印刷キューの内容を一覧表示するには、次のように入力します。

```
net print \\Production\Dotmatrix
```

* \\ 実稼働*コンピューター上のジョブ番号*35*に関する情報を表示するには、次のように入力します。

```
net print \\Production 35
```

* \\ 実稼働*コンピューターでジョブ番号*263*を遅延させるには、次のように入力します。

```
net print \\Production 263 /hold
```

* \\ 実稼働*コンピューターでジョブ番号*263*を解放するには、次のように入力します。

```
net print \\Production 263 /release
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [印刷コマンドのリファレンス](print-command-reference.md)

- [prnjobs.vbs コマンド](prnjobs.md)

- [Windows Management Instrumentation (WMI)](https://docs.microsoft.com/windows/win32/wmisdk/wmi-start-page)

- [Powershell での PrintManagement](https://docs.microsoft.com/powershell/module/printmanagement)

- [IT プロフェッショナル向けのスクリプトリソース](https://gallery.technet.microsoft.com/ScriptCenter/site/search?f%5B0%5D.Type=RootCategory&f%5B0%5D.Value=printing&f%5B0%5D.Text=Printing)
