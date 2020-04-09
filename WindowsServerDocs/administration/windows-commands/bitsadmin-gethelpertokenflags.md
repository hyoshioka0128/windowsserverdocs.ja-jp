---
title: bitsadmin gea pertokenflags
description: Windows コマンドに関するトピックでは、BITS 転送ジョブに関連付けられているヘルパートークンの使用フラグを返す**bitsadmin geの pertokenflags**について説明しています。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 37e40ea1f71795e0c975988169577deb205c3335
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850665"
---
# <a name="bitsadmin-gethelpertokenflags"></a>bitsadmin gea pertokenflags

BITS 転送ジョブに関連付けられている  [ヘルパートークン](https://docs.microsoft.com/windows/win32/bits/helper-tokens-for-bits-transfer-jobs)の使用フラグを返します。

> [!NOTE]
> このコマンドは、BITS 3.0 以前ではサポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /gethelpertokenflags <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| 送信 | ジョブの表示名または GUID。 |

## <a name="remarks"></a>コメント

次のような戻り値が返される可能性があります。

- **0x0001.** ヘルパートークンは、アップロードジョブのローカルファイルを開き、ダウンロードジョブの一時ファイルを作成または名前を変更するため、またはアップロード/応答ジョブの応答ファイルを作成または名前を変更するために使用されます。

- **0x0002.** ヘルパートークンは、サーバーメッセージブロック (SMB) のアップロードジョブまたはダウンロードジョブのリモートファイルを開くため、または暗黙の NTLM または Kerberos 資格情報に対する HTTP サーバーまたはプロキシのチャレンジに対する応答として使用されます。 資格情報が HTTP 経由で送信されるようにするには、/SetCredentialsJob TargetScheme NULL NULL を呼び出す必要があります。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
