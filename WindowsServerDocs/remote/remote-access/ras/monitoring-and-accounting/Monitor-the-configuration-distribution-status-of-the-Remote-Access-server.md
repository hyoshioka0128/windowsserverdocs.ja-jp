---
title: リモート アクセス サーバーの構成配布の状態を監視する
description: このトピックでは、リモート アクセスの監視とアカウンティング Windows Server 2016 では、ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: de285d13-9e54-4c46-88f0-607182e5e3dc
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ab5deea9d594d6e9570d2472b5628a3d5fb8d616
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282725"
---
# <a name="monitor-the-configuration-distribution-status-of-the-remote-access-server"></a>リモート アクセス サーバーの構成配布の状態を監視する

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

**注:** Windows Server 2012 では、単一のリモート アクセス役割に DirectAccess とリモート アクセス サービス (RAS) を結合します。  
  
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
|警告|サーバー [*server name*] の構成は、ドメイン コントローラーから取得されていません。 GPO はリンクされていません。|GPO 内の構成はまだサーバーに届いていません。 原因として GPO がサーバーにリンクされていないことが考えられます。|サーバーに適用されている管理の対象に GPO をリンクするか、ステージング GPO のシナリオで、ステージング GPO の設定を手動でエクスポートし、それを実稼働 GPO にインポートします。 ステージング Gpo の詳細については、次を参照してください。**限られたアクセス許可を持つリモート アクセス Gpo を管理**で[Step-1-Plan-the-DirectAccess-Infrastructure](../../directaccess/single-server-advanced/Step-1-Plan-the-DirectAccess-Infrastructure.md)します。 GPO のステージング手順を参照してください。**限られたアクセス許可を持つリモート アクセス Gpo を構成する**で[手順 1。DirectAccess インフラストラクチャを構成する](../../directaccess/single-server-advanced/Step-1-Configuring-DirectAccess-Infrastructure.md)します。|  
|警告|サーバー [*server name*] の構成は、ドメイン コントローラーからまだ取得されていません。|GPO 内の構成はまだサーバーに届いていません。<br /><br />新しい構成が伝達されるまで最大 10 分かかる場合があります。|サーバー上でポリシーが更新されるまでもう少し待ちます。|  
|エラー|ドメイン コントローラーからサーバー [*server name*] の構成を取得できません。|GPO 内の構成がサーバーに届いていません。また、構成が変更されてから 10 分以上経過しています。|この問題は、次のいずれかのシナリオで発生する可能性があります。<br /><br />-サーバーには、ポリシーを更新するドメインに接続がありません。 ポリシーの更新を強制するサーバーで"gpupdate/force"を行うことができます。<br />GPO のレプリケーションは、更新された構成を取得する必要があります。<br />リモート アクセス サーバーの Active Directory サイトには、書き込み可能なドメイン コント ローラーが-はありません。<br /><br />すべてのドメイン コントローラーに GPO がレプリケートされるのを待ってから、Windows PowerShell コマンドレット **Set-DAEntryPointDC** を使って、リモート アクセス サーバーの Active Directory 内の書き込み可能ドメイン コントローラーにエントリ ポイントを関連付けます。|  
|警告|サーバー [*server name*] の構成は、ドメイン コントローラーから取得されましたが、まだ適用されていません。|GPO 内の構成はサーバーに届いていますが、まだ適用されていません。<br /><br />構成が適用されるまで最大 15 分かかる場合があります。|構成がサーバーに完全に適用されるまでもう少し待ちます。|  
|エラー|ドメイン コントローラーから取得されたサーバー [*server name*] の構成を適用できません。|GPO 内の構成はサーバーに届いていますが、正常に適用されていません。また、構成が変更されてから 15 分以上経過しています。|この問題は、次のいずれかのシナリオで発生する可能性があります。<br /><br />1. 構成の適用が進行中です。 GPO からの構成の取得に長い時間がかかった可能性があるため、エラーとして表示されます。<br />    このことが原因であるかどうかを確認するには、**タスク スケジューラ**を使って Microsoft\Windows\RemoteAccess に移動し、**RAConfigTask** が実行中であるかどうかを確認します。<br />2. **RAConfigTask** が実行中でない場合、サーバー上での構成の適用に失敗した可能性があります。<br />    **イベント ビューアー**で、リモート アクセス サーバーの操作チャネル (\Applications and Services Logs\Microsoft\Windows\RemoteAccess-RemoteAccessServer) にエラーがないかどうか確認します。<br />    リモート アクセス管理コンソールの **[操作の状況]** にエラーがないかどうか確認します。 詳細については、「[リモート アクセス サーバーとそのコンポーネントの操作状態を監視する](Monitor-the-operations-status-of-the-Remote-Access-server-and-its-components.md)」を参照してください。|  
|エラー|マルチサイト サーバー用の構成がドメイン コントローラーから取得されました。 この構成は、すべてのサーバーで一致しません。|マルチサイト展開でのサーバー GPO の構成バージョン間に不整合があります。<br /><br />すべてのエントリ ポイントのすべてのサーバー GPOが同じグローバル構成を持つことが理想ですが、何らかの理由によって同期されていません。|構成の変更に失敗し、正常にロールバックされないと、このようなことが起こる場合があります。<br /><br />すべてのサーバー GPO が同期されていたバックアップ状態から GPO を復元する必要があります。 使用できるスクリプトについては、次を参照してください。[バックアップおよびリモート アクセスの構成を復元する](https://gallery.technet.microsoft.com/Back-up-and-Restore-Remote-e157e6a6)します。|  
  


