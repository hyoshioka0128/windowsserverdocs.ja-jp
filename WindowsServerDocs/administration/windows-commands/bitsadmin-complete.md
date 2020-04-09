---
title: bitsadmin complete
description: '**Bitsadmin complete**の Windows コマンドに関するトピックでは、ジョブを完了します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a5e86677-8f7b-43b3-929e-97706c57e7f1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 847f6e298ff9701064ce4e577c785f7fc78ea22c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850825"
---
# <a name="bitsadmin-complete"></a>bitsadmin complete

ジョブを完了します。 ダウンロードしたファイルは、このスイッチを使用するまで使用できません。 ジョブが転送済み状態に移行した後に、このスイッチを使用します。 それ以外の場合は、正常に転送されたファイルのみを使用できます。

## <a name="syntax"></a>構文

```
bitsadmin /complete <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| 送信 | ジョブの表示名または GUID。 |

## <a name="examples"></a><a name=BKMK_examples></a>例

ジョブの状態が [転送済み] になると、そのジョブ内のすべてのファイルが BITS によって正常に転送されます。 ただし、 **[完了]** スイッチを使用するまで、ファイルは使用できません。 

複数のジョブが*Mydownloadjob*を名前として使用する場合は、ジョブを一意に識別するために、 *mydownloadjob*をジョブの GUID に置き換える必要があります。

```
C:\>bitsadmin /complete myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)