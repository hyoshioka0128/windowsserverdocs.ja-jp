---
title: regsvr32
description: Regsvr32 コマンドのリファレンス記事。レジストリのコマンドコンポーネントとして .dll ファイルを登録します。
ms.topic: article
ms.assetid: 3345e964-7d3e-42b8-abeb-42ed6edfe2b2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8a591813480163a6d43329222d20e2a29651f576
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87883882"
---
# <a name="regsvr32"></a>regsvr32

レジストリ内のコマンド コンポーネントとして .dll ファイルを登録します。

## <a name="syntax"></a>構文

```
regsvr32 [/u] [/s] [/n] [/i[:cmdline]] <Dllname>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| /U | サーバーの登録を解除します。 |
| /s | メッセージが表示されないようにします。 |
| /n | **DllRegisterServer**を呼び出さないようにします。 このパラメーターでは、 **/i**パラメーターも使用する必要があります。 |
| /i`<cmdline>` | 省略可能なコマンドライン文字列を渡します (*cmdline*) に **DllInstall**します。 このパラメーターを **/u**パラメーターと共に使用すると、 **dlluninstall**が呼び出されます。 |
| `<Dllname>` | 登録される .dll ファイルの名前。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

### <a name="examples"></a>例

Active Directory スキーマの .dll ファイルを登録するには、次のように入力します。

```
regsvr32 schmmgmt.dll
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
