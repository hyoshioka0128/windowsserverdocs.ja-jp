---
title: リモート アクセス サーバーの構成配布の状態を監視する
description: このトピックは、Windows Server 2016 のリモートアクセスの監視とアカウンティングに関するガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: de285d13-9e54-4c46-88f0-607182e5e3dc
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3218e1110bc17979fdda949956f551997859f5ed
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71368246"
---
# <a name="monitor-the-configuration-distribution-status-of-the-remote-access-server"></a>リモート アクセス サーバーの構成配布の状態を監視する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

**注:** Windows Server 2012 は DirectAccess とリモート アクセス サービス (RAS) は単一のリモート アクセス役割に結合します。  
  
リモート アクセス管理コンソールは、すべての監視対象サーバーの構成バージョンを比較して、それらが一致していることと、最新の構成バージョンが使用されていることを確認します。 この確認によって、最新の構成バージョン (グループ ポリシー オブジェクト (GPO) 内で指定) がすべてのサーバーに配布されたかどうかと、すべてのサーバーで正常に適用されたかどうかがわかります。  
  
### <a name="to-use-the-monitoring-dashboard-to-monitor-the-configuration-distribution"></a>監視ダッシュボードを使って構成の配布を監視するには  
  
1.  **サーバー マネージャー**, をクリックして **ツール**, 、順にクリック **リモート アクセス管理**します。  
  
2.  **[ダッシュボード]** をクリックして**リモート アクセス管理コンソール**の**リモート アクセス ダッシュボード**に移動します。  
  
3.  監視ダッシュボードの上部中央にある **[構成の状態]** タイルに注目します。 このタイルには、構成配布の現在の状態が示されます。  
  
次の表に、 **[構成の状態]** タイルで生成されるメッセージ、その意味、および必要な管理操作 (ある場合) を示します。  
  
|||||  
|-|-|-|-|  
|重大度|メッセージ|説明|対処方法|  
|成功|構成が正常に配布されました。|GPO 内の構成がサーバーで正常に適用されました。|操作は必要ありません。|  
|Warning|サーバー [*server name*] の構成は、ドメイン コントローラーから取得されていません。 GPO はリンクされていません。|GPO 内の構成はまだサーバーに届いていません。 原因として GPO がサーバーにリンクされていないことが考えられます。|サーバーに適用されている管理の対象に GPO をリンクするか、ステージング GPO のシナリオで、ステージング GPO の設定を手動でエクスポートし、それを実稼働 GPO にインポートします。 ステージング Gpo の詳細については、「[手順 1-計画-DirectAccess-インフラストラクチャ](../../directaccess/single-server-advanced/Step-1-Plan-the-DirectAccess-Infrastructure.md)の**アクセス許可が制限されたリモートアクセス Gpo を管理する**」を参照してください。 GPO のステージング手順については、「[手順 1: DirectAccess インフラストラクチャを構成](../../directaccess/single-server-advanced/Step-1-Configuring-DirectAccess-Infrastructure.md)する」の「**アクセス許可が制限されたリモートアクセス Gpo を構成する**」を参照してください。|  
|Warning|サーバー [*server name*] の構成は、ドメイン コントローラーからまだ取得されていません。|GPO 内の構成はまだサーバーに届いていません。<br /><br />新しい構成が伝達されるまで最大 10 分かかる場合があります。|サーバー上でポリシーが更新されるまでもう少し待ちます。|  
|エラー|ドメイン コントローラーからサーバー [*server name*] の構成を取得できません。|GPO 内の構成がサーバーに届いていません。また、構成が変更されてから 10 分以上経過しています。|この問題は、次のいずれかのシナリオで発生する可能性があります。<br /><br />-サーバーは、ポリシーを更新するドメインに接続していません。 サーバーで "gpupdate/force" を実行して、ポリシーの更新を強制することができます。<br />-更新された構成を取得するには、GPO のレプリケーションが必要になる場合があります。<br />-リモートアクセスサーバーの Active Directory サイトに書き込み可能なドメインコントローラーがありません。<br /><br />すべてのドメイン コントローラーに GPO がレプリケートされるのを待ってから、Windows PowerShell コマンドレット **Set-DAEntryPointDC** を使って、リモート アクセス サーバーの Active Directory 内の書き込み可能ドメイン コントローラーにエントリ ポイントを関連付けます。|  
|Warning|サーバー [*server name*] の構成は、ドメイン コントローラーから取得されましたが、まだ適用されていません。|GPO 内の構成はサーバーに届いていますが、まだ適用されていません。<br /><br />構成が適用されるまで最大 15 分かかる場合があります。|構成がサーバーに完全に適用されるまでもう少し待ちます。|  
|エラー|ドメイン コントローラーから取得されたサーバー [*server name*] の構成を適用できません。|GPO 内の構成はサーバーに届いていますが、正常に適用されていません。また、構成が変更されてから 15 分以上経過しています。|この問題は、次のいずれかのシナリオで発生する可能性があります。<br /><br />1. 構成は現在適用中です。 GPO からの構成の取得に長い時間がかかった可能性があるため、エラーとして表示されます。<br />    このことが原因であるかどうかを確認するには、**タスク スケジューラ**を使って Microsoft\Windows\RemoteAccess に移動し、**RAConfigTask** が実行中であるかどうかを確認します。<br />2. **Raconfigtask**が現在実行されていない場合、サーバーに構成を適用できなかった可能性があります。<br />    **イベント ビューアー**で、リモート アクセス サーバーの操作チャネル (\Applications and Services Logs\Microsoft\Windows\RemoteAccess-RemoteAccessServer) にエラーがないかどうか確認します。<br />    リモート アクセス管理コンソールの **[操作の状況]** にエラーがないかどうか確認します。 詳細については、「[リモート アクセス サーバーとそのコンポーネントの操作状態を監視する](Monitor-the-operations-status-of-the-Remote-Access-server-and-its-components.md)」を参照してください。|  
|エラー|マルチサイト サーバー用の構成がドメイン コントローラーから取得されました。 この構成は、すべてのサーバーで一致しません。|マルチサイト展開でのサーバー GPO の構成バージョン間に不整合があります。<br /><br />すべてのエントリ ポイントのすべてのサーバー GPOが同じグローバル構成を持つことが理想ですが、何らかの理由によって同期されていません。|構成の変更に失敗し、正常にロールバックされないと、このようなことが起こる場合があります。<br /><br />すべてのサーバー GPO が同期されていたバックアップ状態から GPO を復元する必要があります。 使用できるスクリプトの詳細については、「[リモートアクセス構成のバックアップと復元](https://gallery.technet.microsoft.com/Back-up-and-Restore-Remote-e157e6a6)」を参照してください。|  
  


