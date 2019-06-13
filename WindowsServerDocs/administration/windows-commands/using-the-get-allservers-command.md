---
title: Get AllServers コマンドを使用してください。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fe2e3c69-8f2e-457d-af55-d249ebf70f53
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dbccb834f9058f2c3cca097cdf998455f2a6892e
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440494"
---
# <a name="using-the-get-allservers-command"></a>Get AllServers コマンドを使用してください。



すべての Windows 展開サービス サーバーに関する情報を取得します。

> [!NOTE]
> このコマンドは、期間を延長環境内で多くの Windows 展開サービス サーバーがある場合、または、サーバーのリンクのネットワーク接続速度が遅い場合の所要時間をかかる場合があります。

## <a name="syntax"></a>構文

```
WDSUTIL [Options] /Get-AllServers /Show:{Config | Images | All} [/Detailed] [/Forest:{Yes | No}]
```

## <a name="parameters"></a>パラメーター

|   パラメーター   |                                                                                                                 説明                                                                                                                  |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /Show:{Config |                                                                                                                    画像                                                                                                                    |
|  [/詳細]  | 組み合わせて使用すると、 **/Show:Images** または **/Show:All**, 、すべてのイメージの各イメージからメタデータを返します。 場合、 **詳細/** オプションを指定しない場合、既定の動作は、イメージの名前、説明、およびファイル名を返す。 |
| []、[フォレスト: {[はい] |                                                                                                                     No}]                                                                                                                     |

## <a name="BKMK_examples"></a>例

すべてのサーバーに関する情報を表示するには、次のように入力します。
```
WDSUTIL /Get-AllServers /Show:Config
```
すべてのサーバーに関する詳細情報を表示するには、次のように入力します。
```
WDSUTIL /Verbose /Get-AllServers /Show:All /Detailed /Forest:Yes
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)