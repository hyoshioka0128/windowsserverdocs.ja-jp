---
title: クライアントが接続できず、クラスが登録されていませんというエラーが発生する
description: リモート デスクトップ接続での "クラスが登録されていません" エラーのトラブルシューティング。
ms.reviewer: rklemen
ms.topic: troubleshooting
author: kaushika-msft
manager: dcscontentpm
ms.author: delhan
ms.date: 07/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 52e696bd4229b947ea63a379211192b8664a9f93
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857185"
---
# <a name="clients-cant-connect-and-get-the-class-not-registered-error"></a>クライアントが接続できず、"クラスが登録されていません" というエラーが発生する

Windows 10 バージョン 1709 以降を実行しているクライアントを使用してリモート コンピューターに接続しようとすると、リモート デスクトップ セッション ホスト サーバーで "クラスが登録されていません (0x80040154)" エラー コードを含むメッセージが報告されて、クライアントが接続できないことがあります。

この問題は、接続しようとしているユーザーに必須のユーザー プロファイルがある場合に発生します。 この問題を解決するには、[2018 年 7 月 24 日 — KB4338817 (OS ビルド 16299.579)](https://support.microsoft.com/help/4338817/windows-10-update-kb4338817) Windows 10 更新プログラムをインストールします。
