---
title: bitsadmin setdisplayname
description: Windows コマンド」のトピック**bitsadmin setdisplayname** -指定したジョブの表示名を設定します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 13706c53-fb5f-4879-b5ca-82531361d6e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d50cd2785e42b554cee340abc97fe4e4b53adcfc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843673"
---
# <a name="bitsadmin-setdisplayname"></a>bitsadmin setdisplayname



指定したジョブの表示名を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /SetDisplayName <Job> <DisplayName>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|DisplayName|指定したジョブの表示名を使用するテキスト。|

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブの表示名を設定する*myDownloadJob*に*myDownloadJob2*します。
```
C:\>bitsadmin /SetDisplayName myDownloadJob "Download Music Job"
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)