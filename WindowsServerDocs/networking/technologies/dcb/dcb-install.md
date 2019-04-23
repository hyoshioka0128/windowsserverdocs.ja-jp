---
title: インストールのデータ センター ブリッジング (DCB) を windows サーバーまたはクライアント
description: このトピックでは、Windows Server または Windows クライアントでのデータ センター ブリッジングをインストールする方法について説明します。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: b89213d8-143a-45f3-a609-bc6a7027204c
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7c20ef027279780181ff176afa39a19f2976c4c1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845443"
---
# <a name="install-data-center-bridging-dcb-in-windows-server-2016-or-windows-10"></a>インストールのデータ センター ブリッジング\(DCB\)で Windows Server 2016 または Windows 10

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックを使用すると、Windows Server 2016 または Windows 10 に DCB をインストールするのに方法について説明します。

## <a name="prerequisites-for-using-dcb"></a>DCB を使用するための前提条件

構成および DCB を管理するための前提条件を次に示します。

### <a name="install-a-compatible-operating-system"></a>互換性のあるオペレーティング システムをインストールします。

次のオペレーティング システムで使用できるは、このガイドの DCB コマンド。

- Windows Server (半期チャネル)
- Windows Server 2016
- Windows 10\(すべてのバージョン\)

次のオペレーティング システムには、Windows Server 2016 および Windows 10 の DCB ドキュメントで使用されるコマンドと互換性がない DCB の以前のバージョンが含まれます。

- Windows Server 2012 R2
- Windows Server 2012

###  <a name="hardware-requirements"></a>ハードウェア要件

DCB のハードウェア要件の一覧を次に示します。

- DCB\-対応のイーサネット ネットワーク アダプター\(s\) Windows Server 2016 の DCB を提供しているコンピューターにインストールする必要があります。
- DCB\-対応のハードウェア スイッチは、ネットワークに展開する必要があります。


## <a name="install-dcb-in-windows-server-2016"></a>DCB を Windows Server 2016 をインストールします。

次のセクションを使用して、Windows Server 2016 を実行しているコンピューターに DCB をインストールすることができます。

**管理者の資格情報**

これらの手順を実行する**管理者**します。

### <a name="install-dcb-using-windows-powershell"></a>Windows PowerShell を使用して DCB をインストールします。

次の手順を使用すると、Windows PowerShell を使用して DCB をインストールします。

1. を Windows Server 2016 を実行するコンピューターで次のようにクリックします。**開始**、Windows PowerShell アイコンを右クリックします。 メニューが表示されます。 メニューで、次のようにクリックします。**詳細**、 をクリックし、**管理者として実行**します。 メッセージが表示されたら、コンピューターで管理者特権を持つアカウントの資格情報を入力します。 Windows PowerShell を管理者特権で開きます。
2. 次のコマンドを入力し、Enter キーを押します。

````
    Install-WindowsFeature -Name Data-Center-Bridging -IncludeManagementTools
````

### <a name="install-dcb-using-server-manager"></a>サーバー マネージャーを使用して DCB をインストールします。

次の手順を使用して、サーバー マネージャーを使用して DCB をインストールすることができます。

>[!NOTE]
>この手順で最初の手順を実行した後、**開始する前に**以前選択した場合、追加の役割と機能のウィザードのページが表示されない**既定でこのページをスキップ**ときの追加役割と機能ウィザードが実行されました。 場合、**開始する前に**ページが表示されない場合、手順 1. から手順 3. に進んでください。

1. Dc1 のサーバー マネージャーで、**管理**、 をクリックし、**追加の役割と機能の**。 役割と機能の追加ウィザードが起動されます。
2. **開始する前に**, 、クリックして **次**します。
3. **[インストールの種類の選択]** で **[役割ベースまたは機能ベースのインストール]** が選択されていることを確認して、**[次へ]** をクリックします。
4. **[対象サーバーの選択]** で、**[サーバー プールからサーバーを選択]** が選択されていることを確認します。 **[サーバー プール]** で、ローカル コンピューターが選択されていることを確認します。 **[次へ]** をクリックします。
5. **[サーバーの役割の選択]** で、**[次へ]** をクリックします。
6. **機能の選択**の**機能**、 をクリックして**データ センター ブリッジング**します。 かどうかは、DCB が必要な機能を追加するかを確認するダイアログ ボックスが開きます。 クリックして **機能を追加**します。
7. **機能の選択**, をクリックして **次**します。 
8. 7. で**インストール オプションの確認**、 をクリックして**インストール**します。 **インストールの進行状況**ページには、インストール プロセス中に状態が表示されます。 インストールが成功したというメッセージが表示された後で、**閉じる**します。

### <a name="configure-the-kernel-debugger-to-allow-qos-optional"></a>QoS を許可するカーネル デバッガーを構成する\((省略可能)\)

 既定では、カーネル デバッガーは NetQos をブロックします。 コンピューターにインストールされているカーネル デバッガーがある場合は、DCB には、インストールに使用するメソッドに関係なく、QoS を有効にし、次のコマンドを実行して、構成するようにデバッガーを構成する必要があります。

````
Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 -Force
````

## <a name="install-dcb-in-windows-10"></a>Windows 10 での DCB をインストールします。

Windows 10 コンピューターでは、次の手順を実行できます。

この手順を実行する**管理者**します。

### <a name="install-dcb"></a>DCB のインストール

1. クリックして**開始**下へスクロールして をクリックして**Windows システム**します。
2. **[コントロール パネル]** をクリックします。 **コントロール パネルの [** ] ダイアログ ボックスが表示されます。
3. **コントロール パネルの **、 をクリックして**によって表示**、 をクリックし、**大きいアイコン**または**小さいアイコン**します。
4. クリックして**プログラムと機能**します。 プログラムと機能 ダイアログ ボックスが開きます。
5. **プログラムと機能**、左側のウィンドウで次のようにクリックします。**オンまたはオフにする Windows 機能**します。 **Windows 機能** ダイアログ ボックスが表示されます。
6. **Windows 機能**、 をクリックして**データ センター ブリッジング**、順にクリックします**OK**します。

![Windows 機能オン/オフ ダイアログ ボックス](../../media/Dcb-Scripting/Dcb-Scripting.jpg)


