---
title: bitsadmin sethelpertokenflags
description: Windows コマンド」のトピック**bitsadmin sethelpertokenflags** -BITS 転送ジョブに関連付けられているヘルパー トークンの使用法フラグを設定します。
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
ms.openlocfilehash: cc9652afe73476041aa42e64671885bfc1af9628
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813863"
---
# <a name="bitsadmin-sethelpertokenflags"></a>bitsadmin sethelpertokenflags

使用法フラグを設定、 [ヘルパー トークン](/windows/desktop/bits/helper-tokens-for-bits-transfer-jobs) BITS 転送ジョブに関連付けられています。

**3.0 と以前の BITS**: サポートされません。

## <a name="syntax"></a>構文

```
bitsadmin /SetHelperTokenFlags <Job> <Flags>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID。|
|フラグ|使用可能な値は、次に示します。 0x0001&mdash;アップロード ジョブのローカル ファイルを開く、作成またはダウンロード ジョブの一時ファイルの名前を変更するかを作成またはアップロード応答ジョブの応答ファイルの名前を変更するヘルパー トークンを使用します。 0x0002&mdash;ヘルパー トークンがサーバー メッセージ ブロック (SMB) のアップロードのリモート ファイルを開くか、ジョブをダウンロードするために使用または資格情報の暗黙的な NTLM または Kerberos の HTTP サーバーまたはプロキシ チャレンジに応答します。 呼び出す必要があります `/SetCredentialsJob TargetScheme NULL NULL` HTTP 経由で送信される資格情報を許可します。|

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)
