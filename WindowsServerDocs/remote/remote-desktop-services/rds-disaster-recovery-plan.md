---
title: ディザスター リカバリー計画を作成する
description: RDS デプロイのディザスター リカバリー計画を作成する方法について説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 05/05/2017
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: 8ad759a73e4a0ce1dc28f2b8e8d80f4365895430
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879503"
---
# <a name="create-your-disaster-recovery-plan-for-rds"></a>RDS のディザスター リカバリー計画を作成します。

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

フェールオーバー プロセスを自動化する Azure Site Recovery でディザスター リカバリー計画を作成できます。 RDS のコンポーネントのすべての Vm を復旧計画に追加します。

Azure で復旧計画を作成するのに、次の手順を使用します。

1. Azure portal で Azure Site Recovery コンテナーを開き、クリックして**復旧計画**します。
2. クリックして**作成**プランの名前を入力します。
3. 選択、**ソース**と**ターゲット**します。 対象は、セカンダリ サイトの RDS または Azure です。
4. クリックして、RDS のコンポーネントをホストする Vm を選択する**OK**します。

次のセクションでは、RDS デプロイのさまざまな種類の復旧計画の作成に関する追加情報を提供します。

## <a name="sessions-based-rds-deployment"></a>セッション ベースの RDS の展開

RDS セッション ベースの展開では、シーケンスに出現するための Vm をグループします。

1. フェールオーバー グループ 1 - セッションのホスト VM
2. フェールオーバー グループ 2 - 接続ブローカー VM
3. 3 - Web アクセスの VM のフェールオーバー グループ

ご利用のプランは次のようになります。 

![セッション ベースの RDS デプロイのディザスター リカバリー計画](media/rds-asr-session-drplan.png)

## <a name="pooled-desktops-rds-deployment"></a>プールされたデスクトップの RDS のデプロイ

RDS 展開されているプールされたデスクトップを使用して、手動の手順とスクリプトを追加する、シーケンスに出現するための Vm をグループします。

1. フェールオーバー グループ 1 の RDS 接続ブローカー VM
2. 手動アクションの 1 - DNS の更新プログラムをグループ化します。

   接続ブローカー VM で管理者特権モードで PowerShell を実行します。 次のコマンドを実行し、新しい値で、DNS が更新されることを確認するまで数分待ちます。

   ```
   ipconfig /registerdns
   ```
3. 仮想化ホストの追加 - 1 のスクリプトをグループ化

   クラウド内の各仮想化ホストで実行するには、次のスクリプトを変更します。 通常、接続ブローカーに仮想化ホストを追加した後、ホストを再起動する必要があります。 ホストは、スクリプトの実行前に保留中の再起動がないか、失敗を確認してください。

   ```
   Broker - broker.contoso.com
   Virtualization host - VH1.contoso.com

   ipmo RemoteDesktop; 
   add-rdserver –ConnectionBroker broker.contoso.com –Role RDS-VIRTUALIZATION –Server VH1.contoso.com 
   ```
4. フェールオーバー グループ 2 - VM のテンプレート
5. テンプレート VM をグループ 2 スクリプト 1 - 有効にします。
   
   テンプレート VM をセカンダリ サイトに復旧されるときに起動しますが、sysprep 済みの VM には、完全に開始できません。 RDS では、VM は、そこから、プールされた VM の構成を作成するシャット ダウンである必要があります。 そのため、無効にする必要があります。 単一の VMM サーバーがあれば、テンプレート VM 名は同じで、プライマリとセカンダリが。 そのためで指定された VM の ID を使って、*コンテキスト*以下のスクリプトの変数。 複数のテンプレートを使用する場合は、すべて無効にします。

   ```powershell
   ipmo virtualmachinemanager; 
   Foreach($vm in $VMsAsTemplate)
   {
      Get-SCVirtualMachine -ID $vm | Stop-SCVirtualMachine –Force
   } 
   ```
6. グループ 2 のスクリプトを 2 - 既存のプールされた Vm の削除

   セカンダリ サイトで新しい Vm を作成できるように、接続ブローカーからプライマリ サイトにプールされた Vm を削除する必要があります。 ここでは、プールされた VM を作成する正確なホストを指定する必要があります。 コレクションのみから Vm を削除このことに注意してください。

   ```powershell
   ipmo RemoteDesktop
   $desktops = Get-RDVirtualDesktop -CollectionName Win8Desktops; 
   Foreach($vm in $desktops){
      Remove-RDVirtualDesktopFromCollection -CollectionName Win8Desktops -VirtualDesktopName $vm.VirtualDesktopName –Force
   }
   ```
7. 手動アクションのグループ 2 - 新しいテンプレートの割り当て

   復旧サイトで新しいプールされた Vm を作成できるように、コレクションの接続ブローカーに新しいテンプレートを割り当てる必要があります。 RDS 接続ブローカーに移動し、コレクションを識別します。 プロパティを編集し、そのテンプレートとして新しい VM イメージを指定します。
8. スクリプト 3 の 2 つのグループ - すべてのプールされた Vm を再作成

   接続ブローカーを使用して復旧サイトにプールされた Vm を再作成します。 この場合、プールされた VM を作成する正確なホストを指定する必要があります。

   プールされた VM 名をプレフィックスとサフィックスを使用して、一意である必要があります。 VM 名が既に存在する場合、スクリプトは失敗します。 また、プライマリ側 Vm は、1 ~ 5、番号が復旧サイト番号から続行 6。

   ```powershell
   ipmo RemoteDesktop; 
   Add-RDVirtualDesktopToCollection -CollectionName Win8Desktops -VirtualDesktopAllocation @{"RDVH1.contoso.com" = 1} 
   ```
9. 3 - Web アクセスおよびゲートウェイ サーバー VM のフェールオーバー グループ

復旧計画は、次のようになります。

![プールされたデスクトップを使用して、RDS デプロイのディザスター リカバリー計画](media/rds-asr-pooled-drplan.png)

## <a name="personal-desktops-rds-deployment"></a>個人用デスクトップ RDS のデプロイ

パーソナル デスクトップを使用して RDS 展開は、手動の手順とスクリプトを追加する、シーケンスに出現するための Vm をグループします。

1. フェールオーバー グループ 1 の RDS 接続ブローカー VM
2. 手動アクションの 1 - DNS の更新プログラムをグループ化します。

   接続ブローカー VM で管理者特権モードで PowerShell を実行します。 次のコマンドを実行し、新しい値で、DNS が更新されることを確認するまで数分待ちます。

   ```
   ipconfig /registerdns
   ```
3. グループ 1 のスクリプトの追加の仮想化ホスト
      
   クラウド内の各仮想化ホストで実行するには、次のスクリプトを変更します。 通常、接続ブローカーに仮想化ホストを追加した後、ホストを再起動する必要があります。 ホストは、スクリプトの実行前に保留中の再起動がないか、失敗を確認してください。

   ```powershell
   Broker - broker.contoso.com
   Virtualization host - VH1.contoso.com

   ipmo RemoteDesktop; 
   add-rdserver –ConnectionBroker broker.contoso.com –Role RDS-VIRTUALIZATION –Server VH1.contoso.com 
   ```
4. フェールオーバー グループ 2 - VM のテンプレート
5. テンプレート VM をグループ 2 スクリプト 1 - 有効にします。
   
   テンプレート VM をセカンダリ サイトに復旧されるときに起動しますが、sysprep 済みの VM には、完全に開始できません。 RDS では、VM は、そこから、プールされた VM の構成を作成するシャット ダウンである必要があります。 そのため、無効にする必要があります。 単一の VMM サーバーがあれば、テンプレート VM 名は同じで、プライマリとセカンダリが。 そのためで指定された VM の ID を使って、*コンテキスト*以下のスクリプトの変数。 複数のテンプレートを使用する場合は、すべて無効にします。

   ```powershell
   ipmo virtualmachinemanager; 
   Foreach($vm in $VMsAsTemplate)
   {
      Get-SCVirtualMachine -ID $vm | Stop-SCVirtualMachine –Force
   } 
   ```
6. フェールオーバー グループ 3 - パーソナル Vm
7. グループ 3 のスクリプトを 1 - 個人の既存の Vm を削除して追加

   セカンダリ サイトで新しい Vm を作成できるように、接続ブローカーからプライマリ サイトで個人、Vm を削除します。 Vm の割り当てを抽出し、再割り当てのハッシュを使用して接続ブローカーに仮想マシンを追加する必要があります。 コレクションからの個人、Vm の削除のみされ追加し直す。 個人用のデスクトップの割り当てはエクスポートされ、コレクションにインポートします。

   ```powershell
   ipmo RemoteDesktop
   $desktops = Get-RDVirtualDesktop -CollectionName CEODesktops; 
   Export-RDPersonalVirtualDesktopAssignment -CollectionName CEODesktops -Path ./Desktopallocations.txt -ConnectionBroker broker.contoso.com 

   Foreach($vm in $desktops){
     Remove-RDVirtualDesktopFromCollection -CollectionName CEODesktops -VirtualDesktopName $vm.VirtualDesktopName –Force
   }
   
   Import-RDPersonalVirtualDesktopAssignment -CollectionName CEODesktops -Path ./Desktopallocations.txt -ConnectionBroker broker.contoso.com 
   ```
8. 3 - Web アクセスおよびゲートウェイ サーバー VM のフェールオーバー グループ

ご利用のプランは次のようになります。 

![個人用デスクトップ RDS のデプロイのディザスター リカバリー計画](media/rds-asr-personal-desktops-drplan.png)
