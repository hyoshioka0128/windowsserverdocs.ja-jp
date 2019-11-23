---
title: AD FS 2019 のリスク評価モデルを使用してプラグインをビルドする
description: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.reviewer: ''
ms.date: 04/16/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 1a4569b1fa3791d1d3b412b0801f216c975aa4dc
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70867606"
---
# <a name="build-plug-ins-with-ad-fs-2019-risk-assessment-model"></a>AD FS 2019 のリスク評価モデルを使用してプラグインをビルドする

独自のプラグインを構築して、さまざまな段階 (要求の受信、事前認証、事後認証) で、認証要求に対するリスクスコアをブロックまたは割り当てることができるようになりました。 これは、AD FS 2019 で導入された新しいリスク評価モデルを使用して実現できます。 

## <a name="what-is-the-risk-assessment-model"></a>リスク評価モデルとは何ですか。

リスク評価モデルは、開発者が認証要求ヘッダーを読み取り、独自のリスク評価ロジックを実装できるようにするためのインターフェイスとクラスのセットです。 実装されたコード (プラグイン) は、AD FS 認証プロセスを使用してラインで実行されます。 たとえば、モデルに含まれているインターフェイスとクラスを使用して、要求ヘッダーに含まれるクライアント IP アドレスに基づいて認証要求をブロックまたは許可するコードを実装できます。 AD FS は、各認証要求のコードを実行し、実装されているロジックに従って適切なアクションを実行します。 

このモデルでは、次に示すように、AD FS 認証パイプラインの3つの段階のいずれかでプラグインコードを使用できます。

![model](media/ad-fs-risk-assessment-model/risk1.png)

1.  **要求の受信ステージ**-ユーザーが資格情報を入力する前に、AD FS が認証要求を受信するときに、要求を許可またはブロックするプラグインを作成できるようにします。 この段階で利用可能な要求コンテキスト (クライアント IP、Http メソッド、プロキシサーバー DNS など) を使用して、リスク評価を実行できます。 たとえば、要求コンテキストから IP を読み取るためのプラグインを作成し、その IP が危険な ip の事前定義リストにある場合は認証要求をブロックすることができます。 

2.  **事前認証段階**–プラグインを使用して、ユーザーが資格情報を入力した時点で要求を許可またはブロックすることができますが、AD FS によって評価されます。 この段階では、要求コンテキストに加えて、リスク評価ロジックで使用するセキュリティコンテキスト (ユーザートークン、ユーザー id など) とプロトコルコンテキスト (認証プロトコル、clientid、resourceid など) に関する情報も用意されています。 たとえば、ユーザートークンからユーザーのパスワードを読み取り、パスワードが危険なパスワードの事前定義リストにある場合は認証要求をブロックすることで、パスワードスプレー攻撃を防ぐためのプラグインを構築できます。 

3.  **認証後**-ユーザーが資格情報を入力し、AD FS によって認証が実行された後に、プラグインを構築してリスクを評価できるようにします。 この段階では、要求コンテキスト、セキュリティコンテキスト、およびプロトコルコンテキストに加え、認証結果 (成功または失敗) に関する情報も表示されます。 このプラグインでは、利用可能な情報に基づいてリスクスコアを評価し、さらに評価するためにリスクスコアを要求およびポリシーの規則に渡すことができます。 

リスク評価プラグインを構築して AD FS プロセスで実行する方法について理解を深めるために、危険と特定された特定の**エクストラネット**ip からの要求をブロックするサンプルプラグインを作成し、AD FS にプラグインを登録し、最後に機能をテストします。 

>[!NOTE]
>このチュートリアルでは、サンプルプラグインを作成する方法についてのみ説明します。 このソリューションは、エンタープライズ対応のソリューションを作成することを意味します。  

## <a name="building-a-sample-plug-in"></a>サンプルプラグインのビルド

### <a name="pre-requisites"></a>前提条件
このサンプルプラグインをビルドするために必要な前提条件の一覧を次に示します。

- AD FS 2019 がインストールおよび構成されている
- 4\.7 以降の .NET Framework
- Visual Studio

### <a name="build-plug-in-dll"></a>ビルドプラグイン dll
次の手順では、サンプルプラグイン dll を構築する方法について説明します。

1. サンプルプラグインをダウンロードし、Git Bash を使用して次のように入力します。 

   ```
   git clone https://github.com/Microsoft/adfs-sample-RiskAssessmentModel-RiskyIPBlock
   ```

2. AD FS サーバー上の任意の場所に .csv ファイルを作成し**ます**(ここでは、 **authconfigdb**ファイルを**c:\ 拡張機能**に作成し、このファイルにブロックする ip を追加します)。 

   このサンプルプラグインは、このファイルに記載されている**エクストラネット ip**からの認証要求をすべてブロックします。 

   >{!注: AD FS ファームがある場合は、任意またはすべての AD FS サーバー上にファイルを作成できます。 すべてのファイルを使用して、危険な Ip を AD FS にインポートできます。 インポートプロセスの詳細については、後述の「[プラグイン dll を AD FS に登録](#register-the-plug-in-dll-with-ad-fs)する」を参照してください。 

3. Visual Studio を使用して `ThreatDetectionModule.sln` プロジェクトを開く

4. 次に示すように、ソリューションエクスプローラーから `Microsoft.IdentityServer.dll` を削除します。</br>
   ![model](media/ad-fs-risk-assessment-model/risk2.png)

5. 次に示すように、AD FS の `Microsoft.IdentityServer.dll` への参照を追加します。

   a.   **ソリューションエクスプローラー**で **[参照]** を右クリックし、 **[参照の追加]** を選択します。</br> 
   ![モデル](media/ad-fs-risk-assessment-model/risk3.png)
   
   b.   **[参照マネージャー]** ウィンドウで、 **[参照]** を選択します。 [**参照するファイルの選択...]** ダイアログボックスで、AD FS インストールフォルダー (ここでは**C:\Windows\ADFS**) から [`Microsoft.IdentityServer.dll`] を選択し、 **[追加]** をクリックします。
   
   >[!NOTE]
   >ここでは、AD FS サーバー自体にプラグインを構築しています。 開発環境が別のサーバー上にある場合は、の AD FS サーバーの AD FS インストールフォルダーから開発用のボックスに `Microsoft.IdentityServer.dll` をコピーします。</br> 
   
   ![model](media/ad-fs-risk-assessment-model/risk4.png)
   
   c.   `Microsoft.IdentityServer.dll` チェックボックスがオンになっていることを確認した後、 **[参照マネージャー]** ウィンドウで [ **OK]** をクリックします。</br>
   ![model](media/ad-fs-risk-assessment-model/risk5.png)
 
6. すべてのクラスと参照が、ビルドを実行するために配置されました。   ただし、このプロジェクトの出力は dll であるため、AD FS サーバーの**グローバルアセンブリキャッシュ**(GAC) にインストールする必要があり、dll を先に署名する必要があります。 これは、次のように実行できます。

   a.   プロジェクトの名前 ThreatDetectionModule を**右クリック**します。 メニューの **[プロパティ]** をクリックします。</br>
   ![model](media/ad-fs-risk-assessment-model/risk6.png)
   
   b.   **[プロパティ]** ページで、左側の **[署名]** をクリックし、 **[アセンブリの署名]** チェックボックスをオンにします。 [**厳密な名前のキーファイルを選択**してください] プルダウンメニューから、[ **< 新規作成] を選択します。>**</br>
   ![model](media/ad-fs-risk-assessment-model/risk7.png)

   c.   [**厳密な名前キーの作成] ダイアログ**ボックスで、キーの名前 (任意の名前を選択できます) を入力し、 **[キーファイルをパスワードで保護**する] チェックボックスをオフにします。 クリックして **OK**します。
   ![model](media/ad-fs-risk-assessment-model/risk8.png)</br>
 
   d.   次のようにプロジェクトを保存します。</br>
   ![model](media/ad-fs-risk-assessment-model/risk9.png)

7. 次に示すように、 **[ビルド]** 、 **[ソリューションのリビルド]** の順にクリックして、プロジェクトをビルドします。</br>
   ![model](media/ad-fs-risk-assessment-model/risk10.png)
 
   画面の下部にある [**出力] ウィンドウ**で、エラーが発生していないかどうかを確認します。</br>
   ![model](media/ad-fs-risk-assessment-model/risk11.png)


プラグイン (dll) が使用できるようになりました。プロジェクトフォルダーの **\bin\debug**フォルダー (ここでは**C:\extensions\ThreatDetectionModule\bin\Debug\ThreatDetectionModule.dll**) にあります。 

次の手順では、この dll を AD FS に登録して、AD FS 認証プロセスで実行します。 

### <a name="register-the-plug-in-dll-with-ad-fs"></a>AD FS にプラグイン dll を登録する

AD FS サーバーで `Register-AdfsThreatDetectionModule` PowerShell コマンドを使用して AD FS に dll を登録する必要があります。ただし、登録する前に、公開キートークンを取得する必要があります。 この公開キートークンは、キーを作成し、そのキーを使用して dll に署名したときに作成されたものです。 Dll の公開キートークンの詳細については、Sn.exe を次のように使用できます **。**

1. **\Bin\debug**フォルダーから別の場所に dll ファイルをコピーします (ここでは、 **c:\ 拡張子**にコピーします)。

2. Visual Studio の**開発者コマンドプロンプト**を開始し、sn.exe を含むディレクトリにアクセスし**ます**(ここでは、ディレクトリは**C:\Program files (X86) \Microsoft SDKs\Windows\v10.0A\bin\NETFX 4.7.2 Tools**) ![モデル](media/ad-fs-risk-assessment-model/risk12.png)

3. **-T**パラメーターと、ファイルの場所 (ここでは `SN -T “C:\extensions\ThreatDetectionModule.dll”`) ![モデルを指定して、 **SN**コマンドを実行し](media/ad-fs-risk-assessment-model/risk13.png)</br>
   このコマンドにより、公開キートークンが提供されます (**公開キートークンは 714697626ef96b35**)

4. AD FS サーバーの**グローバルアセンブリキャッシュ**に dll を追加するベストプラクティスとして、プロジェクトに適したインストーラーを作成し、インストーラーを使用してファイルを GAC に追加することをお勧めします。 もう1つの解決策として、 **gacutil.exe** ([こちら](https://docs.microsoft.com/dotnet/framework/tools/gacutil-exe-gac-tool)で入手できる**gacutil.exe**の詳細) を開発用コンピューターで使用することができます。  AD FS と同じサーバーに visual studio をインストールしているため、次のように Gacutil.exe を使用し**ます。**

   a.   Visual Studio の開発者コマンドプロンプトで、Gacutil.exe を含むディレクトリ (ここでは、ディレクトリは**C:\Program files (x86) \Microsoft SDKs\Windows\v10.0A\bin\NETFX 4.7.2 Tools**) にアクセスし**ます。**

   b.   **Gacutil**コマンド (my の場合 `Gacutil /IF C:\extensions\ThreatDetectionModule.dll`) ![モデルを実行し](media/ad-fs-risk-assessment-model/risk14.png)
 
   >[!NOTE]
   >AD FS ファームがある場合は、ファーム内の各 AD FS サーバーで上記の手順を実行する必要があります。 

5. **Windows PowerShell**を開き、次のコマンドを実行して dll を登録します。
   ```
   Register-AdfsThreatDetectionModule -Name "<Add a name>" -TypeName "<class name that implements interface>, <dll name>, Version=10.0.0.0, Culture=neutral, PublicKeyToken=< Add the Public Key Token from Step 2. above>" -ConfigurationFilePath "<path of the .csv file>”
   ```
   この場合、コマンドは次のようになります。 
   ```
   Register-AdfsThreatDetectionModule -Name "IPBlockPlugin" -TypeName "ThreatDetectionModule.UserRiskAnalyzer, ThreatDetectionModule, Version=10.0.0.0, Culture=neutral, PublicKeyToken=714697626ef96b35" -ConfigurationFilePath "C:\extensions\authconfigdb.csv”
   ```
 
   >[!NOTE]
   >AD FS ファームがある場合でも、dll を登録する必要があるのは1回だけです。 

6. Dll の登録後に AD FS サービスを再起動する

これで、dll が AD FS に登録され、使用できるようになりました。

 >[!NOTE]
 > プラグインに変更が加えられ、プロジェクトが再構築された場合は、更新された dll を再度登録する必要があります。 登録する前に、次のコマンドを使用して現在の dll の登録を解除する必要があります。</br></br>
 >`
  UnRegister-AdfsThreatDetectionModule -Name "<name used while registering the dll in 5. above>"
 >`</br></br> この場合、コマンドは次のようになります。
 >``` 
 >UnRegister-AdfsThreatDetectionModule -Name "IPBlockPlugin"
 >```

### <a name="testing-the-plug-in"></a>プラグインのテスト

1. 前の手順で作成**した authconfig .csv**ファイル (ここでは、" **c:\ 拡張子**") を開き、ブロックする**エクストラネット ip**を追加します。 すべての IP は個別の行に配置する必要があり、末尾にスペースを入れないでください。</br>
   ![model](media/ad-fs-risk-assessment-model/risk18.png)
 
2. ファイルを保存して閉じます。

3. 次の PowerShell コマンドを実行して、更新されたファイルを AD FS にインポートします。 

   ```
   Import-AdfsThreatDetectionModuleConfiguration -name "<name given while registering the dll>" -ConfigurationFilePath "<path of the .csv file>"
   ```
 
   この場合、コマンドは次のようになります。 
   ```
   Import-AdfsThreatDetectionModuleConfiguration -name "IPBlockPlugin" -ConfigurationFilePath "C:\extensions\authconfigdb.csv")
   ```
 
4. **Authconfig .csv**で追加したものと同じ IP アドレスを使用して、サーバーから認証要求を開始します。

   このデモでは、要求を開始するために AD FS を使用して、 [X レイ](https://adfshelp.microsoft.com/ClaimsXray/TokenRequest)の要求を使用します。 X レイツールを使用する場合は、次の手順に従ってください。 

   フェデレーションサーバーインスタンスを入力し、 **[認証のテスト]** ボタンをクリックします。</br> 
   ![モデル](media/ad-fs-risk-assessment-model/risk15.png) 

5. 次に示すように、認証はブロックされます。</br>
   ![model](media/ad-fs-risk-assessment-model/risk16.png)
 
これで、プラグインをビルドして登録する方法がわかりました。次は、モデルで導入された新しいインターフェイスとクラスを使用して実装を理解するためのプラグインコードについて説明します。 

## <a name="plug-in-code-walkthrough"></a>プラグインコードのチュートリアル

Visual Studio を使用してプロジェクト `ThreatDetectionModule.sln` を開き、画面の右側にある**ソリューションエクスプローラー**からメインファイル**UserRiskAnalyzer.cs**を開きます。</br>
![model](media/ad-fs-risk-assessment-model/risk17.png)
 
このファイルには、抽象クラス[ThreatDetectionModule](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule?view=adfs-2019)とインターフェイス[IRequestReceivedThreatDetectionModule](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.irequestreceivedthreatdetectionmodule?view=adfs-2019)を実装する main クラス UserRiskAnalyzer が含まれています。このクラスは、要求コンテキストから ip を読み取り、取得した ip と AD FS DB から読み込まれた ip を比較し、IP 一致がある場合は要求をブロックします。 これらの型についてさらに詳しく説明します。

### <a name="threatdetectionmodule-abstract-class"></a>ThreatDetectionModule 抽象クラス

この抽象クラスは、プラグインを AD FS パイプラインに読み込み、AD FS プロセスを使用してプラグインコードをインラインで実行できるようにします。 

```
public abstract class ThreatDetectionModule 
{ 
    protected ThreatDetectionModule(); 
 
    public abstract string VendorName { get; } 
    public abstract string ModuleIdentifier { get; } 
 
 public abstract void OnAuthenticationPipelineLoad(ThreatDetectionLogger logger, ThreatDetectionModuleConfiguration configData); 
 public abstract void OnAuthenticationPipelineUnload(ThreatDetectionLogger logger); 
  public abstract void OnConfigurationUpdate(ThreatDetectionLogger logger, ThreatDetectionModuleConfiguration configData); 
 }   
```
クラスには、次のメソッドとプロパティが含まれています。

|メソッド |種類|定義|
|-----|-----|-----| 
|[OnAuthenticationPipelineLoad](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onauthenticationpipelineload?view=adfs-2019) |無効化|プラグインがパイプラインに読み込まれるときに AD FS によって呼び出されます| 
|[OnAuthenticationPipelineUnload](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onauthenticationpipelineunload?view=adfs-2019) |無効化|プラグインがそのパイプラインからアンロードされるときに AD FS によって呼び出されます| 
|[OnConfigurationUpdate](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onconfigurationupdate?view=adfs-2019)| 無効化|構成の更新時に AD FS によって呼び出されます |
|**プロパティ** |**Type** |**定義**|
|[VendorName](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.vendorname?view=adfs-2019)|String |プラグインを所有しているベンダーの名前を取得します。|
|[ModuleIdentifier](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.moduleidentifier?view=adfs-2019)|String |プラグインの識別子を取得します。|

このサンプルプラグインでは、 [Onauthenticationpipelineload](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onauthenticationpipelineload?view=adfs-2019)メソッドと[onconfigurationupdate](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onconfigurationupdate?view=adfs-2019)メソッドを使用して、AD FS DB から事前に定義された ip を読み取ります。 [Onauthenticationpipelineload](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onauthenticationpipelineload?view=adfs-2019)は、プラグインが AD FS に登録されているときに呼び出されます。また、`Import-AdfsThreatDetectionModuleConfiguration` コマンドレットを使用して .csv がインポートされるときに[onconfigurationupdate](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onconfigurationupdate?view=adfs-2019)が呼び出されます。 

#### <a name="irequestreceivedthreatdetectionmodule-interface"></a>IRequestReceivedThreatDetectionModule インターフェイス

この[インターフェイス](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.irequestreceivedthreatdetectionmodule?view=adfs-2019)を使用すると、AD FS が認証要求を受信する前に、ユーザーが認証プロセスの受信要求ステージで資格情報を入力する前に、リスク評価を実装できます。 
 
```
public interface IRequestReceivedThreatDetectionModule
{
Task<ThrottleStatus> EvaluateRequest (
ThreatDetectionLogger logger, 
RequestContext requestContext );
}
```

インターフェイスには、 [EvaluateRequest](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.irequestreceivedthreatdetectionmodule.evaluaterequest?view=adfs-2019)メソッドが含まれています。これにより、requestContext 入力パラメーターで渡される認証要求のコンテキストを使用して、リスク評価ロジックを記述できます。 RequestContext パラメーターの型は[requestcontext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019)です。 

渡されたもう1つの入力パラメーターは、 [ThreatDetectionLogger](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionlogger?view=adfs-2019)型の logger です。 パラメーターを使用すると、エラー、監査、およびデバッグメッセージを AD FS ログに書き込むことができます。 

このメソッドは、[ThrottleStatus](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.throttlestatus?view=adfs-2019) を返します。これは、 (注として、1からブロック、および 2) AD FS が返されます。その後、要求をブロックするか許可します。

このサンプルプラグインでは、 [EvaluateRequest](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.irequestreceivedthreatdetectionmodule.evaluaterequest?view=adfs-2019)メソッドの実装は、 [RequestContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019)パラメーターから[clientIpAddress](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext.clientipaddresses?view=adfs-2019#Microsoft_IdentityServer_Public_ThreatDetectionFramework_RequestContext_ClientIpAddresses)を解析し、AD FS DB から読み込まれたすべての ip と比較します。 一致が見つかった場合、メソッドは**Block**に2を返します。それ以外の場合は、 **Allow**に1を返します。 返された値に基づいて、AD FS がブロックされるか、または要求が許可されます。 

>[!NOTE]
>上記で説明したサンプルプラグインは、IRequestReceivedThreatDetectionModule インターフェイスのみを実装します。 ただし、リスク評価モデルには、IPreAuthenticationThreatDetectionModule (事前認証段階) と IPostAuthenticationThreatDetectionModule という2つの追加のインターフェイスが用意されています (リスク評価を実装する場合)。認証後の段階での評価ロジック。 2つのインターフェイスの詳細については、以下を参照してください。 

#### <a name="ipreauthenticationthreatdetectionmodule-interface"></a>IPreAuthenticationThreatDetectionModule インターフェイス 

この[インターフェイス](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.ipreauthenticationthreatdetectionmodule?view=adfs-2019)を使用すると、ユーザーが資格情報を入力した時点でリスク評価ロジックを実装することができます。ただし、AD FS は事前認証段階です。 

```
public interface IPreAuthenticationThreatDetectionModule
{
Task<ThrottleStatus> EvaluatePreAuthentication (
ThreatDetectionLogger logger, 
RequestContext requestContext, 
SecurityContext securityContext, 
ProtocolContext protocolContext, 
IList<Claim> additionalClams
);
}
```
インターフェイスには、 [Evaluatepreauthentication](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.ipreauthenticationthreatdetectionmodule.evaluatepreauthentication?view=adfs-2019)メソッドが含まれています。これにより、 [requestcontext Requestcontext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019)、 [SecurityContext SecurityContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.securitycontext?view=adfs-2019)、 [protocolcontext Protocolcontext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.protocolcontext?view=adfs-2019)、および[IList<Claim> additionalclams](https://docs.microsoft.com/dotnet/api/system.collections.generic.ilist-1?view=netframework-4.7.2)入力パラメーターで渡された情報を使用して、事前認証のリスク評価ロジックを作成できます。 

>[!NOTE]
>各コンテキストの種類で渡されるプロパティの一覧については、「 [RequestContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019)、 [SecurityContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.securitycontext?view=adfs-2019)、および[protocolcontext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.protocolcontext?view=adfs-2019)クラスの定義」を参照してください。 

渡されたもう1つの入力パラメーターは、 [ThreatDetectionLogger](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionlogger?view=adfs-2019)型の logger です。 パラメーターを使用すると、エラー、監査、およびデバッグメッセージを AD FS ログに書き込むことができます。

このメソッドは、[ThrottleStatus](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.throttlestatus?view=adfs-2019) を返します。これは、 (注として、1からブロック、および 2) AD FS が返されます。その後、要求をブロックするか許可します。 

#### <a name="ipostauthenticationthreatdetectionmodule-interface"></a>IPostAuthenticationThreatDetectionModule インターフェイス

この[インターフェイス](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.ipostauthenticationthreatdetectionmodule?view=adfs-2019)を使用すると、ユーザーが資格情報を提供し、AD FS が認証後の段階で認証を実行した後に、リスク評価ロジックを実装できます。 

```
public interface IPostAuthenticationThreatDetectionModule
{
Task<RiskScore> EvaluatePostAuthentication (
ThreatDetectionLogger logger, 
RequestContext requestContext, 
SecurityContext securityContext, 
ProtocolContext protocolContext, 
AuthenticationResult authenticationResult, 
IList<Claim> additionalClams
);
}
```

このインターフェイスには、評価後のリスク評価ロジックを記述するために、 [requestContext requestcontext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019)、 [SecurityContext SecurityContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.securitycontext?view=adfs-2019)、 [protocolcontext protocolcontext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.protocolcontext?view=adfs-2019)、および[IList<Claim> additionalclams](https://docs.microsoft.com/dotnet/api/system.collections.generic.ilist-1?view=netframework-4.7.2)入力パラメーターで渡される情報を使用できる[evaluatepostauthentication](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.ipostauthenticationthreatdetectionmodule.evaluatepostauthentication?view=adfs-2019)メソッドが含まれています。 

>[!NOTE]
> 各コンテキスト型で渡されるプロパティの完全な一覧については、「 [RequestContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019)、 [SecurityContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.securitycontext?view=adfs-2019)、および[protocolcontext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.protocolcontext?view=adfs-2019)クラスの定義」を参照してください。 

渡されたもう1つの入力パラメーターは、 [ThreatDetectionLogger](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionlogger?view=adfs-2019)型の logger です。 パラメーターを使用すると、エラー、監査、およびデバッグメッセージを AD FS ログに書き込むことができます。 

メソッドは、AD FS ポリシーと要求規則で使用できる[リスクスコア](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.authentication.riskscoreconstants?view=adfs-2019)を返します。 

>[!NOTE]
>プラグインを機能させるには、メインクラス (この場合は UserRiskAnalyzer) が[ThreatDetectionModule](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule?view=adfs-2019)抽象クラスを派生する必要があり、上記の3つのインターフェイスのうち少なくとも1つを実装する必要があります。 Dll が登録されると、AD FS 実装されているインターフェイスを確認し、パイプラインの適切なステージでそれらを呼び出します。

### <a name="faqs"></a>よく寄せられる質問

**これらのプラグインを作成する必要があるのはなぜですか。**</br>
**A:** これらのプラグインは、パスワードスプレー攻撃などの攻撃から環境を保護するための追加機能を提供するだけでなく、お客様の要件に基づいて独自のリスク評価ロジックを構築するための柔軟性も提供します。 

**ログはどこでキャプチャされますか。**</br>
**A:** WriteAdminLogErrorMessage メソッドを使用して "AD FS/Admin" イベントログにエラーログを書き込むことができます。また、WriteAuditMessage メソッドを使用して "監査ログ" を "AD FS 監査" し、ログを "AD FS トレース" を使用して、WriteDebugMessage メソッドを使用してデバッグログに記録します。 

**これらのプラグインを追加すると、認証プロセスの待機時間 AD FS 増加しますか。**</br>
**A:** 待機時間の影響は、実装するリスク評価ロジックの実行にかかった時間によって決まります。 運用環境にプラグインを展開する前に、待機時間の影響を評価することをお勧めします。 

**危険な Ip やユーザーなどの一覧を AD FS 提案できないのはなぜですか。**</br>
**A:** 現在は利用できませんが、プラグ可能なリスク評価モデルでは、危険な Ip やユーザーなどを提案するインテリジェンスの構築に取り組んでいます。 近日中に発表日を共有します。 
