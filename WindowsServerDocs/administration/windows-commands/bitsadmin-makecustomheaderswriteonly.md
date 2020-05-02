---
title: bitsadmin makecustomheaderswriteonly
description: Bitsadmin makecustomheaderswriteonly コマンドのリファレンストピックです。これにより、ジョブのカスタム HTTP ヘッダーが書き込み専用になります。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 2aeab7e0ee7797b3e0be7be1156920f3bafc84dc
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717404"
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

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブに対して、カスタム HTTP ヘッダーを書き込み専用にするには、次のようにします。

```
bitsadmin /makecustomheaderswriteonly myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
