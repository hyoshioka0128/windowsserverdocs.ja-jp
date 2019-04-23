---
title: showmount
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 26acf24922e6ac53a5c902d65eb0f23bff0af93b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852353"
---
# <a name="showmount"></a>showmount

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

使用することができます**showmount**マウントされたディレクトリを表示します。  
  
## <a name="syntax"></a>構文  
```
showmount {-e|-a|-d} <Server>  
```

## <a name="description"></a>説明  
**Showmount**コマンド\-ライン ユーティリティで指定されたコンピューターに nfs サーバーからエクスポートされたマウントされているファイル システムに関する情報を表示する*Server*します。 場合*サーバー*が指定されていない**showmount**コンピューターに関する情報を表示しますが、 **showmount**コマンドを実行します。  
  
次のオプションのいずれかを指定する必要があります。  
  
- **\-e** -すべてのファイルのエクスポート サーバーでシステムが表示されます。  
- **\-** -すべてのネットワーク ファイル システムが表示されます\(NFS\)クライアントおよびマウントされている各サーバー上のディレクトリ。  
- **\-d** -NFS クライアントが現在マウントされているサーバー上のすべてのディレクトリを表示します。  
  
## <a name="see-also"></a>関連項目  
[サービス ネットワーク ファイル システム コマンドのリファレンス](services-for-network-file-system-command-reference.md)  