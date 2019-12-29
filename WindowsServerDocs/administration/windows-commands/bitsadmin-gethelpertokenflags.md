---
title: bitsadmin gea pertokenflags
description: '**Bitsadmin ge pertokenflags**の Windows コマンドのトピック-BITS 転送ジョブに関連付けられているヘルパートークンの使用フラグを返します。'
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
ms.openlocfilehash: 25d667736d5fdcd018f557b2a5565b94898f6e51
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381568"
---
# <a name="bitsadmin-gethelpertokenflags"></a>bitsadmin gea pertokenflags

BITS 転送ジョブに関連付けられている  [ヘルパートークン](/windows/desktop/bits/helper-tokens-for-bits-transfer-jobs)の使用フラグを返します。

**BITS 3.0 以前**: サポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /GetHelperTokenFlags <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>注釈

返される戻り値には、次のようなものがあります。

- 0x0001. ヘルパートークンは、アップロードジョブのローカルファイルを開き、ダウンロードジョブの一時ファイルを作成または名前を変更するため、またはアップロード/応答ジョブの応答ファイルを作成または名前を変更するために使用されます。
- 0x0002. ヘルパートークンは、サーバーメッセージブロック (SMB) のアップロードジョブまたはダウンロードジョブのリモートファイルを開くため、または暗黙の NTLM または Kerberos 資格情報に対する HTTP サーバーまたはプロキシのチャレンジに対する応答として使用されます。 資格情報が HTTP 経由で送信されるようにするには、/SetCredentialsJob TargetScheme NULL NULL を呼び出す必要があります。

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)
