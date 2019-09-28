---
title: 手順 3. 展開を確認する
description: このトピックは、「Windows Server 2016 で DirectAccess クライアントをリモート管理する」ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a78a078-d2e7-4cbd-b8d5-20cfb6d1524b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 81ac8bf7321df915330d8d706fa5ba3912b8f54c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71367297"
---
# <a name="step-3-verify-the-deployment"></a>手順 3. 展開を確認する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、DirectAccess クライアントのリモート管理の展開が正しく構成されていることを確認する方法について説明します。  
  
### <a name="to-verify-proper-deployment"></a>適切な展開を検証するには  
  
1.  DirectAccess クライアントコンピューターを企業ネットワークに接続し、グループポリシーオブジェクトを取得します。  
  
2.  クライアントコンピューターで、通知領域の **[ネットワーク接続]** アイコンをクリックして、DirectAccess メディアマネージャーにアクセスします。  
  
3.  **[DirectAccess 接続]** をクリックすると、状態が**ローカルに接続**されていることがわかります。  
  
4.  企業ネットワークからコンピューターを削除し、パブリックネットワークに接続します。  
  
5.  コマンドプロンプトで、「 **nltest/dsgetdc: [完全修飾ドメイン名]** 」と入力します。 このコマンドは、クライアントが企業ネットワークにアクセスできることを確認します。 ドメインコントローラにアクセスできない場合は、次のエラーメッセージが表示され、ドメインが存在しないというレポートが表示されます。ERROR_NO_SUCH_DOMAIN.  
  


