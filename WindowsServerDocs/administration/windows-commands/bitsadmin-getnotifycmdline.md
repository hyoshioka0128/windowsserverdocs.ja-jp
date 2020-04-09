---
title: bitsadmin getnotifycmdline
description: '**Bitsadmin getnotifycmdline**の Windows コマンドトピックでは、ジョブがデータの転送を終了したときに実行されるコマンドラインコマンドを取得します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 90fa33e6-aca5-4a23-82bd-19a9f13f8416
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 24b49b3fa0c2dafb999d8cb9c6e0c13ae68bf6f4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850595"
---
# <a name="bitsadmin-getnotifycmdline"></a>bitsadmin getnotifycmdline

ジョブがデータの転送を終了したときに実行するコマンドラインコマンドを取得します。

> [!NOTE]
> このコマンドは、BITS 1.2 以前ではサポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /getnotifycmdline <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| 送信 | ジョブの表示名または GUID。 |

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブが完了すると、サービスによって使用されるコマンドラインコマンドを取得します。

```
C:\>bitsadmin /getnotifycmdline myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)