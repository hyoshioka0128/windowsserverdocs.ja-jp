---
title: showmount
description: マウントされたディレクトリを表示する showmount のリファレンス記事です。
ms.topic: article
ms.assetid: a6dd562e-e3bd-4ee6-be3b-6d29e29fd20e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0be623eadd56a55a87f2df57fec9b4c6558770c9
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87882403"
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

## <a name="see-also"></a>参照
[サービスがネットワーク ファイル システム コマンドのリファレンス](services-for-network-file-system-command-reference.md)