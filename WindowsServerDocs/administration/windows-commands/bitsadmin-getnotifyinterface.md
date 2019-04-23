---
title: bitsadmin getnotifyinterface
description: Windows コマンド」のトピック**bitsadmin getnotifyinterface** -別のプログラムに指定したジョブの COM のコールバック インターフェイスが登録されているかどうかを決定します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 40bf9dd8-b167-406a-80a6-a5a6f1b8cf7f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8316721a20cc477f9e8e15fc57b5d1c861da3ff4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868043"
---
# <a name="bitsadmin-getnotifyinterface"></a>bitsadmin getnotifyinterface

別のプログラムに指定したジョブの COM コールバック インターフェイス (通知インターフェイス) が登録されているかどうかを判断します。

## <a name="syntax"></a>構文

```
bitsadmin /GetNotifyInterface <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>注釈

登録または登録解除が表示されます。

> [!NOTE]
> コールバック インターフェイスが登録されているプログラムを特定することはできません。

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブの通知インターフェイスを取得する*myDownloadJob*します。
```
C:\>bitsadmin /GetNotifyInterface myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)