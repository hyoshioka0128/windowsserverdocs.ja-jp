---
title: bitsadmin sei pertoken
description: '**Bitsadmin se pertoken**の Windows コマンドのトピック-現在のコマンドプロンプトのプライマリトークン (または、指定されている場合は任意のローカルユーザーアカウントのトークン) を BITS 転送ジョブのヘルパートークンとして設定します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 91c03366998168dad9ab4530ef36a5020b8ad6ec
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380568"
---
# <a name="bitsadmin-sethelpertoken"></a>bitsadmin sei pertoken

現在のコマンドプロンプトのプライマリトークン (または、指定されている場合は任意のローカルユーザーアカウントのトークン) を BITS 転送ジョブの [ヘルパートークン](/windows/desktop/bits/helper-tokens-for-bits-transfer-jobs)として設定します。

**BITS 3.0 以前**: サポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /SetHelperToken <Job> [\<username@domain\> \<password\>]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID。|
|\<username@domain\> \<パスワード\>|必要に応じて、使用するトークンを持つローカルユーザーアカウントの資格情報&mdash;ます。|

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)
