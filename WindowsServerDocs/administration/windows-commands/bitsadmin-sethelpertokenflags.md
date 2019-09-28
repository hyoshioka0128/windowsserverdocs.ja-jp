---
title: bitsadmin sea pertokenflags
description: '**Bitsadmin se pertokenflags**の Windows コマンドトピック-BITS 転送ジョブに関連付けられているヘルパートークンの使用フラグを設定します。'
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
ms.openlocfilehash: 6047c63677fac3311634ababb675be5301b7f3b5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380577"
---
# <a name="bitsadmin-sethelpertokenflags"></a>bitsadmin sea pertokenflags

BITS 転送ジョブに関連付けられている [ヘルパートークン](/windows/desktop/bits/helper-tokens-for-bits-transfer-jobs)  の使用フラグを設定します。

**BITS 3.0 以前**: サポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /SetHelperTokenFlags <Job> <Flags>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID。|
|フラグ|使用できる値は次のとおりです。 0x0001 @ no__t: ヘルパートークンを使用して、アップロードジョブのローカルファイルを開き、ダウンロードジョブの一時ファイルを作成または名前を変更するか、アップロード応答ジョブの応答ファイルを作成または名前を変更します。 0x0002 @ no__t ヘルパートークンは、サーバーメッセージブロック (SMB) のアップロードまたはダウンロードジョブのリモートファイルを開くため、または暗黙の NTLM または Kerberos 資格情報に対する HTTP サーバーまたはプロキシのチャレンジに対する応答として使用されます。 @ No__t-0 @ no__t-1to を呼び出す必要があります。これにより、資格情報を HTTP 経由で送信できるようになります。|

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)
