---
title: Windows Server Update Services (WSUS) コンテンツ サーバーを構成します。
description: このトピックでは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅の使用を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部です。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 9724aa8d-e4ae-404c-bee6-cef1534cd3ca
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8200a0905f7bc5c403288a22faece5f84eac8af9
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="configure-windows-server-update-services-wsus-content-servers"></a>Windows Server Update Services (WSUS) コンテンツ サーバーを構成します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

BranchCache 機能をインストールすると、BranchCache サービスを開始する、ローカル コンピューター上の更新ファイルを保存する WSUS サーバーを構成する必要があります。 

ローカル コンピューター上の更新ファイルを保存する WSUS サーバーを構成するときに、更新プログラムのメタデータと、更新プログラム ファイルの両方がでダウンロードし、WSUS サーバー上で直接格納されています。 これにより、Microsoft Update Web サイトから直接ではなく WSUS サーバーから、BranchCache クライアント コンピューターが Microsoft 製品の更新ファイルを受け取ること。  
  
WSUS の同期の詳細については、次を参照してください[更新プログラムの同期を設定する。](https://technet.microsoft.com/en-us/library/mt612311.aspx)  