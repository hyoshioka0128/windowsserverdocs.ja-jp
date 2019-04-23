---
title: bitsadmin gethelpertokenflags
description: Windows コマンド」のトピック**bitsadmin gethelpertokenflags** -BITS 転送ジョブに関連付けられているヘルパー トークンの使用法フラグを返します。
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
ms.openlocfilehash: e5665ed4670891dcbecd56215342f3d94e1ed753
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885793"
---
# <a name="bitsadmin-gethelpertokenflags"></a>bitsadmin gethelpertokenflags

使用法フラグを返します、 [ヘルパー トークン](/windows/desktop/bits/helper-tokens-for-bits-transfer-jobs) BITS 転送ジョブに関連付けられています。

**3.0 と以前の BITS**: サポートされません。

## <a name="syntax"></a>構文

```
bitsadmin /GetHelperTokenFlags <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>注釈

有効な戻り値は、次に示します。

- 0x0001 します。 ヘルパーのトークンを使用して、アップロード ジョブを作成したり、ダウンロードしたジョブの一時ファイルの名前を変更または作成またはアップロード応答ジョブの応答ファイルの名前を変更するのローカル ファイルを開きます。
- 0x0002 します。 ヘルパー トークンは、サーバー メッセージ ブロック (SMB) のアップロードのリモート ファイルを開くか、ジョブをダウンロードするために使用または資格情報の暗黙的な NTLM または Kerberos の HTTP サーバーまたはプロキシ チャレンジに応答します。 SetCredentialsJob TargetScheme NULL NULL HTTP 経由で送信される資格情報を許可するを呼び出す必要があります。

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)
