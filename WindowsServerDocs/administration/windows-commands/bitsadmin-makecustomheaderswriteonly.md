---
title: bitsadmin makecustomheaderswriteonly
description: '**Bitsadmin makecustomheaderswriteonly**の Windows コマンドに関するトピックでは、ジョブのカスタム HTTP ヘッダーが書き込み専用になっています。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 9183b1b5de51020c5c6d2efad2c0a788d158a183
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850245"
---
# <a name="bitsadmin-makecustomheaderswriteonly"></a>bitsadmin makecustomheaderswriteonly

ジョブのカスタム HTTP ヘッダーを書き込み専用にします。

> [!Important]
> この操作を元に戻すことはできません。

## <a name="syntax"></a>構文

```
bitsadmin /makecustomheaderswriteonly <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| 送信 | ジョブの表示名または GUID。 |

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブに対して、カスタム HTTP ヘッダーを書き込み専用にします。

```
C:\>bitsadmin /makecustomheaderswriteonly myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)