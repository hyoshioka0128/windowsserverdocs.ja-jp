---
title: Windows Server での AD FS のためのカスタム認証方法を構築する
description: このシナリオでは、Windows Server で AD FS 用のカスタム認証方法を構築する方法について説明します。
author: billmath
ms.author: billmath
manager: daveba
ms.date: 05/23/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 868878fa9c38e1a37ec238d57be578727c189471
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2020
ms.locfileid: "87519891"
---
# <a name="build-a-custom-authentication-method-for-ad-fs-in-windows-server"></a>Windows Server での AD FS のためのカスタム認証方法を構築する

このチュートリアルでは、Windows Server 2012 R2 で AD FS 用のカスタム認証方法を実装する手順について説明します。 詳細については、「[その他の認証方法](/previous-versions/orphan-topics/ws.11/dn383648(v=ws.11))」を参照してください。

> [!WARNING]
> ここで作成できる例は、 &nbsp; 学習のみを目的としています。 &nbsp;これらの手順は、モデルの必須要素を公開するために使用できる、最も単純で最小の実装用です。 &nbsp;認証バックエンド、エラー処理、または構成データはありません。

## <a name="setting-up-the-development-box"></a>開発ボックスの設定

このチュートリアルでは、Visual Studio 2012 を使用します。 プロジェクトは、Windows 用の .NET クラスを作成できる任意の開発環境を使用してビルドできます。 **Beginauthentication**メソッドと**tryendauthentication**メソッドは .NET Framework バージョン4.5 の一部を使用するため、プロジェクトは .net **4.5 を対象**とする必要があります。プロジェクトに必要な参照が1つあります。

| 参照 dll | 参照先 | 次のために必須: |
|--|--|--|
| Microsoft.IdentityServer.Web.dll | この dll は、AD FS がインストールされている Windows Server 2012 R2 サーバーの% windir% ADFS にあります。<p>この dll は、開発用コンピューターにコピーし、プロジェクトに明示的に作成する必要があります。 | IAuthenticationContext、IProofData を含むインターフェイス型 |

## <a name="create-the-provider"></a>プロバイダーを作成する

1. Visual Studio 2012: [ファイル]、[新規 >プロジェクトの >] の順に選択します。

2. [クラスライブラリ] を選択し、.NET 4.5 を対象としていることを確認します。

    ![プロバイダーの作成](media/ad-fs-build-custom-auth-method/Dn783423.71a57ae1-d53d-462b-a846-5b3c02c7d3f2(MSDN.10).jpg "プロバイダーの作成")

3. AD FS がインストールされている Windows Server 2012 R2 サーバーで、% windir% ADFS から**Microsoft.IdentityServer.Web.dll**のコピーを作成し、開発用コンピューターのプロジェクトフォルダーに貼り付けます。

4. **ソリューションエクスプローラー**で、[**参照**] を右クリックし、[**参照の追加**] をクリックします。

5. **Microsoft.IdentityServer.Web.dll**のローカルコピーを参照し、[**追加.** ..]

6. [ **OK** ] をクリックして、新しい参照を確認します。

    ![プロバイダーの作成](media/ad-fs-build-custom-auth-method/Dn783423.f18df353-9259-4744-b4b6-dd780ce90951(MSDN.10).jpg "プロバイダーの作成")

    これで、プロバイダーに必要なすべての型を解決するように設定されました。

7. プロジェクトに新しいクラスを追加します (プロジェクトを右クリックし、[追加...] **クラス...**)次に示すように、 **Myadapter**のような名前を付けます。

    ![プロバイダーの作成](media/ad-fs-build-custom-auth-method/Dn783423.6b6a7a8b-9d66-40c7-8a86-a2e3b9e14d09(MSDN.10).jpg "プロバイダーの作成")

8. 新しいファイル MyAdapter.cs で、既存のコードを次のコードに置き換えます。

    ```
    using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Text;
        using System.Threading.Tasks;
        using System.Globalization;
        using System.IO;
        using System.Net;
        using System.Xml.Serialization;
        using Microsoft.IdentityServer.Web.Authentication.External;
        using Claim = System.Security.Claims.Claim;

        namespace MFAadapter
        {
        class MyAdapter : IAuthenticationAdapter
        {
         }
        }
    ```

    これで、IAuthenticationAdapter で F12 キー ([定義に進む]) を使用して、必要なインターフェイスメンバーのセットを確認できるようになります。

    次に、これらの単純な実装を行うことができます。

9. クラスの内容全体を次のように置き換えます。

    ```
    namespace MFAadapter
    {
    class MyAdapter : IAuthenticationAdapter
    {
    public IAuthenticationAdapterMetadata Metadata
    {
    //get { return new <instance of IAuthenticationAdapterMetadata derived class>; }
    }

    public IAdapterPresentation BeginAuthentication(Claim identityClaim, HttpListenerRequest request, IAuthenticationContext authContext)
    {
    //return new instance of IAdapterPresentationForm derived class
    }

    public bool IsAvailableForUser(Claim identityClaim, IAuthenticationContext authContext)
    {
    return true; //its all available for now
    }

    public void OnAuthenticationPipelineLoad(IAuthenticationMethodConfigData configData)
    {
    //this is where AD FS passes us the config data, if such data was supplied at registration of the adapter
    }

    public void OnAuthenticationPipelineUnload()
    {
     }

    public IAdapterPresentation OnError(HttpListenerRequest request, ExternalAuthenticationException ex)
    {
    //return new instance of IAdapterPresentationForm derived class
    }

    public IAdapterPresentation TryEndAuthentication(IAuthenticationContext authContext, IProofData proofData, HttpListenerRequest request, out Claim[] outgoingClaims)
    {
    //return new instance of IAdapterPresentationForm derived class
            }
        }
    }
    ```

1. まだビルドする準備ができていません...さらに2つのインターフェイスがあります。

    2つのクラスをプロジェクトに追加します。1つはメタデータ用で、もう1つはプレゼンテーションフォーム用です。 上記のクラスと同じファイル内にこれらを追加できます。

    ```
    class MyMetadata : IAuthenticationAdapterMetadata
    {
    }
    class MyPresentationForm : IAdapterPresentationForm
    {
    }
    ```

2. 次に、それぞれに必要なメンバーを追加できます。最初に (有用なインラインコメントを含む) メタデータ

    ```
    class MyMetadata : IAuthenticationAdapterMetadata
    {
    //Returns the name of the provider that will be shown in the AD FS management UI (not visible to end users)
    public string AdminName
    {
    get { return "My Example MFA Adapter"; }
    }

    //Returns an array of strings containing URIs indicating the set of authentication methods implemented by the adapter
    /// AD FS requires that, if authentication is successful, the method actually employed will be returned by the
    /// final call to TryEndAuthentication(). If no authentication method is returned, or the method returned is not
    /// one of the methods listed in this property, the authentication attempt will fail.
    public virtual string[] AuthenticationMethods
    {
    get { return new[] { "http://example.com/myauthenticationmethod1", "http://example.com/myauthenticationmethod2" }; }
    }

    /// Returns an array indicating which languages are supported by the provider. AD FS uses this information
    /// to determine the best languagelocale to display to the user.
    public int[] AvailableLcids
    {
    get
    {
    return new[] { new CultureInfo("en-us").LCID, new CultureInfo("fr").LCID};
    }
    }

    /// Returns a Dictionary containing the set of localized friendly names of the provider, indexed by lcid.
    /// These Friendly Names are displayed in the "choice page" offered to the user when there is more than
    /// one secondary authentication provider available.
    public Dictionary<int, string> FriendlyNames
    {
    get
    {
    Dictionary<int, string> _friendlyNames = new Dictionary<int, string>();
    _friendlyNames.Add(new CultureInfo("en-us").LCID, "Friendly name of My Example MFA Adapter for end users (en)");
    _friendlyNames.Add(new CultureInfo("fr").LCID, "Friendly name translated to fr locale");
    return _friendlyNames;
    }
    }

    /// Returns a Dictionary containing the set of localized descriptions (hover over help) of the provider, indexed by lcid.
    /// These descriptions are displayed in the "choice page" offered to the user when there is more than one
    /// secondary authentication provider available.
    public Dictionary<int, string> Descriptions
    {
    get
    {
    Dictionary<int, string> _descriptions = new Dictionary<int, string>();
    _descriptions.Add(new CultureInfo("en-us").LCID, "Description of My Example MFA Adapter for end users (en)");
    _descriptions.Add(new CultureInfo("fr").LCID, "Description translated to fr locale");
    return _descriptions;
    }
    }

    /// Returns an array indicating the type of claim that the adapter uses to identify the user being authenticated.
    /// Note that although the property is an array, only the first element is currently used.
    /// MUST BE ONE OF THE FOLLOWING
    /// "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"
    /// "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"
    /// "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"
    /// "https://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid"
    public string[] IdentityClaims
    {
    get { return new[] { "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn" }; }
    }

    //All external providers must return a value of "true" for this property.
    public bool RequiresIdentity
    {
    get { return true; }
    }
    }
    ```

    次に、プレゼンテーションフォームを示します。

    ```
    class MyPresentationForm : IAdapterPresentationForm
    {
    /// Returns the HTML Form fragment that contains the adapter user interface. This data will be included in the web page that is presented
    /// to the cient.
    public string GetFormHtml(int lcid)
    {
    string htmlTemplate = Resources.FormPageHtml; //todo we will implement this
    return htmlTemplate;
    }

    /// Return any external resources, ie references to libraries etc., that should be included in
    /// the HEAD section of the presentation form html.
    public string GetFormPreRenderHtml(int lcid)
    {
    return null;
    }

    //returns the title string for the web page which presents the HTML form content to the end user
    public string GetPageTitle(int lcid)
    {
    return "MFA Adapter";
    }
    ```

3.  上の**リソースの FormPageHtml**要素の ' todo ' に注意してください。

    1分以内に修正できますが、最初に、新しく実装された型に基づいて、最後に必要な return ステートメントを最初の MyAdapter クラスに追加してみましょう。 これを行うには、次の*斜体*の項目を既存の IAuthenticationAdapter 実装に追加します。

    ```
    class MyAdapter : IAuthenticationAdapter
    {
    public IAuthenticationAdapterMetadata Metadata
    {
    //get { return new <instance of IAuthenticationAdapterMetadata derived class>; }
    get { return new MyMetadata(); }
    }

    public IAdapterPresentation BeginAuthentication(Claim identityClaim, HttpListenerRequest request, IAuthenticationContext authContext)
    {
    //return new instance of IAdapterPresentationForm derived class
    return new MyPresentationForm();
    }

    public bool IsAvailableForUser(Claim identityClaim, IAuthenticationContext authContext)
    {
    return true; //its all available for now
    }

    public void OnAuthenticationPipelineLoad(IAuthenticationMethodConfigData configData)
    {
    //this is where AD FS passes us the config data, if such data was supplied at registration of the adapter

    }

    public void OnAuthenticationPipelineUnload()
    {

    }

    public IAdapterPresentation OnError(HttpListenerRequest request, ExternalAuthenticationException ex)
    {
    //return new instance of IAdapterPresentationForm derived class
        return new MyPresentationForm();
    }

    public IAdapterPresentation TryEndAuthentication(IAuthenticationContext authContext, IProofData proofData, HttpListenerRequest request, out Claim[] outgoingClaims)
    {
    //return new instance of IAdapterPresentationForm derived class
    outgoingClaims = new Claim[0];
    return new MyPresentationForm();
    }

    }
    ```

13. ここで、html フラグメントを含むリソースファイルを使用します。 次の内容を含む新しいテキストファイルをプロジェクトフォルダーに作成します。

    ```
    <div id="loginArea">
    <form method="post" id="loginForm" >
    <!-- These inputs are required by the presentation framework. Do not modify or remove -->
    <input id="authMethod" type="hidden" name="AuthMethod" value="%AuthMethod%"/>
    <input id="context" type="hidden" name="Context" value="%Context%"/>
    <!-- End inputs are required by the presentation framework. -->
    <p id="pageIntroductionText">This content is provided by the MFA sample adapter. Challenge inputs should be presented below.</p>
    <label for="challengeQuestionInput" class="block">Question text</label>
    <input id="challengeQuestionInput" name="ChallengeQuestionAnswer" type="text" value="" class="text" placeholder="Answer placeholder" />
    <div id="submissionArea" class="submitMargin">
    <input id="submitButton" type="submit" name="Submit" value="Submit" onclick="return AuthPage.submitAnswer()"/>
    </div>
    </form>
    <div id="intro" class="groupMargin">
    <p id="supportEmail">Support information</p>
    </div>
    <script type="text/javascript" language="JavaScript">
    //<![CDATA[
    function AuthPage() { }
    AuthPage.submitAnswer = function () { return true; };
    //]]>
    </script></div>
    ```

14. 次に、[**プロジェクト->コンポーネントの追加] を選択します。リソース**ファイルにファイル**リソース**の名前を指定し、[追加] をクリックし**ます。**

   ![プロバイダーの作成](media/ad-fs-build-custom-auth-method/Dn783423.3369ad8f-f65f-4f36-a6d5-6a3edbc1911a(MSDN.10).jpg "プロバイダーの作成")

15. 次に、**リソース .resx**ファイル内で、[リソースの追加] を選択します。 **既存のファイルを追加**します。 前の手順で保存したテキストファイル (html フラグメントを含む) に移動します。

   リソースファイル (.resx ファイル) 名のプレフィックスとリソース自体の名前によって、新しいリソースの名前が GetFormHtml コードによって正しく解決されることを確認します。

```
    public string GetFormHtml(int lcid)
    {
    string htmlTemplate = Resources.MfaFormHtml; //Resxfilename.resourcename
    return htmlTemplate;
    }
```

   これで、をビルドできるようになります。

## <a name="build-the-adapter"></a>アダプターを作成する

アダプターは、Windows の GAC にインストールできる厳密に名前が付けられた .NET アセンブリに組み込まれている必要があります。 これを Visual Studio プロジェクトで実現するには、次の手順を実行します。

1. ソリューションエクスプローラーでプロジェクト名を右クリックし、[**プロパティ**] をクリックします。

2. [**署名**] タブで、 **[アセンブリの署名**] チェックボックスをオンにし、[**厳密な名前のキーファイルを選択**してください] で [ **<新規作成... >** を選択します。キーファイル名とパスワードを入力し、[ **OK]** をクリックします。 次に **、[アセンブリの署名**がチェックされ、**遅延署名のみ**] がオフになっていることを確認します。 [プロパティ] [**署名**] ページは次のようになります。

    ![プロバイダーの構築](media/ad-fs-build-custom-auth-method/Dn783423.0b1a1db2-d64e-4bb8-8c01-ef34296a2668(MSDN.10).jpg "プロバイダーの構築")

3. 次に、ソリューションをビルドします。

## <a name="deploy-the-adapter-to-your-ad-fs-test-machine"></a>アダプターを AD FS のテストコンピューターにデプロイする

外部プロバイダーを AD FS によって呼び出すには、その前にシステムに登録する必要があります。 アダプタープロバイダーは、GAC へのインストールなど、必要なインストール操作を実行するインストーラーを提供する必要があります。また、インストーラーは AD FS での登録をサポートしている必要があります。 これが行われない場合、管理者は次の Windows PowerShell の手順を実行する必要があります。 これらの手順は、テストとデバッグを有効にするためにラボで使用できます。

### <a name="prepare-the-test-ad-fs-machine"></a>テスト AD FS コンピューターを準備する

ファイルをコピーして GAC に追加します。

1. Windows Server 2012 R2 コンピューターまたは仮想マシンがあることを確認します。

2. AD FS の役割サービスをインストールし、少なくとも1つのノードを含むファームを構成します。

    ラボ環境でフェデレーションサーバーをセットアップする詳細な手順については、「 [Windows server 2012 R2 AD FS 展開ガイド](/previous-versions/orphan-topics/ws.11/dn383648(v=ws.11))」を参照してください。

3. Gacutil.exe ツールをサーバーにコピーします。

    Gacutil.exe は、Windows 8 コンピューター上の **% homedrive% Program Files (x86) Microsoft sdkswindowsv 8.0 abinnetfx 4.0 ツール**にあります。 **gacutil.exe**ファイル自体に加え、 **1033**、 **En-us**、および**NETFX 4.0 ツール**の場所の下にあるその他のローカライズされたリソースフォルダーが必要です。

4. プロバイダーファイル (1 つまたは複数の厳密な名前の署名された .dll ファイル) を**gacutil.exe**と同じフォルダーの場所にコピーします (場所は便宜上)

5. ファーム内の各 AD FS フェデレーションサーバーの GAC に .dll ファイルを追加します。

    例: コマンドラインツール GACutil.exe を使用して、GAC に dll を追加します。`C:>.gacutil.exe /if .<yourdllname>.dll`

    GAC に結果のエントリを表示するには、次のようにします。`C:>.gacutil.exe /l <yourassemblyname>`

6.

### <a name="register-your-provider-in-ad-fs"></a>AD FS にプロバイダーを登録する

上記の前提条件が満たされたら、フェデレーションサーバーで Windows PowerShell コマンドウィンドウを開き、次のコマンドを入力します (Windows Internal Database を使用するフェデレーションサーバーファームを使用している場合は、ファームのプライマリフェデレーションサーバーでこれらのコマンドを実行する必要があります)。

1. `Register-AdfsAuthenticationProvider –TypeName YourTypeName –Name “AnyNameYouWish” [–ConfigurationFilePath (optional)]`

    ここで、Typename は .NET の厳密な型名です。 "YourIAuthenticationAdapterImplementationClassName, your Assemblyname, Version = your Assemblyversion, Culture = ニュートラル, PublicKeyToken = your Publickeytokenvalue, processorArchitecture = MSIL"

    これにより、外部プロバイダーが AD FS に登録されます。ここで指定した名前が使用されます。

2. (たとえば、Windows サービススナップインを使用して) AD FS サービスを再起動します。

3. コマンド `Get-AdfsAuthenticationProvider` を実行します。

    これにより、プロバイダーがシステムのプロバイダーの1つとして表示されます。

    例:

    ```powershell
    $typeName = "MFAadapter.MyAdapter, MFAadapter, Version=1.0.0.0, Culture=neutral, PublicKeyToken=e675eb33c62805a0, processorArchitecture=MSIL”
    Register-AdfsAuthenticationProvider -TypeName $typeName -Name “MyMFAAdapter”
    net stop adfssrv
    net start adfssrv
    ```

    AD FS 環境でデバイス登録サービスが有効になっている場合は、次の PowerShell コマンドも実行します。`net start drs`

    登録されているプロバイダーを確認するには、次の PowerShell コマンドを使用し `Get-AdfsAuthenticationProvider` ます。

    これにより、プロバイダーがシステムのプロバイダーの1つとして表示されます。

### <a name="create-the-ad-fs-authentication-policy-that-invokes-your-adapter"></a>アダプターを呼び出す AD FS 認証ポリシーを作成する

#### <a name="create-the-authentication-policy-using-the-ad-fs-management-snap-in"></a>AD FS 管理スナップインを使用して認証ポリシーを作成する

1. [サーバーマネージャー**ツール**] メニューから AD FS 管理スナップインを開きます。

2. [**認証ポリシー**] をクリックします。

3. 中央のウィンドウで、[ **Multi-Factor Authentication**] の下にある [**グローバル設定**] の右側にある [**編集**] リンクをクリックします。

4. ページの下部にある [**追加の認証方法の選択**] で、プロバイダーの adminname のチェックボックスをオンにします。 **[適用]** をクリックします。

5. アダプターを使用して MFA を呼び出す "トリガー" を提供するには、[**場所**] で、**エクストラネット**と**イントラネット**の両方を確認します (例)。 **[OK]** をクリックします。 (証明書利用者ごとにトリガーを構成するには、後述の「Windows PowerShell を使用して認証ポリシーを作成する」を参照してください)。

6. 次のコマンドを使用して結果を確認します。

    最初に使用 `Get-AdfsGlobalAuthenticationPolicy` します。 プロバイダー名は、AdditionalAuthenticationProvider 値の1つとして表示されます。

    次に、を使用し `Get-AdfsAdditionalAuthenticationRule` ます。 管理者 UI でポリシーを選択した結果として、エクストラネットとイントラネットのルールが構成されていることを確認します。

#### <a name="create-the-authentication-policy-using-windows-powershell"></a>Windows PowerShell を使用して認証ポリシーを作成する

1. 最初に、グローバルポリシーでプロバイダーを有効にします。

    ```powershell
    Set-AdfsGlobalAuthenticationPolicy -AdditionalAuthenticationProvider “YourAuthProviderName”`
    ```

    > [!NOTE]
    > AdditionalAuthenticationProvider パラメーターに指定された値は、上の Register-adfsauthenticationprovider コマンドレットの "Name" パラメーターに指定した値と、Register-adfsauthenticationprovider コマンドレットの出力の "Name" プロパティに対応していることに注意してください。

    ```powershell
    Set-AdfsGlobalAuthenticationPolicy –AdditionalAuthenticationProvider “MyMFAAdapter”`
    ```

2. 次に、グローバルまたは証明書利用者固有の規則を構成して、MFA をトリガーします。

   例 1: 外部要求に対して MFA を要求するグローバルルールを作成するには、次のようにします。

   ```powershell
   Set-AdfsAdditionalAuthenticationRule –AdditionalAuthenticationRules 'c:[type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", value == "false"] => issue(type = "https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "https://schemas.microsoft.com/claims/multipleauthn" );
   ```

   例 2: 特定の証明書利用者への外部要求に対して MFA を要求する MFA 規則を作成するには (個々のプロバイダーは、Windows Server 2012 R2 の AD FS の個々の証明書利用者に接続できないことに注意してください)。

    ```powershell
    $rp = Get-AdfsRelyingPartyTrust –Name <Relying Party Name>
    Set-AdfsRelyingPartyTrust –TargetRelyingParty $rp –AdditionalAuthenticationRules 'c:[type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", value == "false"] => issue(type = "https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "https://schemas.microsoft.com/claims/multipleauthn" );
    ```

### <a name="authenticate-with-mfa-using-your-adapter"></a>アダプターを使用して MFA で認証する

最後に、次の手順を実行してアダプターをテストします。

1. AD FS グローバルプライマリ認証の種類が、エクストラネットとイントラネットの両方のフォーム認証として構成されていることを確認します (これにより、デモを特定のユーザーとして簡単に認証できるようになります)。

    1. AD FS スナップインの [**認証ポリシー**] の [**プライマリ認証**] 領域で、[**グローバル設定**] の横にある [**編集**] をクリックします。

        1. または、**多要素ポリシー** UI の [**プライマリ**] タブをクリックします。

2. エクストラネットとイントラネットの両方の認証方法で、**フォーム認証**が唯一のオプションとして選択されていることを確認します。 **[OK]** をクリックします。

3. IDP で開始されたサインオン html ページ (https:// <fsname> /adfs/ls/idpinitiatedsignon.htm) を開き、テスト環境で有効な AD ユーザーとしてサインインします。

4. プライマリ認証の資格情報を入力してください。

5. チャレンジの質問の例が表示された MFA フォームページが表示されます。

    複数のアダプターが構成されている場合は、上記のフレンドリ名を使用して MFA の選択ページが表示されます。

    ![アダプターを使用した認証](media/ad-fs-build-custom-auth-method/Dn783423.c98d2712-cbd3-4cb9-ac03-2838b81c4f63(MSDN.10).jpg "アダプターを使用した認証")

    ![アダプターを使用した認証](media/ad-fs-build-custom-auth-method/Dn783423.fd3aefc0-ef6c-4a8c-a737-4914c78ff2d2(MSDN.10).jpg "アダプターを使用した認証")

これで、インターフェイスを実用的に実装できるようになり、モデルの動作についての知識が得られました。 BeginAuthentication および TryEndAuthentication にブレークポイントを設定するための追加の例として trym を使用できます。 ユーザーが最初に MFA フォームに入力したときに BeginAuthentication が実行され、フォームの送信のたびに TryEndAuthentication がトリガーされることに注意してください。

## <a name="update-the-adapter-for-successful-authentication"></a>認証が成功するようにアダプターを更新する

しかし、お待ちください。アダプターの例は正常に認証されません!  これは、コード内に TryEndAuthentication に対して null を返すものがないためです。

上記の手順を完了すると、基本的なアダプターの実装を作成し、AD FS サーバーに追加しました。 MFA フォームページは取得できますが、TryEndAuthentication 実装に適切なロジックがまだ配置されていないため、まだ認証できません。 それを追加しましょう。

TryEndAuthentication の実装を思い出してください。

```
public IAdapterPresentation TryEndAuthentication(IAuthenticationContext authContext, IProofData proofData, HttpListenerRequest request, out Claim[] outgoingClaims)
{
//return new instance of IAdapterPresentationForm derived class
outgoingClaims = new Claim[0];
return new MyPresentationForm();
}
```

常に MyPresentationForm () を返さないように更新してみましょう。 これには、クラス内に1つの単純なユーティリティメソッドを作成できます。

```
static bool ValidateProofData(IProofData proofData, IAuthenticationContext authContext)
{
if (proofData == null || proofData.Properties == null || !proofData.Properties.ContainsKey("ChallengeQuestionAnswer"))
{
throw new ExternalAuthenticationException("Error - no answer found", authContext);
}

if ((string)proofData.Properties["ChallengeQuestionAnswer"] == "adfabric")
{
return true;
}
else
{
return false;
}
}
```

次に、次のように TryEndAuthentication を更新します。

```
public IAdapterPresentation TryEndAuthentication(IAuthenticationContext authContext, IProofData proofData, HttpListenerRequest request, out Claim[] outgoingClaims)
{
outgoingClaims = new Claim[0];
if (ValidateProofData(proofData, authContext))
{
//authn complete - return authn method
outgoingClaims = new[]
{
// Return the required authentication method claim, indicating the particulate authentication method used.
new Claim( "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod",
"http://example.com/myauthenticationmethod1" )
};
return null;
}
else
{
//authentication not complete - return new instance of IAdapterPresentationForm derived class
return new MyPresentationForm();
}
}
```

次に、[テスト] ボックスでアダプターを更新する必要があります。 最初に AD FS ポリシーを元に戻し、次に AD FS から登録を解除してから AD FS を再起動してから、その .dll を gac に追加してから、新しい .dll を GAC に追加してから、AD FS に登録してから AD FS を再起動し、AD FS ポリシーを再構成する必要があります。

## <a name="deploy-and-configure-the-updated-adapter-on-your-test-ad-fs-machine"></a>テスト AD FS コンピューターで更新されたアダプターをデプロイして構成する

### <a name="clear-ad-fs-policy"></a>AD FS ポリシーのクリア

次に示すように、MFA UI で MFA 関連のすべてのチェックボックスをオフにし、[OK] をクリックします。

![ポリシーのクリア](media/ad-fs-build-custom-auth-method/Dn783423.c111b4e7-5b05-413c-8b0f-222a0e91ac1f(MSDN.10).jpg "ポリシーのクリア")

### <a name="unregister-provider-windows-powershell"></a>プロバイダーの登録解除 (Windows PowerShell)

`PS C:> Unregister-AdfsAuthenticationProvider –Name “YourAuthProviderName”`

例:`PS C:> Unregister-AdfsAuthenticationProvider –Name “MyMFAAdapter”`

"Name" に渡す値は、Register-adfsauthenticationprovider コマンドレットに指定した "Name" と同じ値であることに注意してください。 また、Register-adfsauthenticationprovider から出力される "Name" プロパティでもあります。

プロバイダーの登録を解除する前に、AdfsGlobalAuthenticationPolicy からプロバイダーを削除する必要があることに注意してください (AD FS 管理スナップインでチェックインしたチェックボックスをオフにするか、Windows PowerShell を使用します)。

この操作の後に、AD FS サービスを再起動する必要があることに注意してください。

### <a name="remove-assembly-from-gac"></a>GAC からのアセンブリの削除

1. まず、次のコマンドを使用して、エントリの完全修飾された厳密な名前を検索します。`C:>.gacutil.exe /l <yourAdapterAssemblyName>`

    例:`C:>.gacutil.exe /l mfaadapter`

2. 次に、次のコマンドを使用して GAC から削除します。`.gacutil /u “<output from the above command>”`

    例:`C:>.gacutil /u “mfaadapter, Version=1.0.0.0, Culture=neutral, PublicKeyToken=e675eb33c62805a0, processorArchitecture=MSIL”`

### <a name="add-the-updated-assembly-to-gac"></a>更新されたアセンブリを GAC に追加する

最初に、更新された .dll をローカルに貼り付けてください。 `C:>.gacutil.exe /if .MFAAdapter.dll`

### <a name="view-assembly-in-the-gac-cmd-line"></a>GAC でのアセンブリの表示 (cmd 行)

`C:> .gacutil.exe /l mfaadapter`

### <a name="register-your-provider-in-ad-fs"></a>AD FS にプロバイダーを登録する

1. `PS C:>$typeName = "MFAadapter.MyAdapter, MFAadapter, Version=1.0.0.1, Culture=neutral, PublicKeyToken=e675eb33c62805a0, processorArchitecture=MSIL”`

2. `PS C:>Register-AdfsAuthenticationProvider -TypeName $typeName -Name “MyMFAAdapter1”`

3. AD FS サービスを再起動します。

### <a name="create-the-authentication-policy-using-the-ad-fs-management-snap-in"></a>AD FS 管理スナップインを使用して認証ポリシーを作成する

1. [サーバーマネージャー**ツール**] メニューから AD FS 管理スナップインを開きます。

2. [**認証ポリシー**] をクリックします。

3. [ **Multi-Factor Authentication**で、[**グローバル設定**] の右側にある [**編集**] リンクをクリックします。

4. [**追加の認証方法の選択**] で、プロバイダーの adminname のチェックボックスをオンにします。 **[適用]** をクリックします。

5. アダプターを使用して MFA を呼び出す "トリガー" を提供するには、[場所] で、**エクストラネット**と**イントラネット**の両方を確認します (例)。 **[OK]** をクリックします。

### <a name="authenticate-with-mfa-using-your-adapter"></a>アダプターを使用して MFA で認証する

最後に、次の手順を実行してアダプターをテストします。

1. AD FS のグローバルプライマリ認証の種類が、エクストラネットとイントラネットの両方の**フォーム認証**として構成されていることを確認します (これにより、特定のユーザーとして認証が容易になります)。

    1. AD FS 管理スナップインの [**認証ポリシー**] の [**プライマリ認証**] 領域で、[**グローバル設定**] の横にある [**編集**] をクリックします。

        1. または、多要素ポリシー UI の [**プライマリ**] タブをクリックします。

2. **エクストラネット**と**イントラネット**の両方の認証方法で、**フォーム認証**が唯一のオプションとして選択されていることを確認します。 **[OK]** をクリックします。

3. IDP で開始されたサインオン html ページ (https:// <fsname> /adfs/ls/idpinitiatedsignon.htm) を開き、テスト環境で有効な AD ユーザーとしてサインインします。

4. プライマリ認証の資格情報を入力します。

5. [MFA フォーム] ページが表示され、チャレンジテキストの例が表示されます。

    1. 複数のアダプターが構成されている場合は、[MFA の選択] ページにフレンドリ名が表示されます。

MFA 認証ページで「adfabric」と入力すると、成功したサインインが表示されます。

![アダプターを使用したサインイン](media/ad-fs-build-custom-auth-method/Dn783423.630d8a91-3bfe-4cba-8acf-03eae21530ee(MSDN.10).jpg "アダプターを使用したサインイン")

![アダプターを使用したサインイン](media/ad-fs-build-custom-auth-method/Dn783423.c340fa73-f70f-4870-b8dd-07900fea4469(MSDN.10).jpg "アダプターを使用したサインイン")

## <a name="see-also"></a>参照

#### <a name="other-resources"></a>その他の参照情報

[追加の認証方法](/previous-versions/orphan-topics/ws.11/dn383648(v=ws.11)) 
[機密アプリケーションの追加 Multi-Factor Authentication によるリスク管理](/previous-versions/orphan-topics/ws.11/dn383648(v=ws.11))
