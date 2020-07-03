---
title: bitsadmin sethelpertoken
description: Bitsadmin se pertoken コマンドの参照記事。このコマンドは、現在のコマンドプロンプトのプライマリトークン (または、指定されている場合は任意のローカルユーザーアカウントのトークン) を BITS 転送ジョブのヘルパートークンとして設定します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 21dee45610823cd70e8b7209ec99e080746316f9
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927781"
---
# <a name="bitsadmin-sethelpertoken"></a>bitsadmin sethelpertoken

現在のコマンドプロンプトのプライマリトークン (または、指定されている場合は任意のローカルユーザーアカウントのトークン) を BITS 転送ジョブの [ヘルパートークン](https://docs.microsoft.com/windows/win32/bits/helper-tokens-for-bits-transfer-jobs)として設定します。

> [!NOTE]
> このコマンドは、BITS 3.0 以前ではサポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /sethelpertoken <job> [<user_name@domain> <password>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| `<username@domain>` `<password>` | 任意。 使用するトークンのローカルユーザーアカウントの資格情報。 |

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
