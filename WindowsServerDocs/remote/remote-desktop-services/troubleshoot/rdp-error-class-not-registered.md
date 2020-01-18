---
title: クライアントが接続できず、クラスが登録されていませんというエラーが発生する
description: リモート デスクトップ接続での "クラスが登録されていません" エラーのトラブルシューティング。
audience: itpro
ms.custom: na
ms.reviewer: rklemen
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: troubleshooting
ms.assetid: ''
author: kaushika-msft
manager: dcscontentpm
ms.author: delhan
ms.date: 07/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7a98e894f3eaf47e257ab39c640e93101fd76fc8
ms.sourcegitcommit: c5709021aa98abd075d7a8f912d4fd2263db8803
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/18/2020
ms.locfileid: "76265904"
---
# <a name="clients-cant-connect-and-get-the-class-not-registered-error"></a>クライアントが接続できず、"クラスが登録されていません" というエラーが発生する

Windows 10 バージョン 1709 以降を実行しているクライアントを使用してリモート コンピューターに接続しようとすると、リモート デスクトップ セッション ホスト サーバーで "クラスが登録されていません (0x80040154)" エラー コードを含むメッセージが報告されて、クライアントが接続できないことがあります。

この問題は、接続しようとしているユーザーに必須のユーザー プロファイルがある場合に発生します。 この問題を解決するには、[2018 年 7 月 24 日 — KB4338817 (OS ビルド 16299.579)](https://support.microsoft.com/help/4338817/windows-10-update-kb4338817) Windows 10 更新プログラムをインストールします。
