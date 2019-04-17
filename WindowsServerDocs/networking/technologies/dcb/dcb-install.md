---
title: インストールのデータ センター ブリッジング (DCB) を Windows のサーバーまたはクライアント
description: このトピックでは、Windows Server または Windows クライアントでのデータ センター ブリッジングをインストールする方法について説明します。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: b89213d8-143a-45f3-a609-bc6a7027204c
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 491bdeb1a7458be1f991be68724e7a7b51f67ecf
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="install-data-center-bridging-dcb-in-windows-server-2016-or-windows-10"></a>データ センター ブリッジング \(DCB\) Windows Server 2016 または Windows 10 でのインストールします。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、Windows Server 2016 または Windows 10 での DCB をインストールするのに方法について説明します。

## <a name="prerequisites-for-using-dcb"></a>DCB を使用するための前提条件

構成と DCB の管理の前提条件を次に示します。

### <a name="install-a-compatible-operating-system"></a>互換性のあるオペレーティング システムをインストールします。

次のオペレーティング システムでは、このガイドの DCB コマンドを使用できます。

- Windows Server (半期チャネル)
- Windows Server 2016
- Windows 10 \(all versions\)

次のオペレーティング システムには、Windows Server 2016 および Windows 10 の DCB ドキュメントで使用されているコマンドと互換性がない DCB の以前のバージョンが含まれます。

- Windows Server 2012 R2
- Windows Server 2012

###  <a name="hardware-requirements"></a>ハードウェア要件

DCB のハードウェア要件の一覧を次に示します。

- DCB\ 対応のイーサネット ネットワーク adapter\(s\) は、Windows Server 2016 の DCB を提供しているコンピューターにインストールする必要があります。
- ネットワーク上で DCB\ 対応のハードウェア スイッチを展開する必要があります。


## <a name="install-dcb-in-windows-server-2016"></a>DCB を Windows Server 2016 をインストールします。

次のセクションを使用して、Windows Server 2016 を実行しているコンピューターに DCB をインストールすることができます。

**管理者の資格情報**

これらの手順を実行するには、メンバーである**管理者**します。

### <a name="install-dcb-using-windows-powershell"></a>Windows PowerShell を使用して DCB をインストールします。

Windows PowerShell を使用して DCB をインストールするのには、次の手順を使用できます。

1. Windows Server 2016 を実行するコンピューター上] をクリックして**開始**、Windows PowerShell アイコンを右クリックします。 メニューが表示されます。 メニューで、をクリックして**詳細**、] をクリックし、**管理者として実行**します。 メッセージが表示されたら、コンピューターで管理者権限を持つアカウントの資格情報を入力します。 管理者特権で Windows PowerShell を開きます。
2. 次のコマンドを入力し、し、ENTER キーを押します。

````
    Install-WindowsFeature -Name Data-Center-Bridging -IncludeManagementTools
````

### <a name="install-dcb-using-server-manager"></a>サーバー マネージャーを使用して DCB をインストールします。

次の手順を使用して、サーバー マネージャーを使用して DCB をインストールすることができます。

>[!NOTE]
>この手順で最初の手順を実行した後、**開始する前に**以前選択した場合、追加の役割と機能のウィザードのページが表示されない**既定でこのページをスキップ**、追加の役割と機能のウィザードが実行されました。 場合、**開始する前に**ページが表示されない場合、手順 1. から手順 3 に進みます。

1. DC1 で、サーバー マネージャーで、をクリックして**管理**、] をクリックし、**追加の役割と機能**します。 追加の役割と機能のウィザードが開きます。
2. **開始する前に**、] をクリックして**次**します。
3. **[インストールの種類**、いることを確認**役割ベースまたは機能ベースのインストール**をクリックして選択して**次**します。
4. **対象サーバーの選択**、いることを確認**サーバー プールからサーバーを選択**が選択されています。 **サーバー プール**、ローカル コンピューターが選択されていることを確認します。 をクリックして**次**します。
5. **サーバーの役割の選択**、] をクリックして**次**します。
6. **機能の選択**で、**機能**、] をクリックして**データ センター ブリッジング**します。 DCB が必要な機能を追加するよう依頼するためのダイアログ ボックスが開きます。 をクリックして**機能を追加する**します。
7. **機能の選択**、] をクリックして**次**します。 
8. 7. で**インストール オプションの確認**、] をクリックして**インストール**します。 **インストールの進行状況**ページには、インストール プロセス中にステータスが表示されます。 インストールが成功した内容を示すメッセージが表示された後で、[**閉じる**します。

### <a name="configure-the-kernel-debugger-to-allow-qos-optional"></a>QoS \(Optional\) を許可するようにカーネル デバッガーを構成します。

 既定では、カーネル デバッガーは NetQos をブロックします。 コンピューターにインストールされているカーネル デバッガーがある場合に、DCB をインストールに使用される方法に関係なく、QoS を有効化し、次のコマンドを実行して構成を許可するようにデバッガーを構成する必要があります。

````
Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 -Force
````

## <a name="install-dcb-in-windows-10"></a>Windows 10 での DCB をインストールします。

Windows 10 コンピューターで、次の手順を行うことができます。

この手順を実行するには、メンバーである**管理者**します。

### <a name="install-dcb"></a>DCB をインストールします。

1. をクリックして**開始**下方向にスクロールし] をクリックして**Windows システム**します。
2. をクリックして**コントロール パネル**します。 **コントロール パネルの [** ] ダイアログ ボックスが開きます。
3. **コントロール パネルの [**、] をクリックして**して表示**、いずれかをクリックして**大きいアイコン**または**小さいアイコン**します。
4. をクリックして**プログラムと機能**します。 プログラムと機能] ダイアログ ボックスが開きます。
5. **プログラムと機能**、左側のウィンドウで [ **Windows の機能のオンまたはオフに**します。 **Windows 機能**] ダイアログ ボックスが開きます。
6. **Windows 機能**、] をクリックして**データ センター ブリッジング**、] をクリックし、 **OK**します。

![Windows の機能をオンまたはオフ] ダイアログ ボックス](../../media/Dcb-Scripting/Dcb-Scripting.jpg)


