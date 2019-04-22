---
title: bitsadmin ピアキャッシュと setconfigurationflags
description: Windows コマンド」のトピック**bitsadmin ピアキャッシュと setconfigurationflags** -コンピューターがコンテンツをピアに使用できるし、ピアからコンテンツをダウンロードできるかどうかを決定する構成フラグを設定します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ff0a2b49-66e3-4d40-824c-6a3816055d2e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 22408d4aab7f5ea374511bc16751d911a84644f2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813333"
---
# <a name="bitsadmin-peercaching-and-setconfigurationflags"></a>bitsadmin ピアキャッシュと setconfigurationflags



コンピューターがコンテンツをピアに使用できるし、ピアからコンテンツをダウンロードできるかどうかを決定する構成フラグを設定します。

## <a name="syntax"></a>構文

```
bitsadmin /PeerCaching /SetConfigurationFlags <Job> <Value>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|値|値は、バイナリ表現内のビットの次の解釈では、次の符号なし整数です。</br>ピアからダウンロードするジョブのデータを許可します。最下位ビットを設定します。</br>ピアに提供するジョブのデータを許可します。右から 2 番目のビットを設定します。|

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブのピアからダウンロードするジョブのデータを指定します。 *myJob*します。
```
C:\> Bitsadmin /PeerCaching /SetConfigurationFlags myJob 1
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)