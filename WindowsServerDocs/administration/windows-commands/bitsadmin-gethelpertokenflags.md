---
title: bitsadmin gethelpertokenflags
description: BITS 転送ジョブに関連付けられているヘルパートークンの使用フラグを返す、bitsadmin geの pertokenflags コマンドの参照記事。
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: d49a2aef829b3e443ad5e1fd3e70d8c260f59ec8
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894241"
---
# <a name="bitsadmin-gethelpertokenflags"></a>bitsadmin gethelpertokenflags

BITS 転送ジョブに関連付けられている [ヘルパートークン](/windows/win32/bits/helper-tokens-for-bits-transfer-jobs)の使用フラグを返し   ます。

> [!NOTE]
> このコマンドは、BITS 3.0 以前ではサポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /gethelpertokenflags <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

### <a name="remarks"></a>Remarks

次のような戻り値が返される可能性があります。

- **0x0001.** ヘルパートークンは、アップロードジョブのローカルファイルを開き、ダウンロードジョブの一時ファイルを作成または名前を変更するため、またはアップロード/応答ジョブの応答ファイルを作成または名前を変更するために使用されます。

- **0x0002.** ヘルパートークンは、サーバーメッセージブロック (SMB) のアップロードジョブまたはダウンロードジョブのリモートファイルを開くため、または暗黙の NTLM または Kerberos 資格情報に対する HTTP サーバーまたはプロキシのチャレンジに対する応答として使用されます。  `/SetCredentialsJob TargetScheme NULL NULL`   資格情報が HTTP 経由で送信されるようにするには、を呼び出す必要があります。

## <a name="examples"></a>例

*Mydownloadjob*という名前の BITS 転送ジョブに関連付けられているヘルパートークンの使用フラグを取得するには、次のようにします。

```
bitsadmin /gethelpertokenflags myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
