---
title: 手順7企業ネットワークに戻るときに接続をテストする
description: このトピックは、「windows Server 2016 用 Windows NLB を使用するクラスターでの DirectAccess のデモンストレーション」のテストラボガイドに含まれています。
manager: brianlic
ms.topic: article
ms.assetid: 5a7252d0-6db8-4a9d-98ee-75082ecd2929
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 3c5a20c52c419714cc24ec1d4d76d57fa42e93c9
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87951087"
---
# <a name="step-7-test-connectivity-when-returning-to-the-corpnet"></a>手順7企業ネットワークに戻るときに接続をテストする

>適用先:Windows Server (半期チャネル)、Windows Server 2016

多くのユーザーがリモートの場所と企業ネットワークの間を移動するため、構成を変更しなくてもリソースにアクセスできることを企業ネットワークに戻すことが重要です。 リモートアクセスを使用すると、DirectAccess クライアントが企業ネットワークに戻ったときに、ネットワークロケーションサーバーに接続できるようになります。 ネットワークロケーションサーバーへの HTTPS 接続が正常に確立されると、DirectAccess クライアントは DirectAccess クライアントの構成を無効にし、企業ネットワークへの直接接続を使用します。

### <a name="test-connectivity-on-client1"></a>CLIENT1 での接続テスト

1. CLIENT1 をシャットダウンしてから、CLIENT1 サブネットまたは仮想スイッチから CLIENT1 を取り外し、企業ネットワークのサブネットまたは仮想スイッチに接続します。 CLIENT1 をオンにして、Corp\user1 としてログオンします。

2. 管理者特権の Windows PowerShell ウィンドウを開き、「 **ipconfig/all**」と入力して、enter キーを押します。 出力には、CLIENT1 にローカル IP アドレスがあり、アクティブな6to4、Teredo、または ip-https トンネルがないことが示されます。

3. APP2 上のネットワーク共有への接続をテストします。 **スタート**画面で「<strong> \\ \APP2\Files</strong>」と入力し、enter キーを押します。 そのフォルダー内のファイルを開くことができます。



