---
title: リモート デスクトップ サービスのセキュリティで保護されたデータ ストレージ
description: Rds. でユーザー プロファイル ディスク (Upd) を使用してデータを安全に格納するための情報のプランニング
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 37b7f68e-7c3a-4190-a52f-99ae96885fae
author: lizap
ms.author: elizapo
ms.date: 11/21/2016
manager: dongill
ms.openlocfilehash: 242d09e49141e9fb789a83421714366105730cc2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870593"
---
# <a name="remote-desktop-services---secure-data-storage-with-upds"></a>リモート デスクトップ サービスの Upd をセキュリティで保護されたデータ ストレージ

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

ストアのビジネス リソース、ユーザーのパーソナル化データおよび設定に安全にオンプレミスまたは Azure です。 RD セッション ホストは、AD 認証を使用して、カスタマイズした環境で安全に必要なリソースを持つユーザーを支援します。 

元の リモート リソースにアクセス、RDS デプロイを管理する重要な側面ですが、エンドポイントに関係なく、一貫したエクスペリエンスがあるユーザーのことを確認します。 ユーザー プロファイル ディスク (Upd) は、ユーザー データ、カスタマイズ、およびアプリケーション設定は 1 つのコレクション内のユーザーを許可します。 ユーザーとサインイン - UPD はそのセッションの間のローカル ドライブとして扱われます。 ユーザーのセッションにマウントされているサーバーの全体の共有に保存されているコレクションごとの VHD ファイルを UPD には。 

ユーザーの観点からは、UPD famililar エクスペリエンスを提供します - 自分のドキュメントに、ドキュメント フォルダー (で何がローカルのドライブ) での変更、設定を保存アプリ通常どおりにしたり、Windows 環境のカスタマイズ内容をできるようにします。 このレジストリ ハイブを含むすべてのデータは、UPD に格納されているし、セントラル ネットワーク共有に保持します。 Upd をユーザーが利用できるは、ユーザーがデスクトップまたは RemoteApp にアクティブに接続されている場合だけです。 C:\Users 全体のユーザーのため、Upd は、コレクション内でローミングのみできる&#92;\<username\> UPD にディレクトリ (appdata \local を含む) が格納されています。

使用することができます[PowerShell コマンドレット](https://technet.microsoft.com/library/jj215443.aspx)中央の共有や、各 UPD のサイズ、どのフォルダーを含まれているまたは UPD に保存されたユーザー プロファイルから除外する必要がありますへのパスを指定します。 移動して Upd サーバー マネージャーを使用できるように別の方法として、 **Remote Desktop Services > コレクション > デスクトップのコレクション > デスクトップ コレクションのプロパティ > ユーザー プロファイル ディスク**します。 有効にするか、そのコレクション内の特定のユーザーではなく、コレクション全体のすべてのユーザーの Upd を無効にすることに注意してください。 Upd は、コレクション内のサーバーのフル コントロール アクセス許可のある中央のファイル共有に格納する必要があります。 

Azure でそれらを格納することにより、Upd の高可用性を実現し[記憶域スペース ダイレクト](rds-storage-spaces-direct-deployment.md)します。 