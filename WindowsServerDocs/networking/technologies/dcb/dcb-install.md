---
title: Windows Server またはクライアントにデータセンターブリッジング (DCB) をインストールする
description: このトピックでは、Windows Server または Windows クライアントにデータセンターブリッジングをインストールする方法について説明します。
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: b89213d8-143a-45f3-a609-bc6a7027204c
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 5ecb6ef072dd2328a0a45d57d181dca9c2928a30
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405785"
---
# <a name="install-data-center-bridging-dcb-in-windows-server-2016-or-windows-10"></a>Windows Server 2016 または Windows 10 でデータセンターブリッジング \(DCB\) をインストールする

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、Windows Server 2016 または Windows 10 で DCB をインストールする方法について説明します。

## <a name="prerequisites-for-using-dcb"></a>DCB を使用するための前提条件

DCB を構成および管理するための前提条件は次のとおりです。

### <a name="install-a-compatible-operating-system"></a>互換性のあるオペレーティングシステムをインストールする

このガイドの DCB コマンドは、次のオペレーティングシステムで使用できます。

- Windows Server (半期チャネル)
- Windows Server 2016
- Windows 10 \(すべてのバージョン\)

次のオペレーティングシステムには、Windows Server 2016 および Windows 10 の DCB ドキュメントで使用されるコマンドと互換性のない、以前のバージョンの DCB が含まれています。

- Windows Server 2012 R2
- Windows Server 2012

###  <a name="hardware-requirements"></a>ハードウェア要件

DCB のハードウェア要件の一覧を次に示します。

- DCB\-対応イーサネットネットワークアダプター\(s\) は、Windows Server 2016 DCB を提供しているコンピューターにインストールする必要があります。
- DCB\-対応のハードウェアスイッチをネットワーク上に展開する必要があります。


## <a name="install-dcb-in-windows-server-2016"></a>Windows Server 2016 に DCB をインストールする

Windows Server 2016 を実行しているコンピューターに DCB をインストールするには、次のセクションを使用します。

**管理者の資格情報**

これらの手順を実行するには、 **Administrators**のメンバーである必要があります。

### <a name="install-dcb-using-windows-powershell"></a>Windows PowerShell を使用して DCB をインストールする

Windows PowerShell を使用して DCB をインストールするには、次の手順を実行します。

1. Windows Server 2016 を実行しているコンピューターで、**スタート** をクリックし、windows PowerShell アイコンを右クリックします。 メニューが表示されます。 メニューで **[詳細]** をクリックし、 **[管理者として実行]** をクリックします。 メッセージが表示されたら、コンピューターに対する管理者特権を持つアカウントの資格情報を入力します。 Windows PowerShell が管理者特権で開きます。
2. 次のコマンドを入力し、Enter キーを押します。

````
    Install-WindowsFeature -Name Data-Center-Bridging -IncludeManagementTools
````

### <a name="install-dcb-using-server-manager"></a>サーバーマネージャーを使用して DCB をインストールする

サーバーマネージャーを使用して DCB をインストールするには、次の手順を実行します。

>[!NOTE]
>この手順の最初の手順を実行した後は、役割と機能の追加ウィザードの **[開始する前に]** ページが表示されません。以前に 役割と機能の追加ウィザードの実行時に、 **[既定でこのページをスキップ]** する を選択している場合です。 **[開始する前に]** ページが表示されない場合は、手順 1. から手順 3. に進みます。

1. DC1 の サーバーマネージャーで、 **[管理]** をクリックし、 **[役割と機能の追加]** をクリックします。 役割と機能の追加ウィザードが起動されます。
2. **開始する前に**, 、クリックして **次**します。
3. **[インストールの種類の選択]** で **[役割ベースまたは機能ベースのインストール]** が選択されていることを確認して、 **[次へ]** をクリックします。
4. **[対象サーバーの選択]** で、 **[サーバー プールからサーバーを選択]** が選択されていることを確認します。 **[サーバー プール]** で、ローカル コンピューターが選択されていることを確認します。 **[次へ]** をクリックします。
5. **[サーバーの役割の選択]** で、 **[次へ]** をクリックします。
6. **[機能の選択]** の **[機能]** で、 **[データセンターブリッジング]** をクリックします。 DCB に必要な機能を追加するかどうかを確認するダイアログボックスが表示されます。 クリックして **機能を追加**します。
7. **機能の選択**, をクリックして **次**します。 
8. 7.In**インストールオプションを確認**し、 **[インストール]** をクリックします。 インストール処理中の **[インストールの進行状況]** ページに状態が表示されます。 インストールが成功したことを示すメッセージが表示されたら、 **[閉じる]** をクリックします。

### <a name="configure-the-kernel-debugger-to-allow-qos-optional"></a>QoS \(オプションを許可するようにカーネルデバッガーを構成し\)

 既定では、カーネルデバッガーは NetQos をブロックします。 DCB のインストールに使用した方法に関係なく、コンピューターにカーネルデバッガーがインストールされている場合は、次のコマンドを実行して、QoS が有効になって構成されるように、デバッガーを構成する必要があります。

````
Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 -Force
````

## <a name="install-dcb-in-windows-10"></a>Windows 10 で DCB をインストールする

Windows 10 コンピューターでは、次の手順を実行できます。

この手順を実行するには、 **Administrators**のメンバーである必要があります。

### <a name="install-dcb"></a>DCB のインストール

1. **[スタート]** をクリックし、下にスクロールして **[Windows システム]** をクリックします。
2. **[コントロール パネル]** をクリックします。 **[コントロールパネル]** ダイアログボックスが表示されます。
3. **[コントロールパネル]** で、 **[表示]** 方法 をクリックし、 **[大きいアイコン]** または **[小さいアイコン]** をクリックします。
4. [**プログラムと機能] を**クリックします。 [プログラムと機能] ダイアログボックスが表示されます。
5. **[プログラムと機能]** の左側のウィンドウで、 **[Windows の機能の有効化または無効化]** をクリックします。 **[Windows の機能]** ダイアログボックスが表示されます。
6. **[Windows の機能]** で、 **[データセンターブリッジング]** をクリックし、 **[OK]** をクリックします。

![[Windows の機能の有効化または無効化] ダイアログボックス](../../media/Dcb-Scripting/Dcb-Scripting.jpg)


