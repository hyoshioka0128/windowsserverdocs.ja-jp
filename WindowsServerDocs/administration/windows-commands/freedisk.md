---
title: freedisk
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 91c15166-5baa-4b80-9e0c-4cd815d00530
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 138d637ba3da983ccb931d489f7c22b651e07a0c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817223"
---
# <a name="freedisk"></a>freedisk

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

インストール処理を続行する前に、ディスク領域の指定した量が使用可能なかどうかを確認します。

## <a name="syntax"></a>構文
```
freedisk [/s <computer> [/u [<Domain>\]<User> [/p [<Password>]]]] [/d <Drive>] [<Value>]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/s <computer>|名前またはリモート コンピューターの IP アドレスを指定します (円記号を使用しない)。 既定はローカル コンピュータです。 このパラメーターは、すべてのファイルと、コマンドで指定したフォルダーに適用されます。|
|/u [<Domain>\\]<User>|指定したユーザー アカウントのアクセス許可を持つ、スクリプトを実行します。 既定ではシステムのアクセス許可です。|
|/p [<Password>]|指定されているユーザー アカウントのパスワードを指定します **/u**します。|
|/d <Drive>|空き領域の可用性を確認するドライブを指定します。 指定する必要があります<Drive>リモート コンピューターをします。|
|<Value>|特定の空きディスク領域の容量を確認します。 指定できます。 <Value>KB、MB、GB、TB、PB、EB、ZB または YB バイト。|
## <a name="remarks"></a>注釈
-   使用して、 **/s**、 **/u**、および **/p**コマンド ライン オプションを使用する場合のみ使用可能な **/s**します。 使用する必要があります **/p**で **/u**ユーザーのパスワードを指定します。
-   無人インストールの場合、使用することができます**freedisk**でインストールを続行する前に前提条件となる量の空き領域をチェックするバッチ ファイルをインストールします。
-   使用すると**freedisk**バッチ ファイルで返されます、 **0**十分な領域がある場合、 **1**十分な領域がない場合。
## <a name="BKMK_examples"></a>例
ないか調べ、少なくとも 50 MB の空き領域の使用可能な c: ドライブに、次のように入力します。
```
freedisk 50mb 
```
画面上には、次のような出力が表示されます。
```
INFO: The specified 52,428,800 byte(s) of free space is available on current drive.
```
## <a name="additional-references"></a>その他の参照
[コマンドライン構文キー](command-line-syntax-key.md)
