---
title: MultiPoint Services でのはじめに
description: MultiPoint サービスを紹介し、使用を開始します。
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aca5f0be-f253-46b5-b1e7-0bffa15f3227
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 2ed2084038236dc8914eefe6bdafc133817b7b41
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70871679"
---
# <a name="getting-started-with-multipoint-services"></a>MultiPoint Services でのはじめに
MultiPoint Services システムでは、多くのユーザーが、ステーションハブを使用して物理的に接続されている複数のステーションを1台のコンピューターにしか使用できません。 各ステーションは、通常、ステーションハブ、マウス、キーボード、およびビデオモニターで構成されています。 MultiPoint Services ステーションの各ユーザーには、MultiPoint Manager を使用して管理できる一意の Windows コンピューティングセッションがあります。  
  
MultiPoint Services システムのコンポーネントには、次のものが含まれます。  
  
-   MultiPoint Services システムソフトウェア。コンピューター上の複数のモニター、キーボード、マウスデバイス、およびその他のデバイスをサポートします。  
  
-   Multipoint マネージャーアプリケーション。 MultiPoint Services ステーションで監視およびアクションを実行できます。  
  
-   メンテナンスおよび管理ツール。  
  
-   MultiPoint ダッシュボードアプリケーション。他のユーザーとの通信など、日常のタスクを完了できます。  
  
Multipoint マネージャーと MultiPoint ダッシュボードを使用して MultiPoint Services ステーションを管理する方法については、このヘルプファイルを参照してください。  
  
## <a name="overview-of-multipoint-manager"></a>MultiPoint マネージャーの概要  
Multipoint マネージャーには、MultiPoint Services ステーションを管理するときに使用できる4つのタブが用意されています。 各タブとそれらに対して実行できるタスクについては、各ヘルプトピックで詳しく説明されています。  
  
タブは次のとおりです。  
  
-   **[ホーム] タブ:** 管理タスクを実行したり、MultiPoint サーバーを追加または削除したり、コンピューターを再起動またはシャットダウンしたり、ディスクの保護を有効にしたり、クライアントアクセスライセンスを追加したり、ステーションを再マップしたり、ヘルプやサポートを取得したりするためのモードを切り替えます。 詳細については、「 [MultiPoint マネージャーを使用してシステムタスクを管理](Manage-System-Tasks-Using-MultiPoint-Manager.md)する」を参照してください。  
  
-   **[ステーション] タブ:** ユーザーの*デスクトップ*の状態を表示し、ユーザーセッションを*終了*または*中断*します。 詳細については、「[ユーザーステーションの管理](Manage-User-Stations.md)」を参照してください。  
  
-   **[ユーザー] タブ:** *標準ユーザーアカウント*と*管理ユーザーアカウント*を作成および管理します。 詳細については、「[ユーザー アカウントの管理](Manage-User-Accounts.md)」トピックを参照してください。  
  
-   **[仮想デスクトップ] タブ:** 仮想デスクトップロールを有効にします。 詳細については、[仮想デスクトップの管理](Manage-Virtual-Desktops.md)に関するトピックを参照してください。  
  
## <a name="multipoint-server-management-and-maintenance"></a>MultiPoint Server の管理とメンテナンス  
Multipoint Services システムがセットアップされたら、multipoint マネージャーを使用して MultiPoint Services を管理できます。  
  
MultiPoint マネージャーを使用して実行できるアクションの種類には、次のものがあります。  
  
-   **ユーザーアカウントの追加:** MultiPoint マネージャーを使用して、標準および管理ユーザーアカウントを作成します。  
  
-   **サーバー設定の編集:** MultiPoint Services システムをコンソールモードで起動するように構成したり、1つのアカウントに複数のセッションを許可したり、各ステーションに一意の IP アドレスを割り当てたり、その他のタスクを実行したりすることができます。  
  
-   **コンソールモードへの切り替え:** Multipoint services システムに新しいソフトウェアをインストールするために、MultiPoint Services システムをコンソールモードに変更することができます。 ソフトウェアのインストールとライセンスのオプションに応じて、すべてのユーザーがソフトウェアを実行できるように指定することも、ソフトウェアのみを使用することもできます。  
  
-   **行う**MultiPoint Services で問題が発生した場合は、[トラブルシューティング](Troubleshooting.md)のセクションを参照して、問題の解決に役立つトピックを見つけてください。  
  
## <a name="overview-of-multipoint-dashboard"></a>MultiPoint ダッシュボードの概要  
MultiPoint ダッシュボードには、一般的な毎日のタスクにアクセスする2つのタブのいずれかを選択できるリボンエクスペリエンスがあります。  
  
タブは次のとおりです。  
  
-   **[ホーム] タブ:** ステーションをブロックまたはブロック解除する、web の制限オプションを設定する、他のデスクトップにデスクトップを表示する、アプリケーションを起動または終了する、インスタントメッセージングで通信する、他のユーザーにリモートデスクトップコントロールを使用する、デスクトップのサムネイルビューを調整する、有効または無効にするインスタントメッセージングとアプリケーションの自動起動。 詳細については、「 [MultiPoint ダッシュボードを使用したユーザーデスクトップの管理](Manage-User-Desktops-Using-MultiPoint-Dashboard.md)」を参照してください。  
  
-   **[システム] タブ:** すべてのシステムまたは選択したシステムを再起動、シャットダウン、または再マップします。 詳細については、 [Multipoint ダッシュボードを使用した Multipoint システムの管理](Manage-MultiPoint-Systems-Using-MultiPoint-Dashboard.md)に関するトピックを参照してください。  
  
## <a name="daily-use-of-your-multipoint-server-system"></a>MultiPoint Server システムの毎日の使用  
Multipoint services の使用を毎日開始するときに、multipoint services システムのユーザーと共有する MultiPoint Services の使用方法に関する情報があります。 この情報には、次のものが含まれます。  
  
**コンテンツを共有し、コンテンツをプライベートに保つ:**  
  
-   ユーザーは、そのユーザーのみが表示できるプライベートフォルダーにファイルまたはドキュメントを保存できます。  
  
-   ユーザーは、MultiPoint Services システム上のすべてのユーザーがアクセスできるパブリックフォルダーにドキュメントを保存することもできます。  
  
-   MultiPoint Services では、ユーザーの個人用フォルダーにプライベートに保存されている場合でも、管理ユーザーがシステム上のすべてのファイルとドキュメントにアクセスできることを認識していることが重要です。  
  
プライベートコンテンツとパブリックコンテンツを保存および管理する方法の詳細については、「[ユーザーファイルの管理](Manage-User-Files.md)」を参照してください。  
  
**ユーザーの MultiPoint Services セッションに関する情報:**  
  
-   各ユーザーには、ユーザー名とパスワード、および MultiPoint Services システム上の一意のデスクトップ*セッション*があります。  
  
-   *標準ユーザー*は、MultiPoint Services システムの*管理ユーザー*ではありません。 標準ユーザーは、一部の種類のソフトウェアをインストールすることはできませんが、画面の解像度を除き、ファイルを保存したり、デスクトップの設定を変更したりできます。 ユーザーが実行したデスクトップの変更は、再度ログオンしたときに反映されます。  
  
-   ユーザーは、1つのステーションから切断し、別のステーションのセッションに再びログオンして、作業を失うことができます。 詳細については、「[ユーザー セッションを中断してアクティブな状態で保持する](Suspend-and-Leave-User-Session-Active.md)」トピックを参照してください。  
  
-   標準ユーザーのセッション (またはすべてのユーザーセッション) は、管理ユーザーが MultiPoint マネージャーを使用して切断またはログオフできます。 詳細については、「[ユーザーデスクトップの管理](manage-user-desktops-using-multipoint-dashboard.md)」を参照してください。  
  
-   ユーザーがパスワードを忘れた場合は、標準の Windows ユーザーアカウント管理機能を使用する **[ユーザー]** タブからパスワードをリセットできます。 詳細については、「[ユーザーアカウントを更新または削除する](Update-or-Delete-a-User-Account.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
[MultiPoint Server システムの管理](managing-your-multipoint-services-system.md)  
[ソフトウェアライセンスのコンプライアンスに関する重要な情報](Important-Information-about-Software-License-Compliance.md)  
[MultiPoint マネージャーを使用したシステム タスクの管理](Manage-System-Tasks-Using-MultiPoint-Manager.md)  
[ユーザー ファイルの管理](Manage-User-Files.md)  
[ユーザーデスクトップの管理](manage-user-desktops-using-multipoint-dashboard.md)  
[ユーザーセッションを中断してアクティブのままにする](Suspend-and-Leave-User-Session-Active.md)  
[ユーザーの接続状態を表示する](View-User-Connection-Status.md)  
[ステーション ハードウェアの管理](Manage-Station-Hardware.md)  
[ステーションをセットアップする](Set-Up-a-Station.md)  
[ユーザー アカウントの管理](Manage-User-Accounts.md)  
[ユーザーアカウントを更新または削除する](Update-or-Delete-a-User-Account.md)  
[MultiPoint ダッシュボードを使用したユーザー デスクトップの管理](Manage-User-Desktops-Using-MultiPoint-Dashboard.md)  
[MultiPoint ダッシュボードを使用した MultiPoint システムの管理](Manage-MultiPoint-Systems-Using-MultiPoint-Dashboard.md)  
[トラブルシューティング](Troubleshooting.md)    
  
