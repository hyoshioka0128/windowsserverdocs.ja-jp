---
title: bitsadmin sea pertokenflags
description: Bitsadmin se pertokenflags の Windows コマンドに関するトピックでは、BITS 転送ジョブに関連付けられているヘルパートークンの使用フラグを設定しています。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: c644e82026cfc1d62f3fb5d20e3925002b871036
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849495"
---
# <a name="bitsadmin-sethelpertokenflags"></a>bitsadmin sea pertokenflags

BITS 転送ジョブに関連付けられている  [ヘルパートークン](/windows/desktop/bits/helper-tokens-for-bits-transfer-jobs)の使用フラグを設定します。

**BITS 3.0 以前**: サポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /SetHelperTokenFlags <Job> <Flags>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID。|
|フラグ|使用できる値は次のとおりです。 0x0001&mdash;、ヘルパートークンを使用して、アップロードジョブのローカルファイルを開き、ダウンロードジョブの一時ファイルを作成または名前を変更するか、アップロード応答ジョブの応答ファイルを作成または名前を変更します。 0x0002&mdash;ヘルパートークンを使用して、サーバーメッセージブロック (SMB) のアップロードまたはダウンロードジョブのリモートファイルを開いたり、暗黙の NTLM または Kerberos 資格情報に対する HTTP サーバーまたはプロキシのチャレンジに応答したりします。 資格情報が HTTP 経由で送信されるようにするには、 `/SetCredentialsJob TargetScheme NULL NULL` を呼び出す必要があります。|

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
