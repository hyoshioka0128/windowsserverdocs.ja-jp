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
manager: ''
ms.author: delhan
ms.date: 07/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: cdc6d1c292f554e6d7fedd3fea0b1e9d6673df0c
ms.sourcegitcommit: f6503e503d8f08ba8000db9c5eda890551d4db37
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/26/2019
ms.locfileid: "68529892"
---
# <a name="clients-cant-connect-and-get-the-class-not-registered-error"></a>クライアントが接続できず、"クラスが登録されていません" というエラーが発生する

Windows 10 バージョン 1709 以降を実行しているクライアントを使用してリモート コンピューターに接続しようとすると、リモート デスクトップ セッション ホスト サーバーで "クラスが登録されていません (0x80040154)" エラー コードを含むメッセージが報告されて、クライアントが接続できないことがあります。

この問題は、接続しようとしているユーザーに必須のユーザー プロファイルがある場合に発生します。 この問題を解決するには、[2018 年 7 月 24 日 — KB4338817 (OS ビルド 16299.579)](https://support.microsoft.com/help/4338817/windows-10-update-kb4338817) Windows 10 更新プログラムをインストールします。
