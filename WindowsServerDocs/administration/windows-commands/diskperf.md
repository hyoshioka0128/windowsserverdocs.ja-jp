---
title: diskperf
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f06916e8-069b-4ec8-a6eb-59f1d9f77111
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a99f18b56c9295e902a3c89e2e89b36c9c1b6c89
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852583"
---
# <a name="diskperf"></a>diskperf



Windows 2000 では、物理および論理ディスクのパフォーマンス カウンターは既定で有効にできません。

**Diskperf**リモートを有効にまたはを実行するコンピューターの論理または物理ディスクのパフォーマンス カウンターを無効にするために使用できるように、Windows XP、Windows Server 2003、Windows Server 2008、Windows Vista、Windows Server 2008 R2、および Windows 7 に含めるはWindows 2000 です。

## <a name="syntax"></a>構文

```
diskperf [-Y[D|V] | -N[D|V]] [\\computername]
```

## <a name="options"></a>オプション

|オプション|説明|
|------|-----------|
|-?|ヘルプ表示のコンテキストに依存します。|
|-Y|コンピューターを再起動すると、すべてのディスクのパフォーマンス カウンターを開始します。|
|-YD|コンピューターを再起動すると、物理ドライブのディスクのパフォーマンス カウンターを有効にします。|
|-YV|コンピューターを再起動すると、論理ドライブまたは記憶域ボリュームのディスク パフォーマンス カウンターを有効にします。|
|-N|コンピューターを再起動すると、すべてのディスクのパフォーマンス カウンターを無効にします。|
|-ND|コンピューターを再起動すると、物理ドライブのディスクのパフォーマンス カウンターを無効にします。|
|-NV|コンピューターを再起動すると、論理ドライブまたは記憶域ボリュームのディスク パフォーマンス カウンターを無効にします。|
|\\\\*\<computername>*|有効またはディスクのパフォーマンス カウンターを無効にコンピューターの名前を指定します。|