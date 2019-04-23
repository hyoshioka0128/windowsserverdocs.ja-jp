---
ms.assetid: 45a65504-70b5-46ea-b2e0-db45263fabaa
title: 仮想化ドメイン コントローラー用 Hyper-V レプリカの使用のサポート
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0203c6de55a4e691d7c484351a3280c49891f317
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866283"
---
# <a name="support-for-using-hyper-v-replica-for-virtualized-domain-controllers"></a>仮想化ドメイン コントローラー用 Hyper-V レプリカの使用のサポート

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

このトピックでは、Hyper-V レプリカを使用して、ドメイン コントローラー (DC) として実行される仮想マシン (VM) をレプリケートする際のサポートについて説明します。 Hyper-V レプリカは、VM レベルでビルトイン レプリケーション メカニズムを提供する Hyper-V の新機能で、Windows Server 2012 以降に用意されています。  
  
Hyper-V レプリカは、選択された VM を、LAN リンクまたは WAN リンクを介して、プライマリ Hyper-V ホストからレプリカ Hyper-V ホストに非同期的にレプリケートします。 初期レプリケーションが完了すると、以降の変更は管理者が定義した間隔でレプリケートされます。  
  
フェールオーバーは計画的または非計画的に行うことができます。 計画フェールオーバーはプライマリ VM で管理者が開始します。レプリケートされていない変更はすべて、データ損失を防ぐためにレプリカ VM にコピーされます。 計画外のフェールオーバーは、プライマリ VM の予期しないエラーに応じてレプリカ VM で開始されます。 プライマリ VM にまだレプリケートされていない可能性がある変更があっても、その変更を転送する機会がないため、データ損失が発生する可能性があります。  
  
Hyper-V レプリカの詳細については、「 [Hyper-V レプリカの概要](https://technet.microsoft.com/library/jj134172.aspx) 」および「 [Hyper-V レプリカの展開](https://technet.microsoft.com/library/jj134207.aspx)」をご覧ください。  
  
> [!NOTE]  
> Hyper-V レプリカは、Windows Server Hyper-V でのみ実行できます。Windows 8 で実行されている Hyper-V バージョンでは実行できません。  
  
## <a name="windows-server-2012-or-newer-domain-controllers-required"></a>Windows Server 2012 または新しいドメイン コント ローラーが必要です。

Windows Server 2012 の HYPER-V には、Vm-generationid (VMGenID) が導入されました。 VMGenID により、ハイパーバイザーは、重要な変更が発生したタイミングをゲスト OS に伝えることができます。 たとえば、スナップショットからの復元が発生したことを仮想化 DC に伝えることができます (バックアップ復元ではなく、Hyper-V スナップショット復元テクノロジ)。 Windows Server 2012 以降の AD DS は VMGenID VM テクノロジを認識と、自体の保護を強化するため、スナップショット復元などのハイパーバイザー操作が実行されるときを検出するために使用します。  
  
> [!NOTE]
> AD DS のみ以降では、Windows Server 2012 Dc は VMGenID によるこうした安全対策を提供します。Windows Server のすべての以前のリリースを実行している Dc では、スナップショット復元など、サポートされていないメカニズムを使用して仮想化 DC を復元するときに発生する可能性が USN のロールバックなどの問題。 これらのセーフガードの詳細、およびトリガーされるタイミングの詳細については、「 [仮想化ドメイン コントローラーのアーキテクチャ](https://technet.microsoft.com/library/jj574118.aspx)」をご覧ください。  
  
HYPER-V レプリカのフェールオーバー (計画または計画外) が発生したときに、仮想化 DC は、前述の安全機能をトリガーするは VMGenID リセットを検出します。 Active Directory の操作が通常どおり行われ、 レプリカ VM は、プライマリ VM の代わりに実行されます。  
  
> [!NOTE]  
> 同じ DC IDの 2 つのインスタンスがあるため、プライマリ インスタンスとレプリケートされたインスタンスの両方が実行される可能性があります。 Hyper-V レプリカには、プライマリ VM とレプリカ VM が同時に実行されないようにするための制御メカニズムがありますが、VM のレプリケーション後にこの 2 つの VM 間のリンクにエラーが発生すると、その VM は同時に実行される可能性があります。 この好ましくない状況が発生しても、Windows Server 2012 が実行されている仮想化 DC には、AD DS の保護をサポートするセーフガードが用意されています。一方、前のバージョンの Windows Server が実行されている仮想化 DC には用意されていません。  
  
Hyper-V レプリカを使用する場合は、必ず [Hyper-V で仮想ドメイン コントローラーを実行する](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=WS.10).aspx)ためのベスト プラクティスに従ってください。 ここでは、たとえば、Active Directory ファイルを仮想 SCSI ディスクに格納する際の推奨事項について説明します。これにより、データの永続性がさらに強力に保証されます。  
  
## <a name="supported-and-unsupported-scenarios"></a>サポートされているシナリオとサポートされていないシナリオ

Vm の計画外のフェールオーバーとフェールオーバーをテストするための Windows Server 2012 を実行または新しいをサポートすることだけです。 計画のフェールオーバーについても Windows Server 2012 以降は、管理者は、プライマリ VM と、レプリケートされた VM の両方を誤って開始すると同時に、リスクを軽減するために、仮想化 DC の推奨します。  
  
以前のバージョンの Windows Server が実行されている VM は、計画フェールオーバーではサポートされますが、計画外フェールオーバーでは USN ロールバックの可能性があるためサポートされていません。 USN ロールバックの詳細については、 [USN および USN ロールバックに関するページ](https://technet.microsoft.com/library/d2cae85b-41ac-497f-8cd1-5fbaa6740ffe(v=ws.10))をご覧ください。  
  
> [!NOTE]  
> ドメインまたはフォレストの機能レベルの要件はありません。Hyper-V レプリカを使用してレプリケートされた VM として実行される DC のオペレーティング システムの要件のみがあります。 VM は、以前のバージョンの Windows Server が実行されている他の物理または仮想 DC が含まれるフォレストにデプロイできます。また、Hyper-V レプリカを使用してレプリケートされている場合もあれば、レプリケートされていない場合もあります。  
  
このサポート文書は、単一ドメイン フォレストで実行されたテストに基づいていますが、マルチドメイン フォレスト構成もサポートされています。 これらのテストでは、仮想化ドメイン コントローラー DC1 および DC2 は、同じサイトの Active Directory レプリケーション パートナーで、Windows Server 2012 で Hyper-V を実行するサーバーでホストされています。 DC2 が実行されている VM ゲストでは、Hyper-V レプリカが有効になっています。 レプリカ サーバーは、地理的に離れた他のデータセンターでホストされています。 以下のテスト ケース プロセスでは説明しやすいように、レプリカ サーバーで実行されている VM は DC2-Rec と呼ばれます (実際は、元の VM と同じ名前になります)。  
  
### <a name="windows-server-2012"></a>Windows Server 2012

次の表では、Windows Server 2012 およびテスト ケースが実行されている仮想化 DC のサポートについて説明します。  
  
|||  
|-|-|  
|計画フェールオーバー|計画外フェールオーバー|  
|サポートされている|サポートされている|  
|テスト ケース:<br /><br />DC1 と DC2 は、Windows Server 2012 を実行しています。<br /><br />-DC2 がシャット ダウンし、DC2 Rec でフェールオーバーを実行します。フェールオーバーは計画的または非計画的に行うことができます。<br /><br />-そのデータベースでは VMGenID の値が値と同じかどうかを確認します DC2 Rec の起動後、HYPER-V レプリカ サーバーによって保存された仮想マシン ドライバーから。<br /><br />、DC2 Rec が仮想化のセーフガードをトリガーするその結果、つまり、InvocationID をリセットが、その RID プールを破棄および操作マスターの役割を前提としていますが、前に、初期同期要件を設定します。 初期同期要件の詳細については、以下を参照してください。<br /><br />DC2-Rec は VMGenID の新しい値をそのデータベースに保存し、新しい InvocationID のコンテキストでの後続の更新をコミットします。<br /><br />-の結果として、InvocationID リセット DC1 が収束時間でロールバックされた場合でも、DC2 Rec によって導入されたすべての AD 変更でつまりすべての AD 更新が安全に収束は、フェールオーバー後に DC2 Rec で実行|テスト ケースは、次の例外を除き、計画フェールオーバーのものと同じです。<br /><br />-任意の AD では、DC2 で受け取ったソフトウェア更新プログラムがレプリケートされていない AD によってレプリケーション パートナーをフェールオーバー イベントが失われる前にします。<br /><br />-で受け取った AD 更新 DC2 後、DC1 に AD によってレプリケートされた回復ポイントの時刻は、DC1 から DC2 Rec にレプリケートされます。|  
  
### <a name="windows-server-2008-r2-and-earlier-versions"></a>Windows Server 2008 R2 以前のバージョン

次の表では、Windows Server 2008 R2 以前のバージョンが実行されている仮想化 DC のサポートについて説明します。  
  
|||  
|-|-|  
|計画フェールオーバー|計画外フェールオーバー|  
|サポートされていますが、お勧めしません。これらのバージョンの Windows Server が実行されている DC では VMGenID がサポートされていないか、または関連する仮想化セーフガードが使用されないからです。 これにより、USN ロールバックが発生するリスクがあります。 詳細については、 [USN および USN ロールバックに関するページ](https://technet.microsoft.com/library/d2cae85b-41ac-497f-8cd1-5fbaa6740ffe(v=ws.10))をご覧ください。|サポートされていません**に注意してください。** 計画外のフェールオーバーは、USN ロールバックが 1 つの DC でフォレスト (は使用しないで構成) などのリスク、サポートされます。|  
|テスト ケース:<br /><br />DC1 と DC2 は、Windows Server 2008 R2 を実行しています。<br /><br />-DC2 がシャット ダウンし、DC2 Rec で計画されたフェールオーバーを実行します。DC2 のすべてのデータが、シャットダウン完了前に DC2-Rec にレプリケートされます。<br /><br />-DC2 Rec の起動後、DC2 と同じ invocationID を使用して DC1 でレプリケーションを再開します。|なし|  
