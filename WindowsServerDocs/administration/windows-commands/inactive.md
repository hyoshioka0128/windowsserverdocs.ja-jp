---
title: 非アクティブ
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4fb4695-4e66-4166-b4ab-2c86a4605580
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9c8ded732d984830c7892720f75938979f1abb67
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438165"
---
# <a name="inactive"></a>非アクティブ



ベーシック マスター ブート レコード (MBR) ディスクにシステム パーティションまたはブート パーティションを非アクティブにフォーカスをマークします。

## <a name="syntax"></a>構文

```
inactive
```

## <a name="remarks"></a>注釈

> [!CAUTION]
> アクティブ パーティションがないコンピューターが起動しない可能性があります。 Windows ファミリのオペレーティング システムの理解と経験を積んだユーザーでない限り、非アクティブとしてシステムまたはブート パーティションを設定できません。</br>> CD-ROM ドライブに Windows セットアップ CD を挿入システムまたはブート パーティションを非アクティブとしてマークした後にコンピューターを起動されない場合、コンピューターを再起動しを使用して、パーティションを修復し、 **fixmbr**と**fixboot**回復コンソールのコマンド。
> -   システム パーティションまたはブート パーティションを非アクティブとしてマークするには、CD-ROM ドライブまたは Pre-boot eXecution Environment (PXE) など、BIOS で指定された次のオプションからお使いのコンピューターが開始されます。
> -   この操作を成功させるのには、アクティブなシステムまたはブート パーティションを選択してください。 使用して、**パーティションを選択**コマンドをアクティブなパーティションを選択し、それにフォーカスをします。

## <a name="BKMK_examples"></a>例

```
inactive
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)

