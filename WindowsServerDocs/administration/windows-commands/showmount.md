---
title: showmount
description: マウントされたディレクトリを表示する showmount の Windows コマンドに関するトピック。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a6dd562e-e3bd-4ee6-be3b-6d29e29fd20e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6fa61d47bb14cf21d93beec0a6e9257b9f66737b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834225"
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