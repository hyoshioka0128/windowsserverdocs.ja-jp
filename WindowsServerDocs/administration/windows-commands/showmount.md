---
title: showmount
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a6dd562e-e3bd-4ee6-be3b-6d29e29fd20e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e1d197072db93130de880b5ec52d1875720b1d26
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383914"
---
# <a name="showmount"></a>showmount

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

**Showmount-** を使用して、マウントされたディレクトリを表示できます。  
  
## <a name="syntax"></a>構文  
```
showmount {-e|-a|-d} <Server>  
```

## <a name="description"></a>説明  
**Showmount-** コマンド\-line ユーティリティは、*サーバー*によって指定されたコンピューター上の NFS サーバーによってエクスポートされたマウントされたファイルシステムに関する情報を表示します。 *サーバー*が指定されていない場合、 **showmount-** コマンドを実行し**たコンピューター**に関する情報が表示されます。  
  
次のいずれかのオプションを指定する必要があります。  
  
- **\-e** -サーバーにエクスポートされたすべてのファイルシステムを表示します。  
- **\-a** -すべてのネットワークファイルシステム \(NFS\) クライアントと、サーバー上の各ディレクトリがマウントされているディレクトリを表示します。  
- **\-d** -NFS クライアントによって現在マウントされているサーバー上のすべてのディレクトリを表示します。  
  
## <a name="see-also"></a>参照  
[サービスがネットワーク ファイル システム コマンドのリファレンス](services-for-network-file-system-command-reference.md)  