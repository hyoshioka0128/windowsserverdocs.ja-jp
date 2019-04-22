---
title: bitsadmin setpeercachingflags
description: Windows コマンド」のトピック**bitsadmin setpeercachingflags** -ジョブのファイルをキャッシュしてピアに提供し、ジョブは、ピアからコンテンツをダウンロードできる場合を決定するフラグを設定します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3f54a127-fb68-49a5-b843-664ec833df67
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2d50a6ccd83a6251808ca3d66437e52f641c60a7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814253"
---
# <a name="bitsadmin-setpeercachingflags"></a>bitsadmin setpeercachingflags



ピアからコンテンツの場合は、ジョブをダウンロードして、ジョブのファイルをキャッシュおよびピアに提供できる場合を決定するフラグを設定します。

## <a name="syntax"></a>構文

```
bitsadmin /SetPeerCachingFlags <Job> <value> 
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|値|値は、バイナリ表現内のビットの次の解釈で符号なし整数です。</br>1 - ジョブは、ピアからコンテンツをダウンロードできます。</br>2 - ジョブのファイルをキャッシュして、ピアに提供できます。|

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブのフラグを設定する*myJob*ピアからコンテンツをダウンロードすることができます。
```
C:\>bitsadmin / SetPeerCachingFlags myJob 1 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)