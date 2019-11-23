---
title: diskperf
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 829f0284d761e6a5134011fa1dff99646d55fc13
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377810"
---
# <a name="diskperf"></a>diskperf



Windows 2000 では、物理ディスクと論理ディスクのパフォーマンスカウンターは既定では有効になっていません。

**Diskperf**は、windows XP、windows server 2003、windows server 2008、windows Vista、windows Server 2008 R2、および windows 7 に含まれています。これにより、windows 2000 を実行しているコンピューターで物理ディスクまたは論理ディスクのパフォーマンスカウンターをリモートで有効または無効にすることができます。

## <a name="syntax"></a>構文

```
diskperf [-Y[D|V] | -N[D|V]] [\\computername]
```

## <a name="options"></a>オプション

|構成方法|説明|
|------|-----------|
|-?|状況依存のヘルプを表示します。|
|-Y|コンピューターの再起動時に、すべてのディスクパフォーマンスカウンターを開始します。|
|-YD|コンピューターの再起動時に、物理ドライブのディスクパフォーマンスカウンターを有効にします。|
|-YV|コンピューターの再起動時に、論理ドライブまたは記憶域ボリュームのディスクパフォーマンスカウンターを有効にします。|
|-N|コンピューターの再起動時に、すべてのディスクパフォーマンスカウンターを無効にします。|
|-ND|コンピューターの再起動時に、物理ドライブのディスクパフォーマンスカウンターを無効にします。|
|-NV|コンピューターの再起動時に、論理ドライブまたは記憶域ボリュームのディスクパフォーマンスカウンターを無効にします。|
|\\\\ *\<computername >*|ディスクパフォーマンスカウンターを有効または無効にするコンピューターの名前を指定します。|