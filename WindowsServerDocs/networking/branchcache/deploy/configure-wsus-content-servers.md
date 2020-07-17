---
title: Windows Server Update Services (WSUS) コンテンツ サーバーを構成する
description: このトピックは、Windows Server 2016 用の BranchCache 展開ガイドに含まれています。これは、ブランチオフィスでの WAN 帯域幅の使用を最適化するために、分散キャッシュモードとホスト型キャッシュモードで BranchCache を展開する方法を示しています。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 9724aa8d-e4ae-404c-bee6-cef1534cd3ca
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 2993c78e85609ac720fd208971dda7ed67a3610d
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80319161"
---
# <a name="configure-windows-server-update-services-wsus-content-servers"></a>Windows Server Update Services (WSUS) コンテンツ サーバーを構成する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

BranchCache 機能をインストールし、BranchCache サービスを開始した後、WSUS サーバーは、ローカルコンピューターに更新プログラムファイルを保存するように構成する必要があります。 

更新ファイルをローカルコンピューターに保存するように WSUS サーバーを構成すると、更新プログラムのメタデータと更新ファイルの両方がによってダウンロードされ、WSUS サーバーに直接保存されます。 これにより、BranchCache クライアントコンピューターは、Microsoft Update Web サイトから直接ではなく、WSUS サーバーから Microsoft 製品の更新ファイルを受け取ることができます。  
  
WSUS 同期の詳細については、「[更新プログラムの同期](https://technet.microsoft.com/library/mt612311.aspx)のセットアップ」を参照してください。  