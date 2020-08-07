---
title: bitsadmin makecustomheaderswriteonly
description: Bitsadmin makecustomheaderswriteonly コマンドの参照記事です。これにより、ジョブのカスタム HTTP ヘッダーが書き込み専用になります。
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: b1e152ee51f3009a5cc1f5bf1b747e65e86e5e04
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893691"
---
# <a name="bitsadmin-makecustomheaderswriteonly"></a>bitsadmin makecustomheaderswriteonly

ジョブのカスタム HTTP ヘッダーを書き込み専用にします。

> [!IMPORTANT]
> この操作を元に戻すことはできません。

## <a name="syntax"></a>構文

```
bitsadmin /makecustomheaderswriteonly <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブに対して、カスタム HTTP ヘッダーを書き込み専用にするには、次のようにします。

```
bitsadmin /makecustomheaderswriteonly myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
