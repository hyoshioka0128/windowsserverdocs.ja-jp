---
title: ftp 追加
description: Ftp append コマンドのリファレンストピック。現在のファイルの種類の設定を使用して、リモートコンピューター上のファイルにローカルファイルを追加します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7c1a133c-31dc-41a4-9eb9-258efd79804d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7d1b6ab4a6ae0c1654d4335d24f135b2893bdcb7
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83819142"
---
# <a name="ftp-append"></a>ftp 追加

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

現在のファイルの種類の設定を使用して、リモートコンピューター上のファイルにローカルファイルを追加します。

## <a name="syntax"></a>構文

```
append <localfile> [remotefile]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<localfile>` | 追加するローカルファイルを指定します。 |
| remotefile | を追加するリモートコンピューター上のファイルを指定し <localfile> ます。 このパラメーターを使用しない場合は、 `<localfile>` リモートファイル名の代わりに名前が使用されます。 |

### <a name="examples"></a>例

リモートコンピューター上の*file2*に*file1*を追加するには、次のように入力します。

```
append file1.txt file2.txt
```

ローカルの*file1*をリモートコンピューター上の*file1*という名前のファイルに追加します。

```
append file1.txt
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [追加の FTP ガイダンス](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
