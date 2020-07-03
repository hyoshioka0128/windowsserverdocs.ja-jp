---
title: showmount
description: マウントされたディレクトリを表示する showmount のリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a6dd562e-e3bd-4ee6-be3b-6d29e29fd20e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 131ecf9dea650dd127e4dff05838245ceece1ead
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931605"
---
# <a name="showmount"></a>showmount

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

**Showmount-** を使用して、マウントされたディレクトリを表示できます。

## <a name="syntax"></a>構文
```
showmount {-e|-a|-d} <Server>
```

## <a name="description"></a>説明
**Showmount-** コマンド \- ラインユーティリティは、*サーバー*によって指定されたコンピューター上の NFS サーバーによってエクスポートされたマウントされたファイルシステムに関する情報を表示します。 *サーバー*が指定されていない場合、 **showmount-** コマンドを実行し**たコンピューター**に関する情報が表示されます。

次のいずれかのオプションを指定する必要があります。

- ** \- e** -サーバーにエクスポートされたすべてのファイルシステムを表示します。
- ** \- a** -すべてのネットワークファイルシステム \( NFS \) クライアントと、サーバー上の各ディレクトリがマウントされているディレクトリを表示します。
- ** \- d** -NFS クライアントによって現在マウントされているサーバー上のすべてのディレクトリを表示します。

## <a name="see-also"></a>関連項目
[サービスがネットワーク ファイル システム コマンドのリファレンス](services-for-network-file-system-command-reference.md)