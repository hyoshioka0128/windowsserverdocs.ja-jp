---
title: bitsadmin addfile
description: '**Bitsadmin addfile**の Windows コマンドに関するトピックでは、指定されたジョブにファイルを追加します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b31aa93-0364-465b-af36-754968825989
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8dfddda92e506dbfca2a47394a310edf16fe78aa
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382045"
---
# <a name="bitsadmin-addfile"></a>bitsadmin addfile

指定されたジョブにファイルを追加します。

## <a name="syntax"></a>構文

```
bitsadmin /AddFile <Job> <RemoteURL> <LocalName>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|RemoteURL|サーバー上のファイルの URL。|
|LocalName|ローカルコンピューター上のファイルの名前。 *LocalName*には、ファイルへの絶対パスが含まれている必要があります。|

## <a name="BKMK_examples"></a>例

ジョブにファイルを追加します。 追加するファイルごとにこの呼び出しを繰り返します。 複数のジョブが*Mydownloadjob*を名前として使用する場合は、ジョブを一意に識別するために、 *mydownloadjob*をジョブの GUID に置き換える必要があります。
```
C:\>bitsadmin /addfile myDownloadJob http://downloadsrv/10mb.zip c:\10mb.zip
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)