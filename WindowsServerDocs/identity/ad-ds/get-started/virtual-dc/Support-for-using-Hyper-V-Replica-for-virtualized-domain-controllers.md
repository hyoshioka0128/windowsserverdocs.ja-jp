---
ms.assetid: 45a65504-70b5-46ea-b2e0-db45263fabaa
title: "仮想化ドメイン コント ローラー用 HYPER-V レプリカを使用するためのサポート"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0444198196ed08a22aba92a0f59cc6e7a2518a2e
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="support-for-using-hyper-v-replica-for-virtualized-domain-controllers"></a>仮想化ドメイン コント ローラー用 HYPER-V レプリカを使用するためのサポート

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、Hyper-V レプリカを使用して、ドメイン コントローラー (DC) として実行される仮想マシン (VM) をレプリケートするのサポートについて説明します。 Hyper-V レプリカは、以降、VM レベルでビルトイン レプリケーション メカニズムを提供する Windows Server 2012 では Hyper-V の新機能です。  
  
Hyper-V レプリカは、選択された Vm をプライマリ Hyper-v ホストをレプリカ Hyper-V ホストから、LAN または WAN リンクのいずれかの間で非同期的にレプリケートされます。 初期レプリケーションが完了したら、それ以降の変更は、管理者が定義した間隔でレプリケートされます。  
  
フェールオーバーは計画または計画外のいずれかにできます。 計画フェールオーバーは、プライマリ VM 上の管理者によって開始され、レプリケートされていない変更は、レプリカ データの消失を防ぐために VM にコピーします。 プライマリ VM の予期しないエラーに応じてレプリカ VM では、計画外のフェールオーバーが開始されます。 データの損失が発生する可能性がありますがまだレプリケートされていませんが、プライマリ VM での変更を転送する機会がないためです。  
  
Hyper-V レプリカの詳細については、次を参照してください。[Hyper-v レプリカの概要](https://technet.microsoft.com/library/jj134172.aspx)と[Hyper-v レプリカの展開](https://technet.microsoft.com/library/jj134207.aspx)します。  
  
> [!NOTE]  
> Hyper-V レプリカは、だけで Windows Server Hyper-V、Windows 8 で実行されている Hyper-V のバージョンではなく実行できます。  
  
## <a name="windows-server-2012-domain-controllers-required"></a>必要な Windows Server 2012 ドメイン コントローラー  
Windows Server 2012 の Hyper-V には、VM-GenerationID (VMGenID) も導入されています。 VMGenID により、ハイパーバイザーはゲスト OS の重要な変更が発生したときに通信にします。 たとえば、ハイパーバイザー通信できます仮想化 DC にスナップショットからの復元には、(Hyper-V スナップショット復元テクノロジ、しないバックアップの復元) が発生しました。 Windows Server 2012 で AD DS は VMGenID VM テクノロジを認識しており、それ自体の保護を強化することができるスナップショット復元などのハイパーバイザー操作が実行されるときに検出するために使用します。  
  
> [!NOTE]  
> 点を強化するには、Windows Server 2012 Dc では AD DS のみが用意されています。VMGenID によるこうした安全対策Windows Server の以前のすべてのリリースが実行されている Dc では、スナップショット復元などのサポートされていないメカニズムを使用して仮想化 DC が復元されたときに発生する、USN ロールバックなどの問題に従います。 これらのセーフガードおよびトリガーされるタイミングに関する詳細については、次を参照してください。[仮想化ドメイン コントローラーのアーキテクチャ](https://technet.microsoft.com/library/jj574118.aspx)します。  
  
Hyper-V レプリカのフェールオーバーでは、(計画または計画外) が発生した場合、Windows Server 2012 仮想化 DC は、前述の安全機能をトリガーは VMGenID リセットを検出します。 Active Directory の操作が通常どおり行われ、します。 レプリカ VM は、プライマリ VM の代わりに実行します。  
  
> [!NOTE]  
> 考えるようになりましたが存在するようになりました同じ DC ID の 2 つのインスタンスを実行するには、プライマリ インスタンスとレプリケートされたインスタンスの両方の可能性があります。 Hyper-V レプリカ、プライマリことを保証するコントロール メカニズムとレプリカ Vm が同時に実行されません、中に、VM のレプリケーションの後にそれらの間のリンクが失敗した場合に、同時に実行する可能性があります。 このほとんどの発生が発生した場合は、Windows Server 2012 を実行している仮想化 Dc には、AD DS の保護、以前のバージョンの Windows Server を実行している Dc を仮想化されたが、そうではないをサポートするセーフガードがあります。  
  
Hyper-V レプリカを使用する場合のベスト プラクティスに従う必要があることを確認[Hyper-V で仮想ドメイン コントローラーを実行している](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=WS.10).aspx)します。 これについて説明、たとえば、Active Directory ファイル、仮想 SCSI ディスクを格納するための推奨事項データの永続性より強力な保証を提供します。  
  
## <a name="supported-and-unsupported-scenarios"></a>サポートされていると、サポートされていないシナリオ  
Windows Server 2012 を実行している Vm のみには、計画外のフェールオーバーおよびテスト フェールオーバーはサポートされています。 計画フェールオーバーは、についても Windows Server 2012 は、管理者は、プライマリ VM と、レプリケートされた VM の両方を誤って起動すると、同時にするリスクを軽減するために仮想化 DC の勧めします。  
  
以前のバージョンの Windows Server を実行している Vm は計画フェールオーバーのサポートされますが、USN ロールバックが発生する可能性のための計画外フェールオーバーのサポートされていません。 USN ロールバックの詳細については、次を参照してください。[USN と USN ロールバック](https://technet.microsoft.com/library/d2cae85b-41ac-497f-8cd1-5fbaa6740ffe(v=ws.10))します。  
  
> [!NOTE]  
> ドメインまたはフォレストの機能レベルの要件はありません。Hyper-V レプリカを使用してレプリケートされた Vm として実行される Dc のオペレーティング システム要件のみがあります。 実行している以前のバージョンの Windows Server と可能性がありますもレプリケート Hyper-V レプリカを使用して他の物理または仮想 Dc を含むフォレスト内の Vm を展開できます。  
  
このサポートに関する声明は、マルチ ドメイン フォレスト構成もサポートされていますが、単一ドメイン フォレストで実行されたテストに基づいています。 これらのテストでは、仮想化ドメイン コントローラー DC1 および DC2 は、同じサイトで Active Directory レプリケーション パートナーを Windows Server 2012 で Hyper-V を実行するサーバーでホストされています。 DC2 を実行している VM ゲストが、Hyper-V レプリカが有効にします。 レプリカ サーバーは、別の地理的に離れた場所にあるデータ センターでホストされています。 以下で説明するテスト ケース プロセスを説明するには、レプリカ サーバーで実行中の VM と呼びます DC2 Rec (ただし、実際には、元の VM と同じ名前が保持されます)。  
  
### <a name="windows-server-2012"></a>Windows Server 2012  
次の表では、Windows Server 2012 およびテスト_ケースを実行している仮想化 Dc のサポートについて説明します。  
  
|||  
|-|-|  
|計画フェールオーバー|計画外フェールオーバー|  
|サポートされています。|サポートされています。|  
|テスト_ケース:<br /><br />DC1 および DC2 は、Windows Server 2012 を実行しています。<br /><br />-DC2 がシャット ダウンし、フェールオーバーが DC2 Rec で実行します。フェールオーバーは計画または計画外のいずれかにできます。<br /><br />の自身のデータベースは VMGenID の値は、値と同じかどうかを確認開始後に DC2 Rec、Hyper-V レプリカ サーバーによって保存された仮想マシン ドライバーからです。<br /><br />-DC2 Rec が; の仮想化セーフガードをトリガーするその結果、つまり、InvocationID をリセット、その RID プールを破棄し、操作マスターの役割を前提としていますが、前に、初期同期要件を設定します。 初期同期要件の詳細についてを参照してください。<br /><br />-Rec DC2 は、VMGenID の新しい値をそのデータベースに保存し、新しい InvocationID のコンテキストでの後続の更新をコミットします。<br /><br />-の結果として、InvocationID リセット DC1 は収束を適時にロールバックされた場合でも、DC2 Rec によって導入されたすべての AD 変更であり、フェールオーバーは安全に収束後に、すべての AD 更新が DC2 Rec で実行|テストの例では、次の例外を除き、計画フェールオーバーと同じであります。<br /><br />DC2 で受け取ったを更新します-AD がレプリケートされていない AD によってレプリケーション パートナーを前に、フェールオーバー イベントが失われます。<br /><br />DC2 Rec に DC1 から AD によって DC1 にレプリケートされた回復ポイントの時刻はレプリケートされた後に DC2 で受け取った AD 更新します。|  
  
### <a name="windows-server-2008-r2-and-earlier-versions"></a>Windows Server 2008 R2 およびそれ以前のバージョン  
次の表では、Windows Server 2008 R2 およびそれ以前のバージョンを実行する仮想化 Dc のサポートについて説明します。  
  
|||  
|-|-|  
|計画フェールオーバー|計画外フェールオーバー|  
|これらのバージョンの Windows Server を実行している Dc が VMGenID をサポートしていない、または関連する仮想化セーフガードを使用しているために、推奨されませんが、サポートされます。 これにより、USN ロールバックのリスクです。 詳細については、次を参照してください。[USN と USN ロールバック](https://technet.microsoft.com/en-us/library/d2cae85b-41ac-497f-8cd1-5fbaa6740ffe(v=ws.10))します。|サポートされていません**注:**、USN ロールバックのリスクがないなど (非推奨構成)、フォレスト内の DC が 1 台の計画外フェールオーバーはサポートされます。|  
|テスト_ケース:<br /><br />DC1 および DC2 は、Windows Server 2008 R2 を実行しています。<br /><br />-DC2 がシャット ダウンし、計画フェールオーバーが DC2 Rec で実行します。DC2 のすべてのデータは、シャット ダウンが完了する前に、DC2 Rec にレプリケートされます。<br /><br />開始後に DC2 Rec、DC2 と同じ invocationID を使用して、DC1 でレプリケーションを再開します。|該当なし|  
  


