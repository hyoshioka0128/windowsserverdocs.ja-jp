---
title: autoconv
description: ファイルアロケーションテーブル (Fat) および Fat32 ボリュームを NTFS ファイルシステムに変換する autoconv コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 17281e54-0b18-4e84-94ac-24586c82df4e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ea8f55270435c6632be2e527569b4a4b4ca81136
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718772"
---
# <a name="autoconv"></a>autoconv

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ファイルアロケーションテーブル (Fat) および Fat32 ボリュームを NTFS ファイルシステムに変換します。これにより、 **autochk**が実行された後も、既存のファイルやディレクトリはそのまま残ります。 NTFS ファイルシステムに変換されたボリュームは、Fat または Fat32 に変換することはできません。

> [!IMPORTANT]
> コマンドラインから**autoconv**を実行することはできません。 このは、 **convert.exe**を使用して設定した場合にのみ、スタートアップ時に実行できます。

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [autochk コマンド](autochk.md)

- [convert コマンド](convert.md)
