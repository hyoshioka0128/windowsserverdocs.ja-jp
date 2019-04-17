---
title: "移行モード 1 の場合の Windows Server Essentials をインストールします。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fd7196ac-cfa6-46a5-ba77-6962b47a825e
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 808a4b1e120fa559d603b34ad006b18de6b94378
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="install-windows-server-essentials-in-migration-mode1"></a>移行モード 1 の場合の Windows Server Essentials をインストールします。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

Windows Server Essentials を実行しているネットワークに 1 つだけのサーバーがあることができ、そのサーバーは、ネットワークのドメイン コントローラーである必要があります。  
  
 Windows Server Essentials を移行モードでインストールするときに、インストール ウィザードは、次のタスクを実行します。  
  
1.  インストールし、移行先サーバーで Windows Server Essentials サーバー ソフトウェアを構成します。  
  
2.  ドメイン スキーマを最新バージョンに更新します。  
  
3.  移行先サーバーを既存のドメインに参加します。 移行元サーバーと移行先サーバーできます両方メンバーである、同じドメインの移行プロセスを完了するまで。 移行が完了したら、21 日以内、ネットワークから移行元サーバーを削除する必要があります。  
  
    > [!WARNING]
    >  エラー メッセージは、1 日に、ネットワークから移行元サーバーを削除するまで、21 日の猶予期間中に、イベント ログに追加されます。 テキスト メッセージの読み取りの"FSMO 役割チェック検出条件環境内が、ライセンス ポリシーに対応していません。 管理サーバーには、プライマリ ドメイン コントローラーとドメイン名前付けマスターの Active Directory の役割を保持する必要があります。 移動してください、Active Directory ロール管理サーバーにできるようになりました。 このサーバーは自動的にシャット ダウンこの状態が最初に検出された時点から 21 日以内に問題が修正されない場合です。" 21 日の猶予期間後は、移行元サーバーをシャット ダウンします。  
  
4.  操作マスター (フレキシブル シングル マスター操作または FSMO とも呼ばれます) の役割を移行元サーバーから移行先サーバーに転送します。 操作マスターの役割は、標準的なデータ転送、および更新方法では不十分である場合に使用される特殊なドメイン コントローラーのタスクです。 移行先サーバーでは、ドメイン コントローラーになると、保持しなければならない、操作マスターの役割。  
  
5.  グローバル カタログ サーバーと移行先サーバーを構成します。 グローバル カタログ サーバーは、分散データ リポジトリを管理するドメイン コントローラーです。 Active Directory フォレスト内のすべてのドメイン内の各オブジェクトの検索可能な部分的な表現が含まれています。  
  
6.  サイト ライセンス サーバーと移行先サーバーを構成します。  
  
##  <a name="BKMK_Install"></a>移行先サーバーでの Windows Server Essentials をインストールします。  
 をインストールして Windows Server Essentials を移行モードで移行先サーバーで構成するには、次の手順を実行します。  
  
#### <a name="to-install-windows-server-essentials-on-the-destination-server"></a>移行先サーバーで Windows Server Essentials をインストールするには  
  
1.  移行先サーバーで有効にして、Windows Server Essentials の DVD1 を DVD ドライブに挿入します。 CD または DVD から起動するかを確認するメッセージが表示された場合は、任意のキーを押します。  
  
    > [!NOTE]
    >  使用することができます、移行先サーバーでは、USB フラッシュ ドライブからの起動をサポートする場合、**Windows 7 USB/DVD Download Tool**を Windows Server Essentials の ISO ファイルから起動可能な USB フラッシュ ドライブを作成します。 USB フラッシュ ドライブを使用することができますが大幅に高速インストール プロセスをフラッシュ ドライブ、DVD-ROM ドライブよりもはるかに高速データを読み取るためします。 起動可能な USB フラッシュ ドライブを作成した後は、フラッシュ ドライブに、応答ファイルを追加できます。 できます[Windows 7 USB/DVD Download Tool をダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=248282)から無料で Microsoft ストアの Web サイト。  
  
    > [!NOTE]
    >  場合は、移行先サーバーが DVD から起動しない、コンピューターを再起動していることを確認する BIOS 設定を確認して**DVD-ROM**ブート シーケンスの最初に表示されます。 BIOS Setup の起動シーケンスを変更する方法の詳細については、ハードウェアの製造元のドキュメントを参照してください。  
  
2.  をクリックして**新規インストール**します。  
  
3.  をクリックした場合、一覧に表示されていない内部ハード ドライブ、**ドライバーの読み込み**して続行する前に、必要なドライバーをインストールします。  
  
4.  すべてのファイルを確認する] チェック ボックスをオンにし、プライマリ ハード ドライブ上のフォルダーは削除され、クリックし、**インストール**します。  
  
5.  **サーバー インストール モードの選択**] ページで [**サーバーの移行**、必要な移行情報を入力します。  
  
6.  ときに、**、サーバーが正常に移行される**メッセージが表示されたら、] をクリックして**閉じる**します。  
  
 インストールが完了したら、自動的にログオンしている管理者のユーザー アカウントと、移行応答ファイルで指定したパスワードを使用します。  
  
> [!NOTE]
>  デスクトップのロックを解除して、Windows Server Essentials のインストール中、ビルトイン administrator アカウントを使用し、パスワードを空白のままにします。  
  
##  <a name="BKMK_VerifyTheHealthOfDC"></a>ドメイン コントローラーの状態を確認します  
 移行を続行する前に、ドメイン コントローラーと Windows Server Essentials ネットワークが正常であることを確認する必要があります。  
  
 次の表に、移行先サーバーとネットワーク、およびドメインの問題の診断に使用できるツールを一覧します。  
  
|ツール|説明|  
|----------|-----------------|  
|Netdiag|ネットワークと接続の問題を切り分けることです。 詳細については、およびをダウンロードするには、「[Netdiag](https://go.microsoft.com/fwlink/?LinkId=217388)します。|  
|Dcdiag.exe|フォレストまたはエンタープライズ内のドメイン コントローラーの状態を分析し、トラブルシューティングに役立つ問題を報告します。 詳細については、およびをダウンロードするには、「[Dcdiag](https://go.microsoft.com/fwlink/?LinkId=217389)します。|  
|Repadmin.exe|ドメイン コントローラー間のレプリケーションの問題の診断に役立ちます。 このツールは、コマンド ライン パラメータを実行する必要があります。 詳細については、およびをダウンロードするには、「[Repadmin](https://go.microsoft.com/fwlink/?LinkId=217387)します。|  
  
 移行を開始する前にこれらのツールによって報告されるすべての問題を修正する必要があります。  
  
> [!NOTE]
>  電子メールを別のオンプレミス Exchange サーバーに移行する場合を参照してください。[社内 Exchange Server を Windows Server Essentials と統合](../manage/Integrate-an-On-Premises-Exchange-Server-with-Windows-Server-Essentials.md)内部設置型 Exchange server をセットアップする方法についてはします。
