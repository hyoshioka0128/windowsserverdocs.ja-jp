---
title: AD FS 2019 リスク評価のモデルでは、プラグインのビルドします。
description: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.reviewer: ''
ms.date: 04/16/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 80f42695af917084ee63297df052adc069340bb3
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190524"
---
# <a name="build-plug-ins-with-ad-fs-2019-risk-assessment-model"></a>AD FS 2019 リスク評価のモデルでは、プラグインのビルドします。

さまざまな段階 – 要求が受信した、事前認証、および事後認証中に認証要求にリスク スコアを割り当てたり、ブロックしたり、独自プラグインを構築できます。 これは、AD FS 2019 で導入された新しいリスク評価のモデルを使用して実現できます。 

## <a name="what-is-the-risk-assessment-model"></a>リスク評価のモデルとは何ですか。

リスク評価のモデルは、一連のインターフェイスと開発者が認証要求のヘッダーを読み取って独自のリスク評価ロジックを実装するクラスです。 実装したコード (プラグイン) は、AD FS の認証プロセスに従って実行されます。 次のようなインターフェイスと、モデルに含まれているクラスを使用して、いずれかのブロックにコードを実装したり、要求ヘッダーに含まれるクライアントの IP アドレスに基づいて認証要求を許可できます。 AD FS は各認証要求のコードを実行し、実装されているロジックに従って適切なアクションを実行します。 

次に示すように、AD FS 認証パイプラインの 3 つの段階のいずれかでプラグインのコードを許可するモデル

![model](media\ad-fs-risk-assessment-model\risk1.png)

1.  **ステージの受信要求**– を許可するか、AD FS の認証は要求を受け取るつまりユーザーが資格情報を入力する前に、要求をブロックするプラグインを構築できます。 要求のコンテキスト (たとえば、クライアント IP、Http メソッド、プロキシ サーバーの DNS など) を使用するリスク評価を実行するには、この段階で使用できます。 例では、要求コンテキストから ip アドレスを読み取るし、IP が危険な Ip の定義済み一覧にある場合は、認証要求をブロックするプラグインを構築できます。 

2.  **事前認証段階**– 許可または資格情報を提供するユーザーが AD FS がそれらを評価する前に、ポイントで要求をブロックするプラグインを構築できます。 この段階で、要求コンテキストだけでなくも情報がある (例: ユーザー トークン、ユーザーの識別子など) のセキュリティ コンテキストで、リスクの評価ロジックに使用するプロトコルのコンテキスト (例: 認証プロトコル、clientid、resourceid など)。 次のようなユーザーのトークンからユーザーのパスワードを読み取り、パスワードがリスクの高いパスワードの事前定義済みリストの場合は、認証要求をブロックしているパスワード スプレー攻撃を防ぐためにプラグインを構築できます。 

3.  **事後認証**– ユーザーが資格情報を提供し、AD FS の認証が実行した後は、リスクを評価するプラグインの構築を可能にします。 要求コンテキスト、セキュリティ コンテキスト、およびプロトコルのコンテキストに加えて、この段階でも、認証結果 (成功または失敗) の情報があります。 プラグイン利用可能な情報に基づいてリスク スコアを評価でき、リスク スコアを要求してさらに評価のためのポリシー ルールを渡します。 

プラグインのリスク評価をビルドし、AD FS のプロセスに合わせて実行する方法を理解する特定から着信する要求をブロックするサンプルのプラグインを構築してみましょう**エクストラネット**Ip として識別、リスクの高いレジスタ プラグインと AD FS最後に、機能をテストします。 

>[!NOTE]
>このチュートリアルでは、どのプラグインを作成するサンプルを表示するためだけです。 はありませんが準備完了のエンタープライズ ソリューションを作成するソリューションです。  

## <a name="building-a-sample-plug-in"></a>プラグイン サンプルのビルド

### <a name="pre-requisites"></a>前提条件
このサンプルのプラグインをビルドするために必要な前提条件の一覧を次に示します

- AD FS 2019 のインストールし、構成
- .NET framework 4.7 以降
- Visual Studio

### <a name="build-plug-in-dll"></a>プラグイン dll をビルドします。
次の手順を追ってサンプル プラグイン dll のビルドします。

 1. プラグインのサンプルをダウンロード、Git Bash を使用して、次の入力します。 

   ```
   git clone https://github.com/Microsoft/adfs-sample-RiskAssessmentModel-RiskyIPBlock
   ```

 2. 作成、 **.csv** 、AD FS サーバー上の任意の場所でファイル (今回は、作成、 **authconfigdb.csv**ファイル**C:\extensions**) し、このファイルをブロックする ip アドレスを追加します。 

   プラグインのサンプルから任意の認証要求がブロックされます、**エクストラネット Ip**このファイルに一覧表示します。 

   >{!注] [AD FS ファームがあれば、任意またはすべての AD FS サーバー上のファイルを作成することができます。 AD FS に危険な ip アドレスをインポートするファイルを使用できます。 インポート プロセスで詳しく説明します、 [AD FS を使用したプラグインの dll を登録](#register-the-plug-in-dll-with-ad-fs)以下のセクション。 

 3. プロジェクトを開く`ThreatDetectionModule.sln`Visual Studio を使用

 4. 削除、`Microsoft.IdentityServer.dll`次に示すようにソリューション エクスプ ローラーから。</br>
 ![model](media\ad-fs-risk-assessment-model\risk2.png)

 5. 参照を追加、`Microsoft.IdentityServer.dll`次に示すように、AD FS の

   a.    右クリックして**参照**で**ソリューション エクスプ ローラー**選択**参照の追加.**</br> 
   ![モデル](media\ad-fs-risk-assessment-model\risk3.png)
   
   b.    **参照マネージャー**ウィンドウ選択**参照**します。 **を参照するファイルを選択しています.** ダイアログで、 `Microsoft.IdentityServer.dll` 、AD FS のインストール フォルダー (ここで**C:\Windows\ADFS**) をクリック**追加**。
   
   >[!NOTE]
    >今回は今作成して、プラグイン、AD FS サーバー自体にします。 開発環境が別のサーバー上にある場合は、コピー、`Microsoft.IdentityServer.dll`開発ボックスに、AD FS サーバーで AD FS のインストール フォルダーから。</br> 
   
   ![model](media\ad-fs-risk-assessment-model\risk4.png)
   
   c.   をクリックして**OK**上、**参照マネージャー**ウィンドウを確認した後`Microsoft.IdentityServer.dll`チェック ボックスをオン</br>
   ![model](media\ad-fs-risk-assessment-model\risk5.png)
 
 6. すべてのクラスと参照は、ビルドを実行するようになりましたが。   ただし、このプロジェクトの出力は、dll であるためする必要がありますにインストールする、**グローバル アセンブリ キャッシュ**GAC、AD FS サーバーと、dll は、最初に署名する必要がありますか。 これには、次のように実行できます。

   a.    **右クリックして**ThreatDetectionModule、プロジェクトの名前。 メニューから、次のようにクリックします。**プロパティ**します。</br>
   ![model](media\ad-fs-risk-assessment-model\risk6.png)
   
   b.    **プロパティ**] ページで [**署名**、左側で、チェック ボックスをオンにマークされているチェックインし**アセンブリに署名**します。 **厳密な名前キー ファイルを選択して**: メニューの プルダウン **< 新規.>**</br>
   ![model](media\ad-fs-risk-assessment-model\risk7.png)

   c.   **厳密な名前キーの作成 ダイアログ**、キーの名前 (任意の名前を選択することができます) を入力、チェック ボックスをオフに**パスワードを使用してキー ファイルを保護**します。 クリックして **OK**します。
   ![model](media\ad-fs-risk-assessment-model\risk8.png)</br>
 
   d.   次に示すように、プロジェクトを保存します。</br>
   ![model](media\ad-fs-risk-assessment-model\risk9.png)

 7. クリックして、プロジェクトをビルド**ビルド**し**ソリューションのリビルド**次に示す</br>
 ![model](media\ad-fs-risk-assessment-model\risk10.png)
 
 チェック、**出力ウィンドウ**エラーが発生しているかどうかに表示する画面の下部にあります。</br>
 ![model](media\ad-fs-risk-assessment-model\risk11.png)


プラグイン (dll) の使用の準備が整いましたとでは、 **\bin\Debug**プロジェクト フォルダーのフォルダー (ここでの**C:\extensions\ThreatDetectionModule\bin\Debug\ThreatDetectionModule.dll**)。 

次の手順では、AD FS の認証プロセスに合わせて実行するように AD fs でこの dll を登録します。 

### <a name="register-the-plug-in-dll-with-ad-fs"></a>AD FS を使用したプラグインの dll を登録します。

使用して AD FS で dll を登録する必要があります、`Register-AdfsThreatDetectionModule`ただし、AD FS サーバーで PowerShell コマンドを登録する前に必要があります、公開キー トークンを取得します。 この公開キー トークンは、キーを作成し、そのキーを使用して dll を署名するときに作成されました。 公開キー トークン、dll の新機能については、使用することができます、 **SN.exe**次のように

 1. Dll ファイルのコピー、 **\bin\Debug**別の場所にフォルダー (ここへのコピーで**C:\extensions**)

 2. 開始、**開発者コマンド プロンプト**for Visual Studio および格納されているディレクトリに移動して、 **sn.exe** (ここでは、ディレクトリは**C:\Program Files (x86) \Microsoft SDKs\Windows\v10.0A\bin\NETFX 4.7.2 ツール**)![モデル](media\ad-fs-risk-assessment-model\risk12.png)

 3. 実行、 **SN**コマンドと、 **-t**パラメーターとファイルの場所 (今回は`SN -T “C:\extensions\ThreatDetectionModule.dll”`)![モデル](media\ad-fs-risk-assessment-model\risk13.png)</br>
 コマンドが公開キー トークンを提供 (の私にとって、**公開キー トークンは 714697626ef96b35**)

 4. Dll を追加、**グローバル アセンブリ キャッシュ**プロジェクトの適切なインストーラーを作成し、インストーラーを使用してファイルを GAC に追加する AD FS サーバーのベスト プラクティスになります。 別のソリューションは、使用する**Gacutil.exe** (詳細について**Gacutil.exe**使用可能な[ここ](https://docs.microsoft.com/dotnet/framework/tools/gacutil-exe-gac-tool)) 開発用コンピューターにします。  使用する、AD FS と同じサーバーに、visual studio があるため**Gacutil.exe**次のように

   a.    Visual Studio を含むディレクトリに移動して開発者コマンド プロンプトで、 **Gacutil.exe** (ここでは、ディレクトリは**C:\Program Files (x86) \Microsoft SDKs\Windows\v10.0A\bin\NETFX 4.7.2 Tools**)

   b.    実行、 **Gacutil**コマンド (今回は`Gacutil /IF C:\extensions\ThreatDetectionModule.dll`)![モデル](media\ad-fs-risk-assessment-model\risk14.png)
 
 >[!NOTE]
 >上記の AD FS ファームがある場合、ファーム内の各 AD FS サーバーで実行する必要があります。 

 5. 開いている**Windows PowerShell** dll を登録する次のコマンドを実行
    ```
    Register-AdfsThreatDetectionModule -Name "<Add a name>" -TypeName "<class name that implements interface>, <dll name>, Version=10.0.0.0, Culture=neutral, PublicKeyToken=< Add the Public Key Token from Step 2. above>" -ConfigurationFilePath "<path of the .csv file>”
    ```
    今回は、コマンドはします。 
    ```
    Register-AdfsThreatDetectionModule -Name "IPBlockPlugin" -TypeName "ThreatDetectionModule.UserRiskAnalyzer, ThreatDetectionModule, Version=10.0.0.0, Culture=neutral, PublicKeyToken=714697626ef96b35" -ConfigurationFilePath "C:\extensions\authconfigdb.csv”
    ```
 
    >[!NOTE]
    >AD FS ファームをしている場合でも、1 回だけで、dll を登録する必要があります。 

 6. Dll を登録した後、AD FS サービスを再起動します。

これで、AD FS を使用するための準備完了、dll が登録されているようになりました。

 >[!NOTE]
 > 変更は、プラグインと、プロジェクトが再構築、更新された dll をもう一度登録する必要があります。 を登録する前に、次のコマンドを使用して現在の dll の登録を解除する必要があります。</br></br>
 >`
  UnRegister-AdfsThreatDetectionModule -Name "<name used while registering the dll in 5. above>"
 >`</br></br> 今回は、コマンドはします。
 >``` 
 >UnRegister-AdfsThreatDetectionModule -Name "IPBlockPlugin"
 >```

### <a name="testing-the-plug-in"></a>プラグインのテスト

 1. 開く、 **authconfig.csv**以前に作成したファイル (場所では、今回は**C:\extensions**) を追加し、**エクストラネット Ip**ブロックします。 すべての IP が別々 の行にする必要があり、ないはずのスペース、最後に</br>
 ![model](media\ad-fs-risk-assessment-model\risk18.png)
 
 2. 保存して、ファイルを閉じる

 3. 次の PowerShell コマンドを実行して AD FS で、更新されたファイルをインポートします。 

  ```
  Import-AdfsThreatDetectionModuleConfiguration -name "<name given while registering the dll>" -ConfigurationFilePath "<path of the .csv file>"
  ```
 
  今回は、コマンドはします。 
  ```
   Import-AdfsThreatDetectionModuleConfiguration -name "IPBlockPlugin" -ConfigurationFilePath "C:\extensions\authconfigdb.csv")
 ```
 
 4. 追加した同じ ip アドレスを持つサーバーから開始認証要求**authconfig.csv**します。

 このデモでは使用[AD FS ヘルプ Claims X-Ray ツール](https://adfshelp.microsoft.com/ClaimsXray/TokenRequest)要求を開始します。 X 線ツールを使用する場合は、手順に従ってください。 

 フェデレーション サーバーのインスタンスを入力し、ヒット**認証のテスト**ボタンをクリックします。</br> 
 ![モデル](media\ad-fs-risk-assessment-model\risk15.png) 

 5. 次に示すように、認証がブロックされます。</br>
 ![model](media\ad-fs-risk-assessment-model\risk16.png)
 
ビルドして、プラグインを登録する方法がわかったら、みましょうチュートリアル新しいインターフェイスとクラスを使用して実装を理解するプラグインのコードで導入されたモデル。 

## <a name="plug-in-code-walkthrough"></a>プラグインのコードのチュートリアル

プロジェクトを開く`ThreatDetectionModule.sln`Visual Studio を使用し、メイン ファイルを開きます**UserRiskAnalyzer.cs**から、**ソリューション エクスプ ローラー**画面の右に</br>
![model](media\ad-fs-risk-assessment-model\risk17.png)
 
ファイルには、メイン クラスは抽象クラスを実装する UserRiskAnalyzer が含まれています[ThreatDetectionModule](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule?view=adfs-2019)とインターフェイス[IRequestReceivedThreatDetectionModule](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.irequestreceivedthreatdetectionmodule?view=adfs-2019)要求から ip アドレスを読み取る。コンテキストでは、AD FS の DB から読み込まれた ip アドレスで取得した IP を比較し、IP に一致する場合は、要求をブロックします。 これらの型について詳しく見てみましょう

### <a name="threatdetectionmodule-abstract-class"></a>ThreatDetectionModule 抽象クラス

この抽象クラスは、AD FS のプロセスに合わせてプラグインのコードを実行できるように AD FS のパイプラインにプラグインを読み込みます。 

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
|[OnAuthenticationPipelineLoad](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onauthenticationpipelineload?view=adfs-2019) |void|そのパイプラインにプラグインが読み込まれるときに、AD FS によって呼び出されます| 
|[OnAuthenticationPipelineUnload](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onauthenticationpipelineunload?view=adfs-2019) |void|プラグインがそのパイプラインから読み込まれたときに AD FS によって呼び出されます| 
|[OnConfigurationUpdate](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onconfigurationupdate?view=adfs-2019)| void|AD FS 構成の更新によって呼び出されます |
|**プロパティ** |**型** |**定義**|
|[VendorName](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.vendorname?view=adfs-2019)|String |プラグインを所有しているベンダーの名前を取得します。|
|[ModuleIdentifier](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.moduleidentifier?view=adfs-2019)|String |プラグインの識別子を取得します。|

このサンプル プラグインでは使用[OnAuthenticationPipelineLoad](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onauthenticationpipelineload?view=adfs-2019)と[OnConfigurationUpdate](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onconfigurationupdate?view=adfs-2019) AD FS DB から定義済みの ip アドレスを読み取る方法。 [OnAuthenticationPipelineLoad](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onauthenticationpipelineload?view=adfs-2019)プラグインを登録中に AD FS を使用したときに呼び出される[OnConfigurationUpdate](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule.onconfigurationupdate?view=adfs-2019)を使用して、.csv をインポート時に呼び出される、`Import-AdfsThreatDetectionModuleConfiguration`コマンドレット。 

#### <a name="irequestreceivedthreatdetectionmodule-interface"></a>IRequestReceivedThreatDetectionModule インターフェイス

これは、[インターフェイス](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.irequestreceivedthreatdetectionmodule?view=adfs-2019)認証要求を受け取ると AD FS がユーザーに入る前に資格情報など、認証プロセスの段階で要求を受信した時点でリスク評価を実装することができます。 
 
```
public interface IRequestReceivedThreatDetectionModule
{
Task<ThrottleStatus> EvaluateRequest (
ThreatDetectionLogger logger, 
RequestContext requestContext );
}
```

インターフェイスが含まれています[EvaluateRequest](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.irequestreceivedthreatdetectionmodule.evaluaterequest?view=adfs-2019)リスク評価ロジックを記述する requestContext 入力パラメーターに渡されたメソッドの認証要求のコンテキストを使用することができます。 RequestContext パラメーターは型[RequestContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019)します。 

渡されたその他の入力パラメーターが型であるロガー [ThreatDetectionLogger](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionlogger?view=adfs-2019)します。 パラメーターは、書き込み、エラーを使用する監査や AD FS ログへのメッセージをデバッグします。 

メソッドを返します[ThrottleStatus](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.throttlestatus?view=adfs-2019) (場合は 0 NotEvaluated、ブロックを 1 と 2 を許可する) を AD FS にするか、ブロックまたは許可要求。

プラグインは、サンプルでは[EvaluateRequest](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.irequestreceivedthreatdetectionmodule.evaluaterequest?view=adfs-2019)メソッドの実装を解析し、 [clientIpAddress](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext.clientipaddresses?view=adfs-2019#Microsoft_IdentityServer_Public_ThreatDetectionFramework_RequestContext_ClientIpAddresses)から、 [requestContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019)パラメーターと、すべての ip アドレスと比較しますAD FS データベースから読み込まれます。 メソッドは 2 を返しますの一致が見つかった場合**ブロック**、それ以外の場合 1 を返します**許可**します。 返される値に基づいて、AD FS をブロックまたは要求を許可します。 

>[!NOTE]
>唯一 IRequestReceivedThreatDetectionModule インターフェイスを実装する前に説明したサンプル プラグイン。 ただし、リスク評価のモデルは、2 つの追加 (リスクの評価ロジック duing 事前認証段階を実装) を IPreAuthenticationThreatDetectionModule – と IPostAuthenticationThreatDetectionModule (リスクを実装するインターフェイス評価ロジック 事後認証段階)。 2 つのインターフェイスの詳細については後述します。 

#### <a name="ipreauthenticationthreatdetectionmodule-interface"></a>IPreAuthenticationThreatDetectionModule インターフェイス 

これは、[インターフェイス](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.ipreauthenticationthreatdetectionmodule?view=adfs-2019)資格情報を提供するユーザーが AD FS はそれらにつまり事前認証段階を評価する前に、ポイント時のリスク評価ロジックを実装することができます。 

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
インターフェイスが含まれています[EvaluatePreAuthentication](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.ipreauthenticationthreatdetectionmodule.evaluatepreauthentication?view=adfs-2019)渡されたメソッドの情報を使用することができますが、 [RequestContext requestContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019)、 [SecurityContext securityContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.securitycontext?view=adfs-2019)、 [ProtocolContext protocolContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.protocolcontext?view=adfs-2019)、および[IList<Claim> additionalClams](https://docs.microsoft.com/dotnet/api/system.collections.generic.ilist-1?view=netframework-4.7.2)事前認証のリスク評価ロジックを記述するパラメーターを入力します。 

>[!NOTE]
>各コンテキストの種類で渡されるプロパティの一覧は、次を参照してください。 [RequestContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019)、 [SecurityContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.securitycontext?view=adfs-2019)、および[ProtocolContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.protocolcontext?view=adfs-2019)クラス定義です。 

渡されたその他の入力パラメーターが型であるロガー [ThreatDetectionLogger](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionlogger?view=adfs-2019)します。 パラメーターは、書き込み、エラーを使用する監査や AD FS ログへのメッセージをデバッグします。

メソッドを返します[ThrottleStatus](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.throttlestatus?view=adfs-2019) (場合は 0 NotEvaluated、ブロックを 1 と 2 を許可する) を AD FS にするか、ブロックまたは許可要求。 

#### <a name="ipostauthenticationthreatdetectionmodule-interface"></a>IPostAuthenticationThreatDetectionModule インターフェイス

これは、[インターフェイス](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.ipostauthenticationthreatdetectionmodule?view=adfs-2019)ユーザーが資格情報を提供し、AD FS が認証つまり事後認証段階を実行した後は、リスク評価のロジックを実装することができます。 

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

インターフェイスが含まれています[EvaluatePostAuthentication](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.ipostauthenticationthreatdetectionmodule.evaluatepostauthentication?view=adfs-2019)渡されたメソッドの情報を使用することができますが、 [RequestContext requestContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019)、 [SecurityContext securityContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.securitycontext?view=adfs-2019)、 [ProtocolContext protocolContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.protocolcontext?view=adfs-2019)、および[IList<Claim> additionalClams](https://docs.microsoft.com/dotnet/api/system.collections.generic.ilist-1?view=netframework-4.7.2)事後認証のリスク評価ロジックを記述するパラメーターを入力します。 

>[!NOTE]
> 各コンテキストの種類で渡されるプロパティの一覧については、参照[RequestContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.requestcontext?view=adfs-2019)、 [SecurityContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.securitycontext?view=adfs-2019)、および[ProtocolContext](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.protocolcontext?view=adfs-2019)クラス定義です。 

渡されたその他の入力パラメーターが型であるロガー [ThreatDetectionLogger](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionlogger?view=adfs-2019)します。 パラメーターは、書き込み、エラーを使用する監査や AD FS ログへのメッセージをデバッグします。 

メソッドを返します、[リスク スコア](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.authentication.riskscoreconstants?view=adfs-2019)要求規則と AD FS のポリシーで使用することができます。 

>[!NOTE]
>(この例では UserRiskAnalyzer) ではメイン クラスが派生する必要がプラグインが機能する、 [ThreatDetectionModule](https://docs.microsoft.com/dotnet/api/microsoft.identityserver.public.threatdetectionframework.threatdetectionmodule?view=adfs-2019)クラスを抽象化し、上記で説明した 3 つのインターフェイスの少なくとも 1 つを実装する必要があります。 Dll が登録されると、AD FS はどのインターフェイスが実装されているを確認し、そのパイプラインの段階で適切な呼び出し。

### <a name="faqs"></a>よく寄せられる質問

**これらのプラグインを構築する必要がありますはなぜですか。**</br>
**A:** これらのプラグインは、パスワード スプレー攻撃などの攻撃からお客様の環境をセキュリティで保護する追加の機能を提供するだけでなくが、要件に基づいて、独自のリスク評価ロジックを構築する柔軟性も提供します。 

**ログのキャプチャの場所**</br>
**A:** WriteAdminLogErrorMessage メソッドを使用して、"AD FS/Admin"イベント ログにエラー ログを書き込むことができます、「AD FS の監査」セキュリティ監査ログ WriteAuditMessage メソッドを使用してログしデバッグ WriteDebugMessage メソッドを使用して、"AD FS トレース"デバッグ ログに記録します。 

**できる AD FS 認証プロセスの待機時間を増やすなプラグインを追加するか。**</br>
**A:** 待機時間による影響については、実装するリスク評価ロジックの実行に要した時間によって決まります。 プラグインの実稼働環境で展開する前に待機時間による影響を評価することをお勧めします。 

**AD FS はなぜできないユーザーなど、危険な ip アドレスの一覧を提案しますか。**</br>
**A:** ただし、現在使用可能なプラグ可能なリスク評価のモデル内のユーザーなど、危険な ip アドレスを提案するインテリジェンスの構築に取り組んでいます。 起動を日付にすぐにお知らせします。 
