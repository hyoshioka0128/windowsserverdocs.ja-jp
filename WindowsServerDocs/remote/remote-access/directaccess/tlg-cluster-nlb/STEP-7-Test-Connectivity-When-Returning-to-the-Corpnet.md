---
title: 手順7企業ネットワークに戻るときに接続をテストする
description: このトピックは、「windows Server 2016 用 Windows NLB を使用するクラスターでの DirectAccess のデモンストレーション」のテストラボガイドに含まれています。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 5a7252d0-6db8-4a9d-98ee-75082ecd2929
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 479ac48bbb04186f97d25e6744e8630b4dc6a51e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80819125"
---
# <a name="step-7-test-connectivity-when-returning-to-the-corpnet"></a>手順7企業ネットワークに戻るときに接続をテストする

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

多くのユーザーがリモートの場所と企業ネットワークの間を移動するため、構成を変更しなくてもリソースにアクセスできることを企業ネットワークに戻すことが重要です。 リモートアクセスを使用すると、DirectAccess クライアントが企業ネットワークに戻ったときに、ネットワークロケーションサーバーに接続できるようになります。 ネットワークロケーションサーバーへの HTTPS 接続が正常に確立されると、DirectAccess クライアントは DirectAccess クライアントの構成を無効にし、企業ネットワークへの直接接続を使用します。  
  
### <a name="test-connectivity-on-client1"></a>CLIENT1 での接続テスト  
  
1. CLIENT1 をシャットダウンしてから、CLIENT1 サブネットまたは仮想スイッチから CLIENT1 を取り外し、企業ネットワークのサブネットまたは仮想スイッチに接続します。 CLIENT1 をオンにして、Corp\user1 としてログオンします。  
  
2. 管理者特権の Windows PowerShell ウィンドウを開き、「 **ipconfig/all**」と入力して、enter キーを押します。 出力には、CLIENT1 にローカル IP アドレスがあり、アクティブな6to4、Teredo、または ip-https トンネルがないことが示されます。  
  
3. APP2 上のネットワーク共有への接続をテストします。 **スタート**画面で、「<strong>\\\APP2\Files</strong>」と入力し、enter キーを押します。 そのフォルダー内のファイルを開くことができます。  
  


