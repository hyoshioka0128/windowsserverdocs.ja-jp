---
title: Windows Server Update Services (WSUS) コンテンツ サーバーを構成する
description: このトピックでは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅の使用を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部です。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 9724aa8d-e4ae-404c-bee6-cef1534cd3ca
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e8576282be92f02daf716da82ea75eddc755ee5c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873843"
---
# <a name="configure-windows-server-update-services-wsus-content-servers"></a>Windows Server Update Services (WSUS) コンテンツ サーバーを構成する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

を BranchCache 機能をインストールして、BranchCache サービスを開始した後は、ローカル コンピューターの更新ファイルを格納する WSUS サーバーを構成する必要があります。 

ローカル コンピューターの更新ファイルを格納する WSUS サーバーを構成するときに、更新プログラムのメタデータと更新プログラム ファイルの両方がによってダウンロードされ、WSUS サーバーに直接格納されています。 これにより、Microsoft Update Web サイトから直接ではなく、WSUS サーバーから、BranchCache クライアント コンピューターが Microsoft 製品の更新ファイルを受信します。  
  
WSUS 同期の詳細については、次を参照してください[更新プログラムの同期の設定。](https://technet.microsoft.com/library/mt612311.aspx)  