---
title: nslookup root
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9c29edc3-ec49-43f2-bc49-86bf0612d816
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bc2952bdbf709c31d720a7fb57430429edf9feb1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59871913"
---
# <a name="nslookup-root"></a>nslookup root

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ドメイン ネーム システム (DNS) ドメインの名前空間のルートのサーバーに既定のサーバーを変更します。
## <a name="syntax"></a>構文
```
root 
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|{help &#124; ?}|簡単な概要を表示します。 **nslookup**サブコマンドします。|
## <a name="remarks"></a>注釈
-   現時点では、ns.nic.ddn.mil ネーム サーバーが使用されます。 このコマンドは、lserver ns.nic.ddn.mil のシノニムです。 使用して、ルート サーバーの名前を変更することができます、**セット ルート**コマンド。
## <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[nslookup ルートの設定](nslookup-set-root.md)
