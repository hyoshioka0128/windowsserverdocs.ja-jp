---
title: マウント
description: Network File System (NFS) ネットワーク共有をマウントする mount コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: dd9d7ecb-ef00-4aaa-bcd0-423fa636e34a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 823b88b8ab1168776c25e05e3dbf5ec08d784724
ms.sourcegitcommit: 5e313a004663adb54c90962cfdad9ae889246151
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84354562"
---
# <a name="mount"></a>マウント

ネットワークファイルシステム (NFS) ネットワーク共有をマウントするコマンドラインユーティリティ。 オプションや引数を指定せずに**マウント**すると、マウントされているすべての NFS ファイルシステムに関する情報が表示されます。

> [!NOTE]
> このユーティリティは **、NFS クライアント**がインストールされている場合にのみ使用できます。

## <a name="syntax"></a>構文

```
mount [-o <option>[...]] [-u:<username>] [-p:{<password> | *}] {\\<computername>\<sharename> | <computername>:/<sharename>} {<devicename> | *}
```

### <a name="parameters"></a>パラメーター

| パラメーター  | 説明 |
| ---------- | ----------- |
| -o の場合は、`<buffersize>` | 読み取りバッファーのサイズを kb 単位で設定します。 使用できる値は1、2、4、8、16、および32です。既定値は 32 KB です。 |
| -o wsize =`<buffersize>` | 書き込みバッファーのサイズを kb 単位で設定します。 使用できる値は1、2、4、8、16、および32です。既定値は 32 KB です。 |
| -o timeout =`<seconds>` | リモートプロシージャコール (RPC) のタイムアウト値を秒単位で設定します。 使用可能な値は、0.8、0.9、および範囲1-60 の任意の整数です。既定値は0.8 です。 |
| -o retry =`<number>` | ソフトマウントの再試行回数を設定します。 許容される値は、1-10 の範囲の整数です。既定値は1です。 |
| -o mtype =`{soft|hard}` | NFS 共有のマウントの種類を設定します。 既定では、Windows はソフトマウントを使用します。 接続の問題があると、ソフトマウントの時間がより簡単になります。ただし、NFS サーバーの再起動中の i/o 中断を減らすために、ハードマウントを使用することをお勧めします。|
| -o anon | 匿名ユーザーとしてマウントします。 |
| -o nolock | ロックを無効にします (既定値は**有効**です)。 |
| -o casesensitive | サーバー上のファイル参照を強制的に大文字と小文字を区別します。 |
| -o fileaccess =`<mode>` | NFS 共有で作成された新しいファイルの既定のアクセス許可モードを指定します。 *Ogw*の形式で、3桁の数字として*mode*を指定します。ここで、 *o*、 *g*、および*w*はそれぞれ、ファイルの所有者、グループ、および世界に与えられたアクセス権を表す数字です。 次のような数字が0-7 の範囲に含まれている必要があります。<ul><li>**0:** アクセスなし</li><li>**1:** x (実行アクセス)</li><li>**2:** w (書き込みアクセス)</li><li>**3:** wx (書き込みおよび実行アクセス)</li><li>**4:** r (読み取りアクセス)</li><li>**5:** rx (読み取りおよび実行アクセス)</li><li>**6:** rw (読み取りおよび書き込みアクセス)</li><li>**7:** rwx (読み取り、書き込み、実行アクセス)</li></ul> |
| -o lang =`{euc-jp|euc-tw|euc-kr|shift-jis|Big5|Ksc5601|Gb2312-80|Ansi)` | NFS 共有で構成する言語エンコードを指定します。 共有で使用できる言語は1つだけです。 この値には、次のいずれかの値を含めることができます。<ul><li>**euc-jp:** 日本語</li><li>**euc-tw:** 中国語</li><li>**韓国:** 韓国語</li><li>**シフト jis:** 日本語</li><li>**Big5:** 中国語</li><li>**Ksc5601:** 韓国語</li><li>**Gb2312-80:** 簡体字中国語</li><li>**Ansi:** ANSI エンコード</li></ul> |
| u`<username>` | 共有のマウントに使用するユーザー名を指定します。 *ユーザー名*の前に円記号 (*) が付いていない場合は *\** 、UNIX ユーザー名として扱われます。 |
| irtran-p`<password>` | 共有をマウントするために使用するパスワード。 アスタリスク (**&#42;**) を使用すると、パスワードの入力を求めるメッセージが表示されます。 |
| `<computername>` | NFS サーバーの名前を指定します。 |
| `<sharename>` | ファイル システムの名前を指定します。 |
| `<devicename>` | デバイスのドライブ文字と名前を指定します。 アスタリスク (**&#42;**) を使用する場合、この値は使用可能な最初のドライバー文字を表します。 |

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
