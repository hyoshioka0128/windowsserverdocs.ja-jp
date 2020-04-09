---
title: bitsadmin sei pertoken
description: Bitsadmin se pertoken の Windows コマンドに関するトピックでは、現在のコマンドプロンプトのプライマリトークン (または、指定されている場合は任意のローカルユーザーアカウントのトークン) を BITS 転送ジョブのヘルパートークンとして設定します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: a1e8fd0054cadf3bf06b6e5b7bdf5010b18781e1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849535"
---
# <a name="bitsadmin-sethelpertoken"></a>bitsadmin sei pertoken

現在のコマンドプロンプトのプライマリトークン (または、指定されている場合は任意のローカルユーザーアカウントのトークン) を BITS 転送ジョブの [ヘルパートークン](/windows/desktop/bits/helper-tokens-for-bits-transfer-jobs)として設定します。

**BITS 3.0 以前**: サポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /SetHelperToken <Job> [\<username@domain\> \<password\>]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID。|
|\<username@domain\> \<パスワード\>|必要に応じて、使用するトークンを持つローカルユーザーアカウントの資格情報&mdash;ます。|

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
