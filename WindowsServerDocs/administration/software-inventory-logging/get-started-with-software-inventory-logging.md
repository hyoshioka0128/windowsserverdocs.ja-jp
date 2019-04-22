---
title: 概要ソフトウェア インベントリ ログ
description: インストールおよびソフトウェア インベントリ ログの使用を開始する方法について説明します
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 5a3e51effa6321c3575e385f1c56bba57318eca5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822833"
---
# <a name="get-started-with-software-inventory-logging"></a>概要ソフトウェア インベントリ ログ

>適用先:Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

 ソフトウェア インベントリ ログは、サーバーごとに Microsoft ソフトウェアのインベントリ データを収集します。 Windows Server 2012 R2 の ソフトウェア インベントリ ログを使用して、前に必ずその更新プログラムを Windows [KB 3000850](https://support.microsoft.com/kb/3000850)と[KB 3060681](https://support.microsoft.com/kb/3060681)インベントリされる各システムにインストールされます。 Windows Update は Windows Server 2016 では必要ありません。 また、SIL の機能を使用して、集計サーバーへのデータを転送する場合は、必ず、ネットワークの有効な SSL 証明書があります。

## <a name="BKMK_OVER"></a>機能の説明
Windows Server のソフトウェア インベントリ ログは、サーバー管理者が簡単な PowerShell コマンドレットのセットを使用して、サーバーにインストールされた Microsoft ソフトウェアの一覧を取得できる機能です。 また、HTTPS プロトコルを使用して、このデータをネットワーク経由で定期的に収集し、集計のためにターゲット Web サーバーへと転送することもできます。 この機能の管理には、PowerShell コマンドも使用できます (主に毎時の収集と転送のため)。

> [!NOTE]
> Web サービスを実行する集計サーバーは個別に構成できます。 [ソフトウェア インベントリ ログ アグリゲーター](software-inventory-logging-aggregator.md)の詳細をご確認ください。

> [!IMPORTANT]
> ソフトウェア インベントリ ログによって収集されたデータがその機能の一部として Microsoft に送信されることはありません。

## <a name="BKMK_APP"></a>実際の適用
ソフトウェア インベントリ ログは、Microsoft ソフトウェアに関する正確な情報を、より安価な運用コストで取得できるよう設計されています。データの取得は、単一サーバー上のローカル展開だけでなく 、IT 環境内の多数のサーバーからも実行できます (機能が IT 環境に展開され、有効化されている場合)。 このデータを集計サーバーに転送する機能によって (IT 管理者によって個別にセット アップされている場合)、自動的で一様なプロセスでデータを 1 つの場所に収集できます。 これはインターフェイスを直接照会することにより実現できますが、ソフトウェア インベントリ ログでは、各サーバーによって起動される (ネットワーク経由での) 転送アーキテクチャを採用することによって、多数のソフトウェア インベントリおよび資産管理のシナリオで一般的なコンピューター検出の課題を解決できます。 HTTPS 経由で管理者の集計サーバーに転送されるデータを保護するために SSL が使用されます。 (1 つのサーバー上の) 1 つの場所にデータを保持することで、データの分析、操作、およびレポートがより簡単になります。 この機能の一部として、データが Microsoft に送信されることはありません。 ソフトウェア インベントリ ログのデータおよび機能は、サーバー ソフトウェアのライセンスされた所有者および管理者のみの使用が意図されています。

ソフトウェア インベントリ ログは、サーバー管理者が次のタスクを実行するのに役立ちます。

-   Windows Server からソフトウェアおよびサーバーのインベントリ情報をリモートおよびオンデマンドで取得する。

-   各サーバーのソフトウェア インベントリ ログ機能を有効にし、ターゲット Web サーバーの URI と、認証用の証明書拇印を選択して、さまざまなソフトウェア資産管理シナリオに対応しながら、ソフトウェアやサーバーのインベントリ情報を集計する。

## <a name="see-also"></a>関連項目
[ソフトウェア インベントリ ログ アグリゲーター](https://technet.microsoft.com/library/mt572043.aspx)<br>
[管理ソフトウェア インベントリ ログ](manage-software-inventory-logging.md)<br>
[Windows PowerShell でのソフトウェア インベントリ ログ コマンドレット](https://technet.microsoft.com/library/dn283390.aspx)<br>
[Microsoft Assessment and Planning Toolkit](https://www.microsoft.com/download/en/details.aspx?id=7826)
[ボリューム ライセンス認証管理ツール](http://blogs.technet.com/b/volume-licensing/)

