---
title: 手順 7 のテスト接続を企業ネットワークに返す場合
description: このトピックは一部のテスト ラボ ガイド - Windows Server 2016 で Windows NLB を使用するクラスターでの DirectAccess のデモンストレーション
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5a7252d0-6db8-4a9d-98ee-75082ecd2929
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 477d11f0e6bf296c41fb7116a7aae43787df263c
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283376"
---
# <a name="step-7-test-connectivity-when-returning-to-the-corpnet"></a>手順 7 のテスト接続を企業ネットワークに返す場合

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

多くのユーザーは間を移動リモートの場所と、企業ネットワークが戻ったときに、企業ネットワークにあるリソースにアクセスできる任意の構成を行うことがなく変更される重要です。 リモート アクセス、この考えられるため、DirectAccess クライアントが、企業ネットワークに戻るときに、ネットワーク ロケーション サーバーへの接続を設定できません。 ネットワーク ロケーション サーバーに HTTPS 接続が正常に確立されると、DirectAccess クライアントは、DirectAccess クライアントの構成を無効になり、企業ネットワークに直接接続を使用します。  
  
### <a name="test-connectivity-on-client1"></a>CLIENT1 で接続をテストします。  
  
1. CLIENT1 をシャット ダウンし、ホームネット サブネットまたは仮想スイッチから CLIENT1 を取り外す Corpnet サブネットまたは仮想スイッチに接続します。 Client1 で、有効にし、corp \user1 としてログオンします。  
  
2. 管理者特権で Windows PowerShell ウィンドウを開き「 **ipconfig/all**、ENTER キーを押します。 CLIENT1 にローカル IP アドレス、およびアクティブな 6to4、Teredo、または IP-HTTPS がないことが出力されますトンネルです。  
  
3. APP2 のネットワーク共有への接続をテストします。 **開始**画面で「<strong>\\\APP2\Files</strong>し、ENTER キーを押します。 そのフォルダーでファイルを開くことができます。  
  


