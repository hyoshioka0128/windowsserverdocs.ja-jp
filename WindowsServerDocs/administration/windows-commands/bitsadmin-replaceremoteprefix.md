---
title: bitsadmin replaceremoteprefix
description: '**Bitsadmin replaceremoteprefix**の Windows コマンドに関するトピック。これにより、必要に応じて、ジョブ内のすべてのファイルのリモート URL が*oldprefix*から*newprefix*に変更されます。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d0e0abb1-bdb4-4c74-abbc-16c809f5fd81
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0cea0108a292815e31e893e91dc4079305c1da9a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849815"
---
# <a name="bitsadmin-replaceremoteprefix"></a>bitsadmin replaceremoteprefix

必要に応じて、ジョブ内のすべてのファイルのリモート URL を*oldprefix*から*newprefix*に変更します。

## <a name="syntax"></a>構文

```
bitsadmin /replaceremoteprefix <job> <oldprefix> <newprefix>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| 送信 | ジョブの表示名または GUID。 |
| oldprefix | 既存の URL プレフィックス。 |
| newprefix | 新しい URL プレフィックス。 |

## <a name="examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブに含まれるすべてのファイルのリモート URL を *http://stageserver* から *http://prodserver* に変更します。

```
C:\>bitsadmin /replaceremoteprefix myDownloadJob http://stageserver http://prodserver
```

## <a name="additional-information"></a>追加情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)