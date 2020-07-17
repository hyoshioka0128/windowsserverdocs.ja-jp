---
title: BranchCache ホスト型キャッシュ モードの展開
description: このガイドでは、Windows Server 2016 と Windows 10 を実行するコンピューターに、ホスト型キャッシュモードで BranchCache を展開する手順について説明します。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: article
ms.assetid: c635fa48-d064-4b8b-9dce-9f26abfbcfa4
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 10aba87b82804234a91dbc011be75b45724a1e9d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861745"
---
# <a name="branchcache-hosted-cache-mode-deployment"></a>BranchCache ホスト型キャッシュ モードの展開

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、BranchCache ホスト型キャッシュモードの展開プロセスに関する詳細な手順に関するトピックへのリンクを示します。

BranchCache ホスト型キャッシュモードを展開するには、次の手順に従います。

- [BranchCache 機能をインストールし、サービス接続ポイントによってホスト型キャッシュサーバーを構成する](5-Bc-Feature-Scp.md)

- [ホスト型キャッシュ&#40;の移動とサイズ変更 (オプション)&#41;](6-Bc-Move-Resize-Cache.md)

- [ホスト型キャッシュサーバー &#40;上でのコンテンツの事前ハッシュと事前読み込み (オプション)&#41;](7-Bc-Prehash-Preload.md)

- [クライアントの自動ホスト型キャッシュ検出をサービス接続ポイントで構成する](10-Bc-Client-By-Scp.md)

>[!NOTE]
>このガイドの手順は含まれていません場合に、 **ユーザー アカウント制御** 続行の許可を要求するダイアログ ボックスが開きます。 このガイドを実行しているときにこのダイアログ ボックスが開いた場合、または操作の結果としてこのダイアログ ボックスが開いた場合、 **[続行]** をクリックします。

このガイドを使用するには、「 [BranchCache 機能をインストールし、サービス接続ポイントによってホスト型キャッシュサーバーを構成](5-Bc-Feature-Scp.md)する」を参照してください。