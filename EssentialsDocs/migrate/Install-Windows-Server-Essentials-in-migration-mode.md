---
title: 移行モード 1 の場合の Windows Server Essentials をインストールします。
description: Windows Server Essentials を使用する方法について説明します
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
ms.openlocfilehash: 74c40cc0f06d73a922a3d7fb819f7e71b47ac088
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66432964"
---
# <a name="install-windows-server-essentials-in-migration-mode1"></a>移行モード 1 の場合の Windows Server Essentials をインストールします。

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

Windows Server Essentials を実行しているネットワークに 1 つだけサーバーがあることができ、そのサーバーは、ネットワークのドメイン コント ローラーである必要があります。  
  
 Windows Server Essentials を移行モードでインストールするときに、インストール ウィザードは、次のタスクを実行します。  
  
1.  インストールし、移行先サーバーで、Windows Server Essentials サーバー ソフトウェアを構成します。  
  
2.  ドメイン スキーマを最新バージョンに更新します。  
  
3.  移行先サーバーを既存のドメインに参加させます。 移行プロセスが終了するまでは、移行元サーバーと移行先サーバーを同じドメインのメンバーにしておくことができます。 移行が終了した後は、21 日以内にネットワークから移行元サーバーを削除する必要があります。  
  
    > [!WARNING]
    >  ネットワークから移行元サーバーを削除するまで、21 日の猶予期間中、エラー メッセージがイベント ログに毎日追加されます。 メッセージのテキストは次のようなものです。"FSMO 役割チェックにより、ライセンス ポリシーに準拠していない状態が環境内に検出されました。 Management Server には、プライマリ ドメイン コントローラーと Active Directory ドメイン名前付けマスターの役割が必要です。 今すぐ Active Directory の役割を Management Server に移動してください。 この状態が最初に検出されてから 21 日以内に問題が修正されない場合、このサーバーは自動的にシャットダウンされます。" 猶予期間の 21 日が経過すると、移行元サーバーはシャットダウンされます。  
  
4.  操作マスター (Flexible Single Master Operations、FSMO ともいう) の役割を、移行元サーバーから移行先サーバーに転送します。 操作マスターの役割は、標準的なデータ転送、および更新方法が適切ではない場合に使用される、ドメイン コントローラーのタスクに特化されています。 移行先サーバーをドメイン コントローラーにする際、移行先サーバーが操作マスターの役割を保持する必要があります。  
  
5.  移行先サーバーをグローバル カタログ サーバーとして構成します。 グローバル カタログ サーバーとは、分散データ リポジトリを管理するドメイン コントローラーのことです。 グローバル カタログ サーバーは、Active Directory フォレスト内の各ドメインにある各オブジェクトの検索可能な部分的表現を含みます。  
  
6.  移行先サーバーをサイト ライセンス サーバーとして構成します。  
  
##  <a name="BKMK_Install"></a> 移行先サーバーでの Windows Server Essentials をインストールします。  
 をインストールして Windows Server Essentials を移行先サーバーを移行モードで構成するには、次の手順を実行します。  
  
#### <a name="to-install-windows-server-essentials-on-the-destination-server"></a>移行先サーバーで Windows Server Essentials をインストールするには  
  
1. 移行先サーバーで有効にして、Windows Server Essentials の DVD1 を DVD ドライブに挿入します。 CD または DVD から起動するかどうかを確認するメッセージが表示されたら、任意のキーを押してそうします。  
  
   > [!NOTE]
   >  使用することができます、移行先サーバーでは、USB フラッシュ ドライブからブートをサポートする場合、 **Windows 7 USB/DVD Download Tool** Windows Server Essentials の ISO ファイルから起動可能な USB フラッシュ ドライブを作成します。 USB フラッシュ ドライブの方が DVD-ROM ドライブよりデータ読み取り速度がはるかに速いので、フラッシュ ドライブを使用するとインストール プロセスの時間を大幅に短縮できます。 起動可能な USB フラッシュ ドライブを作成した後、応答ファイルをフラッシュ ドライブに追加できます。 できます[Windows 7 USB/DVD Download Tool をダウンロード](https://go.microsoft.com/fwlink/p/?LinkId=248282)Microsoft Store の web サイトは無料です。  
  
   > [!NOTE]
   >  移行先サーバーが DVD から起動しない場合は、コンピューターを再起動し、BIOS Setup の起動シーケンスで **DVD-ROM** が一覧の最初に表示されていることを確認します。 BIOS Setup の起動シーケンスを変更する方法の詳細については、ハードウェア メーカーのドキュメントを参照してください。  
  
2. **[新規インストール]** をクリックします。  
  
3. 一覧に表示されない内蔵ハード ドライブがある場合は、 **[ドライバーの読み込み]** をクリックし、必要なドライバーをインストールしてから続行します。  
  
4. プライマリ ハード ドライブのすべてのファイルとフォルダーが削除されることを確認するチェック ボックスをオンにして、 **[インストール]** をクリックします。  
  
5. **[サーバー インストール モードの選択]** ページで、 **[サーバーの移行]** をクリックし、必要な移行情報を指定します。  
  
6. **[サーバーは正常に移行されます]** というメッセージが表示されたら、 **[閉じる]** をクリックします。  
  
   インストールが終了すると、移行応答ファイルで指定した管理者ユーザー アカウントとパスワードで自動的にログオンします。  
  
> [!NOTE]
>  デスクトップのロックを解除して、Windows Server Essentials のインストール中に、ビルトイン administrator アカウントを使用して、およびパスワードを空白のままにします。  
  
##  <a name="BKMK_VerifyTheHealthOfDC"></a> ドメイン コント ローラーの正常性を確認します。  
 移行を続行する前に、ドメイン コント ローラーと Windows Server Essentials ネットワークが正常であることを確認してください。  
  
 次の表は、移行先サーバー、ネットワーク、およびドメインの問題を診断するために使用できるツールの一覧を示しています。  
  
|ツール|説明|  
|----------|-----------------|  
|Netdiag|ネットワークと接続の問題を分離するために役立ちます。 詳細とダウンロードについては、「 [Netdiag](https://go.microsoft.com/fwlink/?LinkId=217388)」を参照してください。|  
|Dcdiag.exe|フォレストまたはエンタープライズ内のドメイン コントローラーの状態を分析し、問題を報告してトラブルシューティングを支援します。 詳細とダウンロードについては、「 [Dcdiag](https://go.microsoft.com/fwlink/?LinkId=217389)」を参照してください。|  
|Repadmin.exe|ドメイン コントローラー間のレプリケーションの問題を診断するために役立ちます。 このツールを実行するには、コマンド ライン パラメーターを指定する必要があります。 詳細とダウンロードについては、「 [Repadmin](https://go.microsoft.com/fwlink/?LinkId=217387)」を参照してください。|  
  
 移行を続行する前に、これらのツールによって報告された問題をすべて修正する必要があります。  
  
> [!NOTE]
>  電子メールを別のオンプレミス Exchange サーバーに移行する場合は「 [、オンプレミスの Exchange Server を Windows Server Essentials と統合](../manage/Integrate-an-On-Premises-Exchange-Server-with-Windows-Server-Essentials.md)オンプレミス Exchange サーバーをセットアップする方法については。
