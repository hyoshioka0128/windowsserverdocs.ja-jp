---
title: jetpack
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82a2b7ef-0db5-4575-a028-8acb0bf6c7ba
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b011658c6a745d62707cf88404379b17b0e05eef
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375323"
---
# <a name="jetpack"></a>jetpack

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows インターネットネームサービス (WINS) または動的ホスト構成プロトコル (DHCP) データベースを圧縮します。 Microsoft では、30 MB に近づいたときに WINS データベースを圧縮することをお勧めします。 

## <a name="syntax"></a>構文
```
jetpack.EXE <database name> <temp database name>
```

### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|<database name>|元のデータベースファイルを指定します。|
|<temp database name>|一時データベースファイルを指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="BKMK_Examples"></a>例
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
-   [コマンド ライン構文の記号](command-line-syntax-key.md)
