---
title: ntbackup
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6bce6b0d-646b-46b6-b833-0ff1d6f082c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ba3aaaa192283e0e1dc1777a27fc13973949784b
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723481"
---
# <a name="ntbackup"></a>ntbackup



Windows Vista または Windows Server 2008 では、 **ntbackup**コマンドは使用できません。 代わりに、 **wbadmin**コマンドとサブコマンドを使用して、コマンドプロンプトからコンピューターとファイルをバックアップおよび復元する必要があります。

**Wbadmin**で作成したバックアップは、wbadmin を使用**して回復**することはできません。 ただし、 **ntbackup のバージョンは、** **ntbackup**を使用して作成したバックアップを回復する Windows Server 2008 および windows Vista ユーザーのダウンロードとして入手できます。 このダウンロード可能なバージョンの**ntbackup**を使用すると、従来のバックアップの回復のみを実行でき、windows Server 2008 または windows Vista を実行しているコンピューターで新しいバックアップを作成することはできません。 このバージョンの**ntbackup**をダウンロードするに[https://go.microsoft.com/fwlink/?LinkId=82917](https://go.microsoft.com/fwlink/?LinkId=82917)は、「」を参照してください。

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

[Wbadmin](wbadmin.md)