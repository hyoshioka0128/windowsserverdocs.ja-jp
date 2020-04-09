---
title: auditpol
description: '**Auditpol**の Windows コマンドに関するトピックでは、に関する情報を表示し、監査ポリシーを操作する関数を実行します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a02cfb9d-732f-4e77-aeba-f18265daa3af
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 00365b0e46b8bff761cf991dbdbd09d8f5e9c687
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851135"
---
# <a name="auditpol"></a>auditpol

に関する情報を表示し、監査ポリシーを操作する関数を実行します。

このコマンドを使用する方法の例については、各トピックの「例」を参照してください。

## <a name="syntax"></a>構文

```
auditpol command [<sub-command><options>]
```

#### <a name="parameters"></a>パラメーター

| サブコマンド | 説明 |
| ----------- | ----------- |
| /get | 現在の監査ポリシーを表示します。 詳細については、「 [auditpol get](auditpol-get.md)の構文とオプション」を参照してください。 |
| /set | 監査ポリシーを設定します。 詳細については、「 [auditpol set](auditpol-set.md) for 構文 and options」を参照してください。 |
| /list | 選択可能なポリシー要素を表示します。 詳細については、「 [auditpol list](auditpol-list.md) for 構文 and options」を参照してください。 |
| /backup | 監査ポリシーをファイルに保存します。 詳細については、「 [auditpol バックアップ](auditpol-backup.md)」で構文とオプションを確認してください。 |
| /restore | Auditpol/backupを使用して以前に作成されたファイルから監査ポリシーを復元します。 詳細については、「構文とオプションについての[auditpol 復元](auditpol-restore.md)」を参照してください。 |
| /clear | 監査ポリシーをクリアします。 詳細については、「構文およびオプションに対する[auditpol clear](auditpol-clear.md) 」を参照してください。 |
| /remove | すべてのユーザーごとの監査ポリシー設定を削除し、すべてのシステム監査ポリシー設定を無効にします。 詳細については、「構文およびオプションに対する[auditpol の削除](auditpol-remove.md)」を参照してください。 |
| /resourcesacl | グローバルリソースシステムアクセス制御リスト (Sacl) を構成します。 **注:** Windows 7 および Windows Server 2008 R2 にのみ適用されます。 詳細については、「 [Auditpol resourceSACL](auditpol-resourcesacl.md)」を参照してください。 |
| /?| コマンド プロンプトでヘルプを表示します。 |

## <a name="remarks"></a>コメント

監査ポリシーのコマンドラインツールを使用すると、次のことができます。

- システム監査ポリシーを設定し、クエリを実行します。

- ユーザーごとの監査ポリシーを設定し、クエリを実行します。

- 監査オプションを設定および照会します。

- 監査ポリシーへのアクセスを委任するために使用されるセキュリティ記述子を設定および照会します。

- 監査ポリシーをレポートするか、コンマ区切り値 (CSV) テキストファイルにバックアップします。

- CSV テキストファイルから監査ポリシーを読み込みます。

- グローバルリソース Sacl を構成します。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)