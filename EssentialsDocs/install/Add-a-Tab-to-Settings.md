---
title: "タブの設定に追加します。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aac6b7f3-9020-46c3-a83f-b81542300385
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 9eaa1aa5a9c5e8d4c2e36f2000e0adecc83245d9
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="add-a-tab-to-settings"></a>タブの設定に追加します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

ダッシュ ボードの設定にタブを追加するには作成してオペレーティング システムの設定マネージャーによって使用されるコード アセンブリをインストールします。  
  
## <a name="add-a-tab-to-settings"></a>タブの設定に追加します。  
 設定にタブを追加するには、次のタスクを実行します。  
  
-   [ISettingsData インターフェイスの実装のアセンブリへの追加](Add-a-Tab-to-Settings.md#BKMK_ISettingsData)します。  
  
-   [Authenticode 署名によるアセンブリの署名](Add-a-Tab-to-Settings.md#BKMK_SignAssembly)します。  
  
-   [参照コンピューターで、アセンブリをインストール](Add-a-Tab-to-Settings.md#BKMK_InstallAssembly)します。  
  
###  <a name="BKMK_ISettingsData"></a>ISettingsData インターフェイスの実装のアセンブリへの追加します。  
 ISettingsData インターフェイスは \Program Files\Windows server \bin にある AdminCommon.dll アセンブリの Microsoft.WindowsServerSolutions.Settings 名前空間に含まれています。  
  
##### <a name="to-add-the-isettingsdata-code-to-the-assembly"></a>ISettingsData コードをアセンブリに追加するには  
  
1.  Visual Studio 2010 でプログラムを右クリックして、管理者として開きます、**開始**メニューを選択して**管理者として実行**します。  
  
2.  をクリックして**ファイル**、] をクリックして**新規**、] をクリックし、**プロジェクト**します。  
  
3.  **新しいプロジェクト**ダイアログ ボックスで、] をクリックして**Visual c#**、] をクリックして**クラス ライブラリ**、入力**DashboardSettingsPage**クリックして、ソリューションの名前の**[OK]**します。  
  
    > [!IMPORTANT]
    >  サーバーにインストールされているアセンブリは、DashboardSettingsPage.dll という名前である必要があり、dll を %ProgramFiles%\Windows server \bin\OEM にコピーします。  
  
4.  タブで使用するコントロールを作成します。この例では、設定コントロールの名前は mysettingscontrol です。  
  
5.  Class1.cs ファイルの名前を変更します。 たとえば、MySettingTab.cs です。  
  
6.  AdminCommon.dll ファイルへの参照を追加します。  
  
7.  次の追加ステートメントを使用します。  
  
    ```c#  
    using Microsoft.WindowsServerSolutions.Settings;  
    ```  
  
8.  名前空間とクラス ヘッダーを次の例に示すように変更します。  
  
    ```  
  
    namespace DashboardSettingsPage  
    {  
        public class MySettingTab : ISettingsData  
        {  
        }  
    }  
  
    ```  
  
9. タブ用に作成したコントロールのインスタンスを作成します。例えば：  
  
    ```c#  
    private MySettingsControl tab;  
    ```  
  
10. クラスのコンス トラクターを追加します。 次のコード例は、コンス トラクターを示しています。  
  
    ```  
  
    public MySettingTab()  
    {  
       tab = new MySettingsControl();  
    }  
    ```  
  
11. 設定の変更を送信する、Commit メソッドを追加します。 次のコード例は、Commit メソッドを示しています。  
  
    ```  
  
    void ISettingsData.Commit(bool dismissed)  
    {  
       // Implement the code that is required to submit your setting changes  
    }  
    ```  
  
12. タブのコントロールを識別する、TabControl メソッドを追加します。次のコード例は、TabControl メソッドを示しています。  
  
    ```  
  
    System.Windows.Forms.Control ISettingsData.TabControl  
    {  
       get { return tab; }  
    }  
    ```  
  
13. タブの一意の識別子を提供する、TabId メソッドを追加します。次のコード例は、TabId メソッドを示しています。  
  
    ```  
  
    private Guid id = Guid.NewGuid();  
  
    Guid ISettingsData.TabId  
    {  
       get { return id; }  
    }  
    ```  
  
14. タブの順序を返す、TabOrder メソッドを追加します。次のコード例は、TabOrder メソッドを示しています。  
  
    ```  
  
    int ISettingsData.TabOrder  
    {  
       get { return 0; }  
    }  
    ```  
  
    > [!NOTE]
    >  タブの順序を定義するには、0 から始まる数値を使用します。 Microsoft 組み込みの設定タブが最初に表示し、タブが表示されます、定義したタブ オーダーに基づきます。 たとえば、3 つの設定タブがある場合は場合、は、0、1、および 2 が表示されるタブ順序に基づいてとしてタブの順序を指定します。  
  
15. タブのタイトルを提供する、TabTitle メソッドを追加します。次のコード例は、TabTitle メソッドを示しています。  
  
    ```  
  
    string ISettingsData.TabTitle  
    {  
      get { return "My Settings Tab"; }  
    }  
    ```  
  
    > [!NOTE]
    >  タイトルのテキストは、ローカライズのニーズに合わせてリソース ファイルからも取得できます。  
  
16. 保存し、ソリューションをビルドします。  
  
###  <a name="BKMK_SignAssembly"></a>Authenticode 署名によるアセンブリを署名します。  
 オペレーティング システムで使用されるようにアセンブリの Authenticode 署名する必要があります。 アセンブリの署名の詳細については、次を参照してください。[Authenticode によるコードのチェックの署名と](https://msdn.microsoft.com/library/ms537364\(VS.85\).aspx#SignCode)します。  
  
###  <a name="BKMK_InstallAssembly"></a>参照コンピューターで、アセンブリをインストールします。  
 ソリューションを正常に作成した後は、参照コンピューターで、次のフォルダーで、DashboardSettingsPage.dll ファイルのコピーを配置します。  
  
 **%Programfiles%\Windows server \bin\OEM**  
  
## <a name="see-also"></a>参照してください。  
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)