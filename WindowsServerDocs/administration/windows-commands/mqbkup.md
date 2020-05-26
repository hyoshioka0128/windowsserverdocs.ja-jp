---
title: mqbkup
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7bdd41c4-75ef-455f-b241-1d64a4c7acf5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bcd31ba6fd2a85c00e7c684f4aeec12c4899c259
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820832"
---
# <a name="mqbkup"></a>mqbkup

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

MSMQ メッセージファイルとレジストリ設定をストレージデバイスにバックアップし、以前に保存されたメッセージと設定を復元します。
バックアップと復元の両方の操作で、ローカル MSMQ サービスが停止されます。 MSMQ サービスが事前に開始されている場合、ユーティリティは、バックアップまたは復元操作の最後に MSMQ サービスの再起動を試みます。 ユーティリティを実行する前にサービスが既に停止していた場合、サービスの再起動は行われません。
MSMQ メッセージのバックアップ/復元ユーティリティを使用する前に、MSMQ を使用しているすべてのローカルアプリケーションを閉じる必要があります。
## <a name="syntax"></a>構文
```
mqbkup {/b | /r} <folder path_to_storage_device>
```
#### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/b|バックアップ操作を指定します|
|/r|復元操作を指定します|
|<フォルダー path_to_storage \_ デバイス>|MSMQ メッセージファイルとレジストリ設定が格納されるパスを指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|
## <a name="examples"></a>例
すべての MSMQ メッセージファイルとレジストリ設定をバックアップし、C: ドライブの*Msmqbkup*フォルダーに保存します。
```
mqbkup /b c:\msmqbkup
```
指定したフォルダーが存在しない場合は、ユーティリティによって自動的に作成されます。 既存のフォルダーを指定する場合は、このフォルダーを空にする必要があります。 空ではないフォルダーを指定すると、ユーティリティは、そのフォルダー内に含まれるすべてのファイルとサブフォルダーを削除します。 この場合、既存のファイルとサブフォルダーを削除するアクセス許可を付与するように求められます。 **/Y**パラメーターを使用して、指定したフォルダー内の既存のすべてのファイルとサブフォルダーの削除に対して事前に同意したことを示すことができます。
C: ドライブの*Oldbkup*フォルダーにあるすべてのファイルとサブフォルダーを削除し、MSMQ メッセージファイルとレジストリ設定をこのフォルダーに格納します。
```
mqbkup /b /y c:\oldbkup
```
MSMQ メッセージとレジストリ設定を復元するには:
```
mqbkup /r c:\msmqbkup
```
MSMQ メッセージファイルの格納に使用されるフォルダーの場所は、レジストリに格納されます。 このため、ユーティリティは、復元操作の前に使用されていたストレージフォルダーではなく、レジストリで指定されているフォルダーに MSMQ メッセージファイルを復元します。 レジストリに指定されているフォルダーが存在しない場合は、復元操作によって自動的に作成されます。 フォルダーディレクトリが存在し、空でない場合は、これらのフォルダーの現在の内容を削除するためのアクセス許可を求めるメッセージが表示されます。
## <a name="additional-references"></a>その他のリファレンス
- [コマンド ライン構文の記号](command-line-syntax-key.md)
