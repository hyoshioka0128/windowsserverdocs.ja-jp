---
title: mqbkup
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7bdd41c4-75ef-455f-b241-1d64a4c7acf5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a809bfc788ba25afab280e80e5c6f0dc9c70dc86
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842903"
---
# <a name="mqbkup"></a>mqbkup

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

上の MSMQ メッセージ ファイルとレジストリ設定、記憶域デバイスにバックアップし、以前に格納されているメッセージと設定を復元します。   
バックアップと復元操作の両方では、ローカルの MSMQ サービスは停止します。 MSMQ サービスが開始された事前ユーティリティは、バックアップまたは復元操作の最後に、MSMQ サービスを再起動しようとします。 サービスは、このユーティリティを実行する前に既に停止されている場合、サービスを再起動する処理は行われません。  
MSMQ メッセージのバックアップ/復元ユーティリティを使用する前に MSMQ を使用しているすべてのローカル アプリケーションを閉じる必要があります。  
## <a name="syntax"></a>構文  
```  
mqbkup {/b | /r} <folder path_to_storage_device>  
```  
### <a name="parameters"></a>パラメーター  
|パラメーター|説明|  
|-------|--------|  
|/b|バックアップ操作を指定します|  
|/r|復元操作を指定します|  
|< フォルダー path_to_storage\_デバイス >|MSMQ メッセージ ファイルとレジストリ設定が格納されているパスを指定します|  
|/?|コマンド プロンプトにヘルプを表示します。|  
## <a name="BKMK_Examples"></a>例  
すべての MSMQ メッセージ ファイルとレジストリ設定をバックアップおよびに保存する、 *Msmqbkup* c: ドライブ上のフォルダー。  
```  
mqbkup /b c:\msmqbkup  
```  
指定したフォルダーが存在しない場合、ユーティリティに自動的に作成されます。 既存のフォルダーを指定する場合は、このフォルダーを空にする必要があります。 空でないフォルダーを指定する場合、すべてのファイルとそれに含まれるサブフォルダーに、ユーティリティが削除されます。 この場合、既存のファイルとサブフォルダーを削除する権限を付与するように求めするは。 使用することができます、 **/y**パラメーターをすべての既存のファイルと、指定したフォルダー内のサブフォルダーの削除にあらかじめ同意を示します。  
すべてのファイルとサブフォルダーを削除する、 *Oldbkup* c: ドライブとストアの MSMQ メッセージ ファイルとレジストリの設定をこのフォルダー内のフォルダー。  
```  
mqbkup /b /y c:\oldbkup  
```  
MSMQ メッセージとレジストリ設定を復元するには。  
```  
mqbkup /r c:\msmqbkup  
```  
MSMQ メッセージ ファイルを格納するために使用するフォルダーの場所は、レジストリに格納されます。 そのため、ユーティリティは、レジストリで指定されたフォルダーおよび復元操作の前に使用されるストレージ フォルダーが、MSMQ メッセージのファイルが復元されます。 レジストリで指定したフォルダーが存在しない場合、復元操作が自動的に作成します。 フォルダーのディレクトリが存在して、空ではない場合は、ユーティリティは、次のフォルダーの現在の内容を削除するアクセス許可を求められます。  
## <a name="additional-references"></a>その他の参照  
-   [コマンドライン構文キー](command-line-syntax-key.md)  
