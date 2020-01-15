---
title: ソフトウェアインベントリログを使ってみる
description: ソフトウェアインベントリログのインストールと使用を開始する方法について説明します。
ms.custom: na
ms.prod: windows-server
ms.technology: manage-software-inventory-logging
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed51c13c-7cbf-4144-a675-011fd29379d4
author: brentfor
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: add11bf51570e3cafa2bd03ee3585de89f3eecab
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2020
ms.locfileid: "75946967"
---
# <a name="get-started-with-software-inventory-logging"></a>ソフトウェアインベントリログを使ってみる

>適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

 ソフトウェアインベントリログは、サーバーごとに Microsoft ソフトウェアインベントリデータを収集します。 Windows Server 2012 R2 でソフトウェアインベントリログを使用する前に、インベントリされる各システムに Windows Update [kb 3000850](https://support.microsoft.com/kb/3000850)と[kb 3060681](https://support.microsoft.com/kb/3060681)がインストールされていることを確認してください。 Windows Server 2016 には Windows Update は必要ありません。 また、SIL の機能を使用して集計サーバーにデータを転送する場合は、ネットワークに対して SSL 証明書が有効になっていることを確認してください。

## <a name="BKMK_OVER"></a>機能の説明
Windows Server のソフトウェア インベントリ ログは、簡単な PowerShell コマンドレットのセットを使用して、サーバー管理者がサーバーにインストールされた Microsoft ソフトウェアの一覧を取得できる機能です。 また、HTTPS プロトコルを使用して、このデータをネットワーク経由で定期的に収集し、集計のためにターゲット Web サーバーへと転送することもできます。 この機能の管理には、PowerShell コマンドも使用できます (主に毎時の収集と転送のため)。

> [!NOTE]
> Web サービスを実行する集計サーバーは個別に構成できます。 [ソフトウェア インベントリ ログ アグリゲーター](software-inventory-logging-aggregator.md)の詳細をご確認ください。

> [!IMPORTANT]
> ソフトウェアインベントリログによって収集されたデータは、機能の一部としてマイクロソフトに送信されることはありません。

## <a name="BKMK_APP"></a>実用的なアプリケーション
ソフトウェア インベントリ ログは、Microsoft ソフトウェアに関する正確な情報を、より安価な運用コストで取得できるよう設計されています。データの取得は、単一サーバー上のローカル展開だけでなく 、IT 環境内の多数のサーバーからも実行できます (機能が IT 環境に展開され、有効化されている場合)。 このデータを集計サーバーに転送する機能によって (IT 管理者によって個別にセット アップされている場合)、自動的で一様なプロセスでデータを 1 つの場所に収集できます。 これはインターフェイスを直接照会することにより実現できますが、ソフトウェア インベントリ ログでは、各サーバーによって起動される (ネットワーク経由での) 転送アーキテクチャを採用することによって、多数のソフトウェア インベントリおよび資産管理のシナリオで一般的なコンピューター検出の課題を解決できます。 HTTPS 経由で管理者の集計サーバーに転送されるデータをセキュリティで保護するには、SSL を使用します。 (1 つのサーバー上の) 1 つの場所にデータを保持することで、データの分析、操作、およびレポートがより簡単になります。 この機能の一部として、データが Microsoft に送信されることはありません。 ソフトウェアインベントリログのデータと機能は、サーバーソフトウェアのライセンス所有者と管理者のみが使用することを目的としています。

ソフトウェア インベントリ ログは、サーバー管理者が次のタスクを実行するのに役立ちます。

-   Windows Server からソフトウェアおよびサーバーのインベントリ情報をリモートおよびオンデマンドで取得する。

-   各サーバーのソフトウェアインベントリログ機能を有効にし、web サーバーのターゲット URI と認証用の証明書の拇印を選択することで、さまざまなソフトウェア資産管理シナリオのソフトウェアおよびサーバーのインベントリ情報を集計します。

## <a name="see-also"></a>関連項目
[ソフトウェア インベントリ ログ アグリゲーター](https://technet.microsoft.com/library/mt572043.aspx)<br>
[ソフトウェア インベントリ ログの管理](manage-software-inventory-logging.md)<br>
[Windows PowerShell のソフトウェアインベントリログコマンドレット](https://technet.microsoft.com/library/dn283390.aspx)<br>
[Microsoft アセスメント & プランニングツールキット](https://www.microsoft.com/download/en/details.aspx?id=7826)
[ボリュームライセンス認証管理ツール](https://blogs.technet.com/b/volume-licensing/)

