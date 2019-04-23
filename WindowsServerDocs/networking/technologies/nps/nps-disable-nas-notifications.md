---
title: NPS の NAS 通知の転送を無効にします。
description: このトピックでは、Windows Server 2016 でのネットワーク ポリシー サーバーの同時実行の認証の構成について説明します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: a09bfb03-95fc-4534-bf3c-97078ef6b07e
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bc4c6afdcb02eb2bbab1f0373a5b3a28236269bf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882263"
---
# <a name="disable-nas-notification-forwarding-in-nps"></a>NPS の NAS 通知の転送を無効にします。

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

開始の転送を無効にして、NPS で構成されているリモート RADIUS サーバー グループのメンバーへのネットワーク アクセス サーバー (Nas) からメッセージを停止するのには、この手順を使用することができます。

リモート RADIUS サーバー グループを構成した場合、NPS で**接続要求ポリシー**、オフにする、**このリモート RADIUS サーバー グループにアカウンティング要求を転送**チェック ボックスで、これらのグループはまだ送信 NAS は起動し、通知メッセージを停止します。 

これには、不要なネットワーク トラフィックが作成されます。 このトラフィックをなくすため、NAS 通知の各リモート RADIUS サーバー グループ内の個々 のサーバーの転送を無効にします。

この手順を実行する、 **管理者** グループです。

### <a name="to-disable-nas-notification-forwarding"></a>NAS 通知の転送を無効にするには

1. サーバー マネージャーで、クリックして **ツール**, 、クリックして **ネットワーク ポリシー サーバー**します。 NPS コンソールが開きます。

2. NPS コンソールで、ダブルクリック**RADIUS クライアントとサーバー**、 をクリックして**リモート RADIUS サーバー グループ**、し構成するリモートの RADIUS サーバー グループをダブルクリックします。 リモート RADIUS サーバー グループ**プロパティ** ダイアログ ボックスが表示されます。

3. 構成、およびクリックするグループのメンバーをダブルクリックして、**認証/アカウンティング**タブ。

4. **アカウンティング**チェック ボックスをオフ、**転送のネットワーク アクセス サーバーの開始と停止の通知をこのサーバー**チェック ボックスをオンにして**OK**。

5. 構成するすべてのグループ メンバーの場合は、手順 3. および 4. を繰り返します。

NPS の管理に関する詳細については、次を参照してください。[ネットワーク ポリシー サーバーの管理](nps-manage-top.md)します。

NPS の詳細については、次を参照してください。[ネットワーク ポリシー サーバー (NPS)](nps-top.md)します。
