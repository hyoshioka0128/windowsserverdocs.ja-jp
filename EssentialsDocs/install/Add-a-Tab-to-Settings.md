---
title: '[設定] へのタブの追加'
description: Windows Server Essentials を使用する方法について説明します
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854983"
---
# <a name="add-a-tab-to-settings"></a>[設定] へのタブの追加

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

オペレーティング システムの設定マネージャーによって使用されるコード アセンブリを作成しインストールすることで、ダッシュボードの [設定] にタブを追加できます。  
  
## <a name="add-a-tab-to-settings"></a>[設定] へのタブの追加  
 次のタスクを実行することで、[設定] にタブを追加します。  
  
-   [ISettingsData インターフェイスの実装のアセンブリへの追加](Add-a-Tab-to-Settings.md#BKMK_ISettingsData)。  
  
-   [Sign the assembly with an Authenticode signature](Add-a-Tab-to-Settings.md#BKMK_SignAssembly) の順にクリックします。  
  
-   [Install the assembly on the reference computer](Add-a-Tab-to-Settings.md#BKMK_InstallAssembly) の順にクリックします。  
  
###  <a name="BKMK_ISettingsData"></a> ISettingsData インターフェイスの実装のアセンブリへの追加します。  
 ISettingsData インターフェイスは、\Program Files\Windows Server\Bin にある AdminCommon.dll アセンブリの Microsoft.WindowsServerSolutions.Settings 名前空間に含まれています。  
  
##### <a name="to-add-the-isettingsdata-code-to-the-assembly"></a>ISettingsData コードをアセンブリに追加するには  
  
1.  **[スタート]** メニューのプログラムを右クリックし、**[管理者として実行]** を選択して、Visual Studio 2010 を管理者として開きます。  
  
2.  をクリックして**ファイル**、 をクリックして**新規**、クリックして**プロジェクト**です。  
  
3.  **[新しいプロジェクト]** ダイアログ ボックスで、**[Visual C#]**、次に **[クラス ライブラリ]** をクリックし、ソリューションの名前に「**DashboardSettingsPage**」と入力して **[OK]** をクリックします。  
  
    > [!IMPORTANT]
    >  サーバーにインストールされるアセンブリの名前は、DashboardSettingsPage.dll である必要があります。この DLL を %ProgramFiles%\Windows Server\Bin\OEM にコピーします。  
  
4.  タブで使用するコントロールを作成します。この例では、設定コントロールの名前は MySettingsControl です。  
  
5.  Class1.cs ファイルの名前を変更します。 たとえば、MySettingTab.cs にします。  
  
6.  AdminCommon.dll ファイルへの参照を追加します。  
  
7.  次の using ステートメントを追加します。  
  
    ```c#  
    using Microsoft.WindowsServerSolutions.Settings;  
    ```  
  
8.  次の例に合わせて、名前空間とクラス ヘッダーを変更します。  
  
    ```  
  
    namespace DashboardSettingsPage  
    {  
        public class MySettingTab : ISettingsData  
        {  
        }  
    }  
  
    ```  
  
9. タブ用に作成したコントロールのインスタンスを作成します。次に、例を示します。  
  
    ```c#  
    private MySettingsControl tab;  
    ```  
  
10. クラスのコンストラクターを追加します。 次のコード例は、コンストラクターを示しています。  
  
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
    >  タブの順序を定義するには、0 から始まる数値を使用します。 Microsoft 組み込みの設定タブが最初に表示され、定義したタブの順序に基づいてユーザー タブが表示されます。 たとえば 3 つの設定タブがある場合、表示する順序に基づいてタブの順序を 0、1、2 と指定します。  
  
15. タブのタイトルを提供する、TabTitle メソッドを追加します。次のコード例は、TabTitle メソッドを示しています。  
  
    ```  
  
    string ISettingsData.TabTitle  
    {  
      get { return "My Settings Tab"; }  
    }  
    ```  
  
    > [!NOTE]
    >  タイトルのテキストも、ローカライズのニーズに合わせてリソース ファイルから指定できます。  
  
16. 保存し、ソリューションをビルドします。  
  
###  <a name="BKMK_SignAssembly"></a> アセンブリに Authenticode 署名で署名します。  
 オペレーティング システムで使用するために、アセンブリを Authenticode で署名する必要があります。 アセンブリの署名の詳細については、「 [Authenticode によるコードの署名と確認 (英語の場合があります)](https://msdn.microsoft.com/library/ms537364\(VS.85\).aspx#SignCode)」を参照してください。  
  
###  <a name="BKMK_InstallAssembly"></a> 参照コンピューターで、アセンブリをインストールします。  
 ソリューションを正常にビルドした後、DashboardSettingsPage.dll ファイルのコピーを参照コンピューターの次のフォルダーに配置します。  
  
 **%Programfiles%\Windows Server\Bin\OEM**  
  
## <a name="see-also"></a>関連項目  
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)