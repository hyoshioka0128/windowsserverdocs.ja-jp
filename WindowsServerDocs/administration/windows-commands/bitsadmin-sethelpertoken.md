---
title: bitsadmin sethelpertoken
description: Windows コマンド」のトピック**bitsadmin sethelpertoken** -BITS 転送ジョブのヘルパー トークンとして現在のコマンド プロンプトのプライマリ トークン (または任意のローカル ユーザー アカウントのトークン、指定されている場合) を設定します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 558a1aca66a7b3ec447136ceff9237d13efe4ede
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853003"
---
# <a name="bitsadmin-sethelpertoken"></a>bitsadmin sethelpertoken

BITS 転送ジョブのとして現在のコマンド プロンプトのプライマリ トークン (または任意のローカル ユーザー アカウントのトークン、指定されている場合) を設定する [ヘルパー トークン](/windows/desktop/bits/helper-tokens-for-bits-transfer-jobs)します。

**3.0 と以前の BITS**: サポートされません。

## <a name="syntax"></a>構文

```
bitsadmin /SetHelperToken <Job> [\<username@domain\> \<password\>]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID。|
|\<username@domain\> \<パスワード\>|省略可能な&mdash;アカウントを使用するトークンのローカル ユーザーの資格情報。|

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)
