---
title: bitsadmin getnotifyflags
description: '**Bitsadmin getnotifyflags**の Windows コマンドに関するトピックでは、指定されたジョブの通知フラグを取得します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d4657e6c-8959-4db7-a4af-e73d3f80ecf8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3138baea05f793cfb587d3f8fb669d446daea6b5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850585"
---
# <a name="bitsadmin-getnotifyflags"></a>bitsadmin getnotifyflags

指定されたジョブの通知フラグを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getnotifyflags <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| 送信 | ジョブの表示名または GUID。 |

## <a name="remarks"></a>コメント

ジョブには、次の1つまたは複数の通知フラグを含めることができます。

| Flag | 説明 |
| ----- | ----- |
| 0x001 | ジョブ内のすべてのファイルが転送されたときにイベントを生成します。 |
| 0x002 | エラーが発生したときにイベントを生成します。 |
| 0x004 | 通知を無効にします。 |
| 0x008 | ジョブが変更されたとき、または転送の進行状況が発生したときにイベントを生成します。 |

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブの通知フラグを取得します。

```
C:\>bitsadmin /getnotifyflags myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)