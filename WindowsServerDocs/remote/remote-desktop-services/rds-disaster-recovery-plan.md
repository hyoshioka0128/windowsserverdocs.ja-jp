---
title: ディザスター リカバリー計画を作成する
description: RDS 展開のディザスター リカバリー計画を作成する方法について説明します。
ms.author: elizapo
ms.date: 05/05/2017
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: e7bf323d1a0506e9f9718d2afb8da392f0118929
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87961736"
---
# <a name="create-your-disaster-recovery-plan-for-rds"></a>RDS のディザスター リカバリー計画を作成する

>適用先:Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016

Azure Site Recovery でディザスター リカバリー計画を作成し、フェールオーバー プロセスを自動化することができます。 リカバリー計画には、すべての RDS コンポーネント VM を追加します。

Azure で次の手順を使用してリカバリー計画を作成します。

1. Azure portal で Azure Site Recovery 資格情報コンテナーを開き、 **[復旧計画]** をクリックします。
2. **[作成]** をクリックして計画の名前を入力します。
3. **[ソース]** と **[ターゲット]** を選択します。 ターゲットは、セカンダリ RDS サイトか Azure のいずれかです。
4. RDS コンポーネントをホストする VM を選択し、 **[OK]** をクリックします。

以降のセクションでは、さまざまな種類の RDS 展開のリカバリー計画の作成に関する追加情報を提供します。

## <a name="sessions-based-rds-deployment"></a>セッション ベースの RDS 展開

RDS のセッション ベースの展開では、VM が正しい順序で切り替わるようにグループ化します。

1. フェールオーバー グループ 1 - セッション ホスト VM
2. フェールオーバー グループ 2 - 接続ブローカー VM
3. フェールオーバー グループ 3 - Web アクセス VM

計画は次のようになります。

![セッション ベースの RDS 展開のディザスター リカバリー計画](media/rds-asr-session-drplan.png)

## <a name="pooled-desktops-rds-deployment"></a>プールされたデスクトップを含む RDS 展開

プールされたデスクトップを含む RDS 展開の場合、手動の手順とスクリプトを追加して、VM が正しい順序で切り替わるようにグループ化します。

1. フェールオーバー グループ 1 - RDS 接続ブローカー VM
2. グループ 1 の手動アクション - DNS の更新

   接続ブローカー VM 上で管理者特権モードで PowerShell を実行します。 次のコマンドを実行し、数分待って DNS が新しい値に更新されたことを確認します。

   ```
   ipconfig /registerdns
   ```
3. グループ 1 のスクリプト - 仮想化ホストの追加

   次のスクリプトを、クラウド内の各仮想化ホストに対して実行するように変更します。 通常は、接続ブローカーに仮想化ホストを追加した後に、ホストを再起動する必要があります。 ホストに保留中の再起動がないことを確認してから、スクリプトを実行してください。そうしないと失敗します。

   ```
   Broker - broker.contoso.com
   Virtualization host - VH1.contoso.com

   ipmo RemoteDesktop;
   add-rdserver –ConnectionBroker broker.contoso.com –Role RDS-VIRTUALIZATION –Server VH1.contoso.com
   ```
4. フェールオーバー グループ 2 - テンプレート VM
5. グループ 2 のスクリプト 1 - テンプレート VM の無効化

   テンプレート VM は、セカンダリ サイトに復旧されると起動しますが、これはシステムで準備された VM であり、完全には起動できません。 また、この VM は、RDS がプールされた VM 構成を作成するために、シャットダウンされている必要があります。 そのため、これを無効にする必要があります。 単一の VMM サーバーを使用している場合、テンプレート VM 名は、プライマリとセカンダリで同じになります。 そのため、次のスクリプトの *Context* 変数で指定された VM ID を使用します。 複数のテンプレートを使用している場合は、そのすべてを無効にします。

   ```powershell
   ipmo virtualmachinemanager;
   Foreach($vm in $VMsAsTemplate)
   {
      Get-SCVirtualMachine -ID $vm | Stop-SCVirtualMachine –Force
   }
   ```
6. グループ 2 のスクリプト 2 - 既存のプールされた VM の削除

   セカンダリ サイトに新しい VM を作成できるように、プライマリ サイト上のプールされた VM を接続ブローカーから削除する必要があります。 この場合、プールされた VM の作成先となるホストを正確に指定する必要があります。 VM はコレクションのみから削除されることに注意してください。

   ```powershell
   ipmo RemoteDesktop
   $desktops = Get-RDVirtualDesktop -CollectionName Win8Desktops;
   Foreach($vm in $desktops){
      Remove-RDVirtualDesktopFromCollection -CollectionName Win8Desktops -VirtualDesktopName $vm.VirtualDesktopName –Force
   }
   ```
7. グループ 2 の手動アクション - 新しいテンプレートの割り当て

   復旧サイトに新しいプールされた VM を作成できるように、コレクションの接続ブローカーに新しいテンプレートを割り当てる必要があります。 RDS 接続ブローカーに移動し、コレクションを特定します。 プロパティを編集し、新しい VM イメージをそのテンプレートとして指定します。
8. グループ 2 のスクリプト 3 - すべてのプールされた VM の再作成

   接続ブローカーを使用して、復旧サイトにプールされた VM を再作成します。 この場合、プールされた VM の作成先となるホストを正確に指定する必要があります。

   プールされた VM 名は、プレフィックスとサフィックスを使用して、一意になるようにします。 VM 名が既に存在する場合、スクリプトは失敗します。 また、プライマリ側の VM に 1 から 5 の番号が付けられている場合、復旧サイトでは 6 から継続されます。

   ```powershell
   ipmo RemoteDesktop;
   Add-RDVirtualDesktopToCollection -CollectionName Win8Desktops -VirtualDesktopAllocation @{"RDVH1.contoso.com" = 1}
   ```
9. フェールオーバー グループ 3 - Web アクセスおよびゲートウェイ サーバー VM

リカバリー計画は次のようになります。

![プールされたデスクトップを含む RDS 展開のディザスター リカバリー計画](media/rds-asr-pooled-drplan.png)

## <a name="personal-desktops-rds-deployment"></a>個人用デスクトップを含む RDS 展開

個人用デスクトップを含む RDS 展開の場合、手動の手順とスクリプトを追加して、VM が正しい順序で切り替わるようにグループ化します。

1. フェールオーバー グループ 1 - RDS 接続ブローカー VM
2. グループ 1 の手動アクション - DNS の更新

   接続ブローカー VM 上で管理者特権モードで PowerShell を実行します。 次のコマンドを実行し、数分待って DNS が新しい値に更新されたことを確認します。

   ```
   ipconfig /registerdns
   ```
3. グループ 1 のスクリプト - 仮想化ホストの追加

   次のスクリプトを、クラウド内の各仮想化ホストに対して実行するように変更します。 通常は、接続ブローカーに仮想化ホストを追加した後に、ホストを再起動する必要があります。 ホストに保留中の再起動がないことを確認してから、スクリプトを実行してください。そうしないと失敗します。

   ```powershell
   Broker - broker.contoso.com
   Virtualization host - VH1.contoso.com

   ipmo RemoteDesktop;
   add-rdserver –ConnectionBroker broker.contoso.com –Role RDS-VIRTUALIZATION –Server VH1.contoso.com
   ```
4. フェールオーバー グループ 2 - テンプレート VM
5. グループ 2 のスクリプト 1 - テンプレート VM の無効化

   テンプレート VM は、セカンダリ サイトに復旧されると起動しますが、これはシステムで準備された VM であり、完全には起動できません。 また、この VM は、RDS がプールされた VM 構成を作成するために、シャットダウンされている必要があります。 そのため、これを無効にする必要があります。 単一の VMM サーバーを使用している場合、テンプレート VM 名は、プライマリとセカンダリで同じになります。 そのため、次のスクリプトの *Context* 変数で指定された VM ID を使用します。 複数のテンプレートを使用している場合は、そのすべてを無効にします。

   ```powershell
   ipmo virtualmachinemanager;
   Foreach($vm in $VMsAsTemplate)
   {
      Get-SCVirtualMachine -ID $vm | Stop-SCVirtualMachine –Force
   }
   ```
6. フェールオーバー グループ 3 - 個人用 VM
7. グループ 3 のスクリプト 1 - 既存の個人用 VM の削除と追加

   セカンダリ サイトに新しい VM を作成できるように、プライマリ サイト上の個人用 VM を接続ブローカーから削除します。 VM の割り当てを抽出し、割り当てのハッシュを使用して仮想マシンを接続ブローカーに再び追加する必要があります。 単に個人用 VM をコレクションから削除し、再び追加するだけです。 個人用デスクトップの割り当てがエクスポートされ、コレクションに再びインポートされます。

   ```powershell
   ipmo RemoteDesktop
   $desktops = Get-RDVirtualDesktop -CollectionName CEODesktops;
   Export-RDPersonalVirtualDesktopAssignment -CollectionName CEODesktops -Path ./Desktopallocations.txt -ConnectionBroker broker.contoso.com

   Foreach($vm in $desktops){
     Remove-RDVirtualDesktopFromCollection -CollectionName CEODesktops -VirtualDesktopName $vm.VirtualDesktopName –Force
   }

   Import-RDPersonalVirtualDesktopAssignment -CollectionName CEODesktops -Path ./Desktopallocations.txt -ConnectionBroker broker.contoso.com
   ```
8. フェールオーバー グループ 3 - Web アクセスおよびゲートウェイ サーバー VM

計画は次のようになります。

![個人用デスクトップを含む RDS 展開のディザスター リカバリー計画](media/rds-asr-personal-desktops-drplan.png)
