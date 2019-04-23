---
title: bdehdcfg driveinfo
description: 'Windows コマンド」のトピック * * bdehdcfg: * * - driveinfo ドライブ文字、合計サイズ、最大の空き領域、およびパーティションの特性を表示します。'
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f2d065e7-eced-4509-a1a0-ee2521a7f02e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4aa041c27b1797e7d00476212887a7dc6dbc1880
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889063"
---
# <a name="bdehdcfg-driveinfo"></a>bdehdcfg: driveinfo

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ドライブ文字、合計サイズ、最大の空き領域、およびパーティションの特性が表示されます。 有効なパーティションのみが一覧表示されます。 4 つのプライマリまたは拡張パーティションが既に存在する場合は、未割り当て領域は表示されません。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。
## <a name="syntax"></a>構文
```
bdehdcfg -driveinfo <DriveLetter>
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|<DriveLetter>|コロンの後にドライブ文字を指定します。|
## <a name="remarks"></a>注釈
このコマンドは情報ですし、ドライブに変更は行われない。
## <a name="BKMK_Examples"></a>例
次の例では、C ドライブのドライブ情報が表示されます。
```
bdehdcfg  driveinfo C:
```
## <a name="additional-references"></a>その他の参照
-   [コマンドライン構文キー](command-line-syntax-key.md)
-   [bdehdcfg](bdehdcfg.md)
