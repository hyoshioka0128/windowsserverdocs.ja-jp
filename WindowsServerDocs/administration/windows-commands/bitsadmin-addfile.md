---
title: bitsadmin addfile
description: '**Bitsadmin addfile**の Windows コマンドに関するトピックでは、指定されたジョブにファイルを追加します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1b31aa93-0364-465b-af36-754968825989
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 330e79eb2ba5a824cea54094f64ceb6f9cfd66b9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850965"
---
# <a name="bitsadmin-addfile"></a>bitsadmin addfile

指定されたジョブにファイルを追加します。

## <a name="syntax"></a>構文

```
bitsadmin /AddFile <Job> <RemoteURL> <LocalName>
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| Job | ジョブの表示名または GUID。 |
| RemoteURL | サーバー上のファイルの URL。 |
| LocalName | ローカルコンピューター上のファイルの名前。 *LocalName*には、ファイルへの絶対パスが含まれている必要があります。 |

## <a name="examples"></a><a name=BKMK_examples></a>例

ジョブにファイルを追加します。 追加するファイルごとにこの呼び出しを繰り返します。 複数のジョブが*Mydownloadjob*を名前として使用する場合は、ジョブを一意に識別するために、 *mydownloadjob*をジョブの GUID に置き換える必要があります。

```
C:\>bitsadmin /addfile myDownloadJob http://downloadsrv/10mb.zip c:\10mb.zip
```

## <a name="additional-references"></a>その他の参照情報

- [コマンドライン構文のキー](command-line-syntax-key.md)&copy;