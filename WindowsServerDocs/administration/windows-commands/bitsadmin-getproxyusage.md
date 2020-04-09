---
title: bitsadmin getproxyusage
description: '**Bitsadmin getproxyusage**に関する Windows コマンドトピックでは、指定されたジョブのプロキシ使用法の設定を取得します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f940a70e-3b02-497e-a47f-b37b905c299e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 01c9bb9a1d413fa847482f652e18eed30ad76109
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850515"
---
# <a name="bitsadmin-getproxyusage"></a>bitsadmin getproxyusage

指定したジョブのプロキシ使用法の設定を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getproxyusage <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| 送信 | ジョブの表示名または GUID。 |

## <a name="remarks"></a>コメント

プロキシの使用には次の値が含まれます。

- **Preconfig** -所有者の Internet Explorer の既定値を使用します。

- **No_Proxy** -プロキシサーバーを使用しないでください。

- **Override** -明示的なプロキシリストを使用します。

- **自動**検出-プロキシ設定を自動的に検出します。

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブのプロキシの使用状況を取得します。

```
C:\>bitsadmin /getproxyusage myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)