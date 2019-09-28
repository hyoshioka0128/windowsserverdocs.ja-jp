---
title: ntbackup
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6bce6b0d-646b-46b6-b833-0ff1d6f082c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ebbe71fd5547311beb36747d32d695823e0f0059
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372680"
---
# <a name="ntbackup"></a>ntbackup



Windows Vista または Windows Server 2008 では、 **ntbackup**コマンドは使用できません。 代わりに、 **wbadmin**コマンドとサブコマンドを使用して、コマンドプロンプトからコンピューターとファイルをバックアップおよび復元する必要があります。

**Wbadmin**で作成したバックアップは、wbadmin を使用**して回復**することはできません。 ただし、 **ntbackup のバージョンは、** **ntbackup**を使用して作成したバックアップを回復する Windows Server 2008 および windows Vista ユーザーのダウンロードとして入手できます。 このダウンロード可能なバージョンの**ntbackup**を使用すると、従来のバックアップの回復のみを実行でき、windows Server 2008 または windows Vista を実行しているコンピューターで新しいバックアップを作成することはできません。 このバージョンの**ntbackup**をダウンロードするには、 [https://go.microsoft.com/fwlink/?LinkId=82917](https://go.microsoft.com/fwlink/?LinkId=82917)を参照してください。

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)

[Wbadmin](wbadmin.md)