---
title: ksetup setcomputerpassword
description: Ksetup setcomputerpassword コマンドのリファレンストピック。ローカルコンピューターのパスワードを設定します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e307d8f6-3b93-4c24-ac04-f31549f7dc7d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1ec410cd85c13cb3a925c3fc65b8c9f86fba606a
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83817432"
---
# <a name="ksetup-setcomputerpassword"></a>ksetup setcomputerpassword

ローカルコンピューターのパスワードを設定します。 このコマンドはコンピューターアカウントのみに影響し、パスワードの変更を有効にするには再起動が必要です。

> [!IMPORTANT]
> コンピューターアカウントのパスワードは、レジストリまたは**ksetup**コマンドからの出力として表示されません。

## <a name="syntax"></a>構文

```
ksetup /setcomputerpassword <password>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<password>` | ローカルコンピューターでコンピューターアカウントを設定するために、指定されたパスワードを指定します。 パスワードは、管理者特権を持つアカウントを使用してのみ設定できます。パスワードは、1 ~ 156 の英数字または特殊文字にする必要があります。 |

### <a name="examples"></a>例

ローカルコンピューターのコンピューターアカウントのパスワードを*IPops897*から*ipop $ 897!* に変更するには、次のように入力します。

```
ksetup /setcomputerpassword IPop$897!
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [ksetup コマンド](ksetup.md)
