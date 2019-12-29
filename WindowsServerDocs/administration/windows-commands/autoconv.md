---
title: autoconv
description: '**Autoconv**の Windows コマンドに関するトピックでは、ファイルアロケーションテーブル (Fat) および Fat32 ボリュームを NTFS ファイルシステムに変換します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 17281e54-0b18-4e84-94ac-24586c82df4e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bf36be6bcf3dd8f6c61c6ab0d8780ed77dd8903a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383446"
---
# <a name="autoconv"></a>autoconv

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ファイルアロケーションテーブル (Fat) および Fat32 ボリュームを NTFS ファイルシステムに変換します。これにより、 **autochk**が実行された後も、既存のファイルやディレクトリはそのまま残ります。 NTFS ファイルシステムに変換されたボリュームは、Fat または Fat32 に変換することはできません。
## <a name="remarks"></a>コメント
コマンドラインで**autoconv**を実行することはできません。 このは、 **convert.exe**を使用して設定した場合にのみ、スタートアップ時に実行されます。
## <a name="additional-references"></a>その他の参照情報
[コマンドライン構文のキー](command-line-syntax-key.md)
[autochk](autochk.md)
[Convert](convert.md)
[ファイルシステムの操作](https://go.microsoft.com/fwlink/?LinkId=4509)
