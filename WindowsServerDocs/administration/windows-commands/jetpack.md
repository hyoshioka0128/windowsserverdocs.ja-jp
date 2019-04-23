---
title: jetpack
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: a3bffc29519df139921bdb1de53e67acd558b306
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858013"
---
# <a name="jetpack"></a>jetpack

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows インターネット ネーム サービス (WINS) または動的ホスト構成プロトコル (DHCP) のデータベースが圧縮されます。 マイクロソフトでは、30 MB に近づくたびに、WINS データベースを最適化することをお勧めします。 

## <a name="syntax"></a>構文
```
jetpack.EXE <database name> <temp database name>
```

### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|<database name>|元のデータベース ファイルを指定します。|
|<temp database name>|一時データベース ファイルを指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="BKMK_Examples"></a>例
WINS データベースを最適化します。
```
cd %SYSTEMROOT%\SYSTEM32\WINS
NET STOP WINS
jetpack WINS.MDB TMP.MDB
NET start WINS
```
DHCP データベースを最適化します。
```
cd %SYSTEMROOT%\SYSTEM32\DHCP
NET STOP DHCPSERver
jetpack DHCP.MDB TMP.MDB
NET start DHCPSERver
```
上記の例では**Tmp.mdb** jetpack.exe で使用される一時データベースです。 **Wins.mdb**は WINS データベースです。 **Dhcp.mdb**は DHCP データベースです。
jetpack.exe 圧縮、WINS、または、次の手順を実行して DHCP データベース:
1.  データベースと呼ばれる一時データベース ファイルに情報をコピー **Tmp.mdb**します。
2.  元のデータベース ファイルを削除します**Wins.mdb**または**Dhcp.mdb**します。
3.  一時データベース ファイルを元のファイル名に変更します。

> [!NOTE]
> Jetpack.exe がで指定された名前の一時ファイルを作成、最適化プロセス中に、*一時データベース名*パラメーター。 最適化プロセスが完了すると、一時ファイルが削除されます。 WINS または DHCP 内の既存のファイルがないことを確認で指定された 1 つとして同じ名前のフォルダー、*一時データベース名*パラメーター。

## <a name="additional-references"></a>その他の参照
-   [コマンドライン構文キー](command-line-syntax-key.md)
