---
title: 手順 3 は、展開を確認します。
description: このトピックでは、リモート Windows Server 2016 での Directaccess の管理ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a78a078-d2e7-4cbd-b8d5-20cfb6d1524b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 89b9e53b7321ebeddda50a448829ad73395eeed0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835613"
---
# <a name="step-3-verify-the-deployment"></a>手順 3 は、展開を確認します。

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、DirectAccess クライアントのリモート管理のために、配置が正しく構成されていることを確認する方法について説明します。  
  
### <a name="to-verify-proper-deployment"></a>適切なデプロイを確認するには  
  
1.  DirectAccess クライアント コンピューターを企業ネットワークに接続し、グループ ポリシー オブジェクトを取得します。  
  
2.  クライアント コンピューターでは、クリックして、**ネットワーク接続**DirectAccess のメディア マネージャーにアクセスする通知領域にアイコン。  
  
3.  をクリックして**DirectAccess 接続**、状態が表示されます、**ローカル接続されている**します。  
  
4.  企業ネットワークからコンピューターを削除し、パブリック ネットワークに接続します。  
  
5.  コマンド プロンプトで「 **nltest/dsgetdc: [完全修飾ドメイン名]** します。 このコマンドは、企業ネットワークがクライアントにアクセスできることを確認します。 ドメイン コント ローラーにアクセスできない場合は、ドメインが存在しないレポート、次のエラー メッセージが表示されます。ERROR_NO_SUCH_DOMAIN します。  
  


