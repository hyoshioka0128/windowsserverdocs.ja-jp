---
title: jetpack
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 82a2b7ef-0db5-4575-a028-8acb0bf6c7ba
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 008e9dd4d41fe270d775b1c44d799dd16429046f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841975"
---
# <a name="jetpack"></a>jetpack

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows インターネットネームサービス (WINS) または動的ホスト構成プロトコル (DHCP) データベースを圧縮します。 Microsoft では、30 MB に近づいたときに WINS データベースを圧縮することをお勧めします。 

## <a name="syntax"></a>構文
```
jetpack.EXE <database name> <temp database name>
```

#### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|<database name>|元のデータベースファイルを指定します。|
|<temp database name>|一時データベースファイルを指定します。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="examples"></a><a name=BKMK_Examples></a>例
WINS データベースを圧縮するには、次のようにします。
```
cd %SYSTEMROOT%\SYSTEM32\WINS
NET STOP WINS
jetpack WINS.MDB TMP.MDB
NET start WINS
```
DHCP データベースを圧縮するには:
```
cd %SYSTEMROOT%\SYSTEM32\DHCP
NET STOP DHCPSERver
jetpack DHCP.MDB TMP.MDB
NET start DHCPSERver
```
上記の例で、 **Tmp**は、jetpack によって使用される一時データベースです。 **Wins-a**は wins データベースです。 **Dhcp**は dhcp データベースです。
jetpack は、次の手順に従って、WINS または DHCP データベースを圧縮します。
1.  データベース情報を**Tmp**という名前の一時データベースファイルにコピーします。
2.  元のデータベースファイル ( **wins-a**または**Dhcp .mdb**) を削除します。
3.  一時データベースファイルの名前を元のファイル名に変更します。

> [!NOTE]
> 圧縮処理中に、jetpack によって一時*データベース名*パラメーターで指定された名前の一時ファイルが作成されます。 一時ファイルは、コンパクトプロセスが完了すると削除されます。 WINS または DHCP フォルダーに既に存在するファイルが、 *temp データベース名*パラメーターに指定されている名前と同じでないことを確認します。

## <a name="additional-references"></a>その他の参照情報
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
