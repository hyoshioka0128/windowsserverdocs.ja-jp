---
title: bitsadmin addfile
description: Windows コマンド」のトピック**bitsadmin addfile** -指定されたジョブにファイルを追加します。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 1c3027bdc4f3f8f3e3ca50400b2c5dbf33bf2bc5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861753"
---
# <a name="bitsadmin-addfile"></a>bitsadmin addfile

指定したジョブには、ファイルを追加します。

## <a name="syntax"></a>構文

```
bitsadmin /AddFile <Job> <RemoteURL> <LocalName>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|RemoteURL|サーバー上のファイルの URL。|
|LocalName|ローカル コンピューター上のファイルの名前。 *LocalName*ファイルへの絶対パスを含める必要があります。|

## <a name="BKMK_examples"></a>例

ジョブにファイルを追加します。 各ファイルを追加するには、この呼び出しを繰り返します。 複数のジョブを使用して場合*myDownloadJob*という名前で置き換える必要がある*myDownloadJob*ジョブを一意に識別するために、ジョブの GUID を持つ。
```
C:\>bitsadmin /addfile myDownloadJob http://downloadsrv/10mb.zip c:\10mb.zip
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)