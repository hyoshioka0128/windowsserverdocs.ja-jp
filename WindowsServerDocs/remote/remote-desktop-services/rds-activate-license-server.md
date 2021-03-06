---
title: リモート デスクトップ サービス ライセンス サーバーをアクティブ化します。
description: インストールして、RD ライセンス サーバーをアクティブ化
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eb24ddd2-0361-41fe-bd6b-c7c63427cb71
author: lizap
ms.author: elizapo
ms.date: 09/20/2016
manager: dongill
ms.openlocfilehash: d28ceac9cde0ee2d4c92867bdd90d5c463a8cd4c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888013"
---
# <a name="activate-the-remote-desktop-services-license-server"></a>リモート デスクトップ サービス ライセンス サーバーをアクティブ化します。

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

リモート デスクトップ サービスのライセンス、RD セッション ホストにアクセスするときにユーザーとデバイスにサーバーの問題のクライアント アクセス ライセンス (Cal)。 リモート デスクトップ ライセンス マネージャーを使用して、ライセンス サーバーをアクティブ化することができます。 

## <a name="install-the-rd-licensing-role"></a>RD ライセンスの役割をインストールします。

1. 管理者アカウントを使用して、ライセンス サーバーとして使用するサーバーにサインインします。
2. サーバー マネージャーで、**役割の概要**、 をクリックし、**役割の追加**します。
   をクリックして**次**役割のウィザードの最初のページでします。
3. 選択**リモート デスクトップ サービス**、順にクリックします**次へ**、し**次**リモート デスクトップ サービス ページ。
4. 選択**リモート デスクトップ ライセンス**、 をクリックし、**次**。
5. ドメインの構成 - 選択**このライセンス サーバーの検出スコープを構成**、 をクリックして**このドメイン**、順にクリックします**次**します。
6. **[インストール]** をクリックします。

## <a name="activate-the-license-server"></a>ライセンス サーバーのアクティブ化

1. リモート デスクトップ ライセンス マネージャを開く: クリックして**開始 > 管理ツール > リモート デスクトップ サービス > リモート デスクトップ ライセンス マネージャー**します。
2. ライセンス サーバーを右クリックし、**サーバーのアクティブ化**します。
3. クリックして**次**[ようこそ] ページ。
4. 接続方法選択**自動接続 (推奨)**、順にクリックします**次**します。
5. 会社の情報 (氏名、会社名、お住まい地域) を入力し、クリックして**次**します。
6. 必要に応じてその他の会社情報 (たとえば、電子メールや会社アドレス) を入力し、クリックして**次**します。 
7. 確認します**ライセンスのインストール ウィザードを開始**が選択されていない (後の手順で、ライセンスをインストールしましたが) をクリックし、**次**。

ライセンス サーバーは、発行ライセンスの管理を開始する準備ができました。 