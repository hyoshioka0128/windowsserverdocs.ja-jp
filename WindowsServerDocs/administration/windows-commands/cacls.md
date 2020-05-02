---
title: cacls
description: 指定されたファイルの随意アクセス制御リスト (DACL) を表示または変更する cacls コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b5bdbaaa-4557-48b8-80df-e75ee0d2f27d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d827199ea319bd41511f9abadfde8c6e8949976e
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82726024"
---
# <a name="cacls"></a>cacls

>[!IMPORTANT]
> このコマンドは非推奨とされました。 代わりに[icacls](icacls.md)を使用してください。  

指定されたファイルの随意アクセス制御リスト (DACL) を表示または変更します。  

## <a name="syntax"></a>構文

```  
cacls <filename> [/t] [/m] [/l] [/s[:sddl]] [/e] [/c] [/g user:<perm>] [/r user [...]] [/p user:<perm> [...]] [/d user [...]]  
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| --------- | ----------- |
| `<filename>` | 必須。 指定されたファイルの Acl を表示します。 |
| /t | 現在のディレクトリとすべてのサブディレクトリ内の指定されたファイルの Acl を変更します。 |
| /m | ディレクトリにマウントされているボリュームの Acl を変更します。 |
| /l | ターゲットではなく、シンボリックリンク自体に対して機能します。 |
| /s: sddl | Acl を SDDL 文字列で指定された Acl に置き換えます。 このパラメーターは、 **/e**、 **/g**、 **/r**、 **/p**、または **/d**パラメーターでは使用できません。 |
| /e | ACL を置き換えるのではなく、編集します。 |
| /c | アクセス拒否エラーの後に続行します。 |
| `/g user:<perm>` | 指定されたユーザーアクセス権を付与します。アクセス許可には、次の有効な値が含まれます。<ul><li>**n** -なし</li><li>**r** -読み取り</li><li>**w** -書き込み</li><li>**c** -変更 (書き込み)</li><li>**f** -フルコントロール</li></ul> |
| /r ユーザー [...] | 指定されたユーザーのアクセス権を取り消します。 **/E**パラメーターと共に使用する場合にのみ有効です。 |
| `[/p user:<perm> [...]` | 指定されたユーザーのアクセス権を置き換えます。アクセス許可には、次の有効な値が含まれます。<ul><li>**n** -なし</li><li>**r** -読み取り</li><li>**w** -書き込み</li><li>**c** -変更 (書き込み)</li><li>**f** -フルコントロール</li></ul> |
| [/d ユーザー [...] | 指定されたユーザーアクセスを拒否します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="sample-output"></a>サンプル出力

| 出力 | アクセス制御エントリ (ACE) はに適用されます |
-------- | ------------------------------------- |
| OI | オブジェクト継承。 このフォルダーとファイル。 |
| CI | コンテナーの継承。 このフォルダーとサブフォルダー。 |
| IO | 継承のみ。 ACE は、現在のファイルまたはディレクトリには適用されません。 |
| 出力メッセージがありません | このフォルダーのみです。 |
| OI項目 | このフォルダー、サブフォルダー、およびファイル。 |
| OI項目IO | サブフォルダーとファイルのみ。 |
| 項目IO | サブフォルダーのみです。 |
| OIIO | ファイルのみ。 |

#### <a name="remarks"></a>Remarks

- ワイルドカード (**?** と **&#42;**) を指定して、複数のファイルを指定します。

- 複数のユーザーを指定できます。  

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [icacls](icacls.md)
