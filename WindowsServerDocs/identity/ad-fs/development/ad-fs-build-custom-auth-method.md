---
title: Windows Server AD FS のカスタム認証方法を構築します。
description: このシナリオでは、Windows server AD FS のカスタム認証方法を構築する方法について説明します。
author: billmath
ms.author: billmath
manager: daveba
ms.date: 05/23/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f28458ed9e781df6eca2478b02fb667d9240ca48
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445302"
---
# <a name="build-a-custom-authentication-method-for-ad-fs-in-windows-server"></a>Windows Server AD FS のカスタム認証方法を構築します。

このチュートリアルでは、Windows Server 2012 R2 で AD FS のカスタム認証メソッドを実装するための手順を提供します。 詳細については、次を参照してください。[追加の認証方法](https://msdn.microsoft.com/en-us/library/dn758113\(v=msdn.10\))します。


> [!WARNING]
> ここで作成できる例は、&nbsp;教育目的のみ。 &nbsp;これらの手順では、モデルの必須の要素を公開する最も単純で最低限の実装です。&nbsp;バック エンドの認証、エラー処理、または構成データはありません。 
> <P></P>



## <a name="setting-up-the-development-box"></a>開発ボックスの設定

このチュートリアルでは、Visual Studio 2012 を使用します。  Windows の .NET クラスを作成できる任意の開発環境では、プロジェクトをビルドすることができます。 プロジェクトは .NET 4.5 をターゲットする必要がありますので、 **BeginAuthentication**と**TryEndAuthentication**メソッドを使用して、型**System.Security.Claims.Claim**.NET の一部であります。フレームワーク バージョン 4.5.There では、プロジェクトに必要な 1 つの参照を示します。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Dll の参照</strong></p></td>
<td><p><strong>参照先</strong></p></td>
<td><p><strong>必要な</strong></p></td>
</tr>
<tr class="even">
<td><p>Microsoft.IdentityServer.Web.dll</p></td>
<td><p>AD FS がインストールされている Windows Server 2012 R2 サーバーで %windir%\ADFS dll にあります。</p>
<p></p>
<p>開発用コンピューターと明示的な参照をプロジェクトの作成には、この dll をコピーする必要があります。</p></td>
<td><p>IAuthenticationContext、IProofData を含むインターフェイスの種類</p></td>
</tr>
</tbody>
</table>


## <a name="create-the-provider"></a>プロバイダーを作成します。

1.  Visual Studio 2012 の場合。ファイルの選択\>新しい-\>プロジェクト.

2.  クラス ライブラリを選択し、.NET 4.5 を対象としていることを確認します。

    ![プロバイダーの作成](media/ad-fs-build-custom-auth-method/Dn783423.71a57ae1-d53d-462b-a846-5b3c02c7d3f2(MSDN.10).jpg "プロバイダーの作成")

3.  コピーを作成**Microsoft.IdentityServer.Web.dll** %windir% から\\ADFS、Windows Server 2012 R2 サーバーの AD FS がインストールされており、開発用コンピューターにプロジェクト フォルダーに貼り付けます。

4.  **ソリューション エクスプ ローラー**を右クリックして**参照**と**参照の追加.**

5.  ローカル コピーを参照**Microsoft.IdentityServer.Web.dll**と**追加しています.**

6.  クリックして**OK**新しい参照を確認します。

    ![プロバイダーの作成](media/ad-fs-build-custom-auth-method/Dn783423.f18df353-9259-4744-b4b6-dd780ce90951(MSDN.10).jpg "プロバイダーの作成")

    必要がありますように設定プロバイダーに必要な種類のすべてを解決します。 

7.  新しいクラスをプロジェクトに追加 (プロジェクトを右クリックして**追加します。クラス.** ) のような名前を付けますと**MyAdapter**、次に示す。

    ![プロバイダーの作成](media/ad-fs-build-custom-auth-method/Dn783423.6b6a7a8b-9d66-40c7-8a86-a2e3b9e14d09(MSDN.10).jpg "プロバイダーの作成")

8.  MyAdapter.cs 新しいファイルでは、次のように、既存のコードを置き換えます。

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

    F12 をできるようになりました (右クリック-定義へ移動) で IAuthenticationAdapter に必要なインターフェイス メンバーのセットを参照してください。 

    次に、これらの単純な実装を行うことができます。

9.  次のように、クラスの内容全体を置き換えます。

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

10. まだを構築する準備ができていない.移動する 2 つ以上のインターフェイスがあります。

    2 つのクラスをプロジェクトに追加します。 1 つは、メタデータ、およびプレゼンテーションのフォームのその他。  上記のクラスとしては、同じファイル内でこれらを追加できます。

        class MyMetadata : IAuthenticationAdapterMetadata
         {

         }

         class MyPresentationForm : IAdapterPresentationForm
         {

         }

11. 次に、それぞれの必須メンバーを追加することができます。最初に、(便利なインライン コメント) を使用したメタデータ

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
         /// to determine the best language\locale to display to the user.
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

         /// Returns an array indicating the type of claim that that the adapter uses to identify the user being authenticated.
         /// Note that although the property is an array, only the first element is currently used.
         /// MUST BE ONE OF THE FOLLOWING
         /// "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"
         /// "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"
         /// "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"
         /// "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid"
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

    次に、プレゼンテーションのフォーム:

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


~~~
     }
~~~

12. 'Todo' に注意してください、 **Resources.FormPageHtml**上の要素。 

   修正、ことを 1 分が 1 つ目のみましょう最終的な必要な戻り値のステートメントを追加、初期 MyAdapter クラスに、新たに実装された型に基づきます。  これを行うには、内の項目を追加*斜体*の下には、既存 IAuthenticationAdapter 実装。

       クラス MyAdapter:IAuthenticationAdapter     {     public IAuthenticationAdapterMetadata Metadata     {     //get { return new <instance of IAuthenticationAdapterMetadata derived class>; }     get { return new MyMetadata(); }     }

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

13. これでリソース ファイルの html フラグメントを含むです。 次のコンテンツと共にプロジェクト フォルダーに新しいテキスト ファイルを作成します。

       <div id="loginArea">
        <form method="post" id="loginForm" >
        <!-- These inputs are required by the presentation framework. Do not modify or remove -->
        <input id="authMethod" type="hidden" name="AuthMethod" value="%AuthMethod%"/>
        <input id="context" type="hidden" name="Context" value="%Context%"/>
        <!-- End inputs are required by the presentation framework. -->
        <p id="pageIntroductionText">このコンテンツは、MFA サンプル アダプターによって提供されます。 チャレンジの入力を記載する必要があります。</p>
        <label for="challengeQuestionInput" class="block">質問のテキスト</label>
        <input id="challengeQuestionInput" name="ChallengeQuestionAnswer" type="text" value="" class="text" placeholder="Answer placeholder" />
        <div id="submissionArea" class="submitMargin">
        <input id="submitButton" type="submit" name="Submit" value="Submit" onclick="return AuthPage.submitAnswer()"/>
        </div>
        </form>
        <div id="intro" class="groupMargin">
        <p id="supportEmail">サポート情報</p>
        </div>
        <script type="text/javascript" language="JavaScript">
        //<![CDATA[
        function AuthPage() { }
        AuthPage.submitAnswer = function () { return true; };
        //]]>
        </script></div>

14. 次に、選択**プロジェクト-\>コンポーネントの追加.リソース**ファイルを開き、ファイルの名前**リソース**、 をクリック**追加。**

   ![プロバイダーの作成](media/ad-fs-build-custom-auth-method/Dn783423.3369ad8f-f65f-4f36-a6d5-6a3edbc1911a(MSDN.10).jpg "プロバイダーの作成")

15. 次に、 **Resources.resx**ファイルで、**リソースの追加.既存のファイル追加**します。  移動します (html フラグメントを含む)、テキスト ファイルの上に保存します。

   GetFormHtml コードは、新しいリソースの名前が正しく解決後に、リソース自体の名前のリソース ファイル (.resx ファイル) 名のプレフィックスを確認します。

       public string GetFormHtml(int lcid)    {     string htmlTemplate = Resources.MfaFormHtml; //Resxfilename.resourcename     return htmlTemplate;    }

   ビルドできるようになりましたにします。

## <a name="build-the-adapter"></a>アダプターをビルドします。

アダプターは、Windows で GAC にインストールできる厳密な名前付きの .NET アセンブリに組み込む必要があります。  Visual Studio プロジェクトにそのために、次の手順を行います。

1.  ソリューション エクスプ ローラーでプロジェクト名を右クリックし、をクリックして**プロパティ**します。

2.  **署名**] タブで、チェック**アセンブリに署名**選択 **\<新規.\>**  [**厳密な名前キー ファイルを選択します。** キー ファイル名とパスワードを入力し、クリックして**OK**します。  確認してください**アセンブリに署名**がオンになってと**遅延署名のみ**がオフになっています。  プロパティ**署名**ページは、次のようになります。

    ![プロバイダーの構築](media/ad-fs-build-custom-auth-method/Dn783423.0b1a1db2-d64e-4bb8-8c01-ef34296a2668(MSDN.10).jpg "プロバイダーの構築")

3.  ソリューションをビルドします。

## <a name="deploy-the-adapter-to-your-ad-fs-test-machine"></a>AD FS テスト対象のコンピューターに、アダプターを展開します。

外部プロバイダーは、AD FS によって呼び出されることができます、前に、システムに登録する必要があります。  アダプター プロバイダーは、GAC にインストールを含め、必要なインストール アクションを実行するインストーラーを提供する必要があり、インストーラーは、AD FS で登録をサポートする必要があります。  行われていない場合、管理者は、次の Windows PowerShell の手順を実行する必要があります。  次の手順は、テストとデバッグを有効にする、ラボで使用できます。

### <a name="prepare-the-test-ad-fs-machine"></a>AD FS テスト マシンを準備します。

ファイルをコピーし、GAC に追加します。

1.  Windows Server 2012 R2 コンピューターまたは仮想マシンがあることを確認します。

2.  AD FS 役割サービスをインストールし、少なくとも 1 つのノードのファームを構成します。

    ラボ環境でのフェデレーション サーバーをセットアップする詳細な手順は、次を参照してください。、 [Windows Server 2012 R2 AD FS 展開ガイド](https://msdn.microsoft.com/en-us/library/dn486820\(v=msdn.10\))します。

3.  Gacutil.exe ツールをサーバーにコピーします。

    見つかる Gacutil.exe **%homedrive%\\Program Files (x86)\\Microsoft Sdk\\Windows\\v8.0A\\bin\\NETFX 4.0 ツール\\** Windows 8 コンピューターでします。  必要があります、 **gacutil.exe**ファイル自体だけでなく**1033**、 **EN-US**、およびその他のローカライズされたリソース下のフォルダー、 **NETFX 4.0 ツール**場所。

4.  プロバイダー ファイルのコピー (1 つまたは複数の厳密な名前で署名済み .dll ファイル) と同じフォルダー場所に**gacutil.exe** (場所は利便性)

5.  .Dll ファイルをファーム内の各 AD FS フェデレーション サーバーの GAC に追加します。

    例: では、コマンド ライン ツール GACutil.exe を使用して、dll を GAC に追加します。 `C:\>.\gacutil.exe /if .\<yourdllname>.dll`

    GAC に結果として得られるエントリを表示します。`C:\>.\gacutil.exe /l <yourassemblyname>`

6.  

### <a name="register-your-provider-in-ad-fs"></a>AD FS では、プロバイダーを登録します。

フェデレーション サーバーで Windows PowerShell コマンド ウィンドウを開き、上記の前提条件が満たされると、次のコマンドを入力します (Windows Internal Database を使用するフェデレーション サーバー ファームを使用している場合は、実行することする必要がありますこれらのコマンドでに注意してください、プライマリ フェデレーション サーバー ファームの):

1.  `Register-AdfsAuthenticationProvider –TypeName YourTypeName –Name “AnyNameYouWish” [–ConfigurationFilePath (optional)]`

    場所 YourTypeName は、.NET の厳密な型名を示します。"YourDefaultNamespace.YourIAuthenticationAdapterImplementationClassName、アセンブリ名、バージョン YourAssemblyVersion、Culture = neutral, PublicKeyToken = YourPublicKeyTokenValue、processorArchitecture = MSIL を ="

    これにより、上記の AnyNameYouWish として指定した名前の AD FS で、外部プロバイダーが登録されます。

2.  (たとえば Windows サービス スナップインを使用)、AD FS サービスを再起動します。

3.  次のコマンドを実行します:`Get-AdfsAuthenticationProvider`します。

    ご利用のプロバイダーが、プロバイダーの 1 つとして、システムで表示されます。

    以下に例を示します。

        PS C:\>$typeName = "MFAadapter.MyAdapter, MFAadapter, Version=1.0.0.0, Culture=neutral, PublicKeyToken=e675eb33c62805a0, processorArchitecture=MSIL”
        PS C:\>Register-AdfsAuthenticationProvider -TypeName $typeName -Name “MyMFAAdapter”
        PS C:\>net stop adfssrv
        PS C:\>net start adfssrv

    デバイス登録サービスが、AD FS 環境で有効にした場合、次も実行します。  `PS C:\>net start drs`

    登録済みのプロバイダーを確認するには、次のコマンドを使用:`PS C:\>Get-AdfsAuthenticationProvider`します。

    ご利用のプロバイダーが、プロバイダーの 1 つとして、システムで表示されます。

### <a name="create-the-ad-fs-authentication-policy-that-invokes-your-adapter"></a>使用してアダプターを呼び出すの AD FS 認証ポリシーを作成します。

#### <a name="create-the-authentication-policy-using-the-ad-fs-management-snap-in"></a>AD FS 管理スナップインを使用して、認証ポリシーを作成します。

1.  AD FS 管理スナップインを開きます (サーバー マネージャーから**ツール**メニュー)。

2.  クリックして**認証ポリシー**します。

3.  中央のウィンドウで [ **Multi-factor Authentication**、] をクリックして、**編集**の右側にあるリンク**グローバル設定**します。

4.  **追加の認証方法を選択します。** 、ページの下部にあるチェック ボックスをオンのプロバイダーの AdminName します。 **[適用]** をクリックします。

5.  下に、アダプターを使用して、MFA を起動する「トリガー」を提供する**場所**両方をチェック**エクストラネット**と**イントラネット**など。 **[OK]** をクリックします。 (トリガーを構成する証明書利用者ごとには、パーティの下に"Windows PowerShell を使用して認証ポリシーの作成 を参照してください)。

6.  次のコマンドを使用して結果を確認します。

    まずを使用して`Get-AdfsGlobalAuthenticationPolicy`します。 AdditionalAuthenticationProvider 値の 1 つとしては、プロバイダー名が表示されます。

    使用して`Get-AdfsAdditionalAuthenticationRule`します。 エクストラネットおよびイントラネット管理者 UI で、ポリシーの選択の結果として構成されている規則が表示されます。

#### <a name="create-the-authentication-policy-using-windows-powershell"></a>Windows PowerShell を使用して、認証ポリシーを作成します。

1.  最初に、プロバイダーは、グローバル ポリシーを有効にします。

    `PS C:\>Set-AdfsGlobalAuthenticationPolicy -AdditionalAuthenticationProvider “YourAuthProviderName”`


~~~
> [!NOTE]
> Note that the value provided for the AdditionalAuthenticationProvider parameter corresponds to the value you provided for the “Name” parameter in the Register-AdfsAuthenticationProvider cmdlet above and to the “Name” property from Get-AdfsAuthenticationProvider cmdlet output. 
> <P></P>


Example:`PS C:\>Set-AdfsGlobalAuthenticationPolicy –AdditionalAuthenticationProvider “MyMFAAdapter”`
~~~

2. 次に、MFA をトリガーするグローバルまたは証明書利用者パーティ固有の規則を構成します。

   例 1: MFA を要求する要求を外部のグローバル ルールを作成します。`PS C:\>Set-AdfsAdditionalAuthenticationRule –AdditionalAuthenticationRules 'c:[type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", value == "false"] => issue(type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "http://schemas.microsoft.com/claims/multipleauthn" );'`

   例 2: MFA を作成する、特定証明書利用者への外部要求に対して MFA を要求する規則がパーティです。  (個々 のプロバイダーを Windows Server 2012 R2 で AD FS での個々 の証明書利用コンポーネントに接続できないことに注意してください。)

       PS C:\>$rp = Get-AdfsRelyingPartyTrust –Name <Relying Party Name>
       PS C:\>Set-AdfsRelyingPartyTrust –TargetRelyingParty $rp –AdditionalAuthenticationRules 'c:[type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", value == "false"] => issue(type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "http://schemas.microsoft.com/claims/multipleauthn" );'

### <a name="authenticate-with-mfa-using-your-adapter"></a>アダプターを使用して MFA を使用した認証します。

最後に、アダプターをテストするのには、次の手順に従います。

1.  AD FS グローバル プライマリ認証の種類がエクストラネットとイントラネット (これにより、デモ、特定のユーザーとして認証しやすい) の両方のフォーム認証として構成されていることを確認します。

    1.  AD FS スナップインで、**認証ポリシー**の**プライマリ認証**領域で、をクリックして**編集**横に**グローバル設定**.

        1.  クリックするだけですか、**プライマリ**タブから、**多要素ポリシー** UI。

2.  確認**フォーム認証**が唯一のオプションをエクストラネットおよびイントラネットの認証方法の両方をチェックします。  **[OK]** をクリックします。

3.  開く、IDP 開始サインオン html ページ (https://\<fsname\>/adfs/ls/idpinitiatedsignon.htm) し、テスト環境で有効な AD のユーザーとしてサインインします。

4.  プライマリ認証の資格情報を入力します。

5.  チャレンジの質問の例を含むページが表示される MFA フォームが表示されます。 

    構成されているアダプターの 1 つ以上の場合は、上記のフレンドリ名で MFA の選択 ページが表示されます。

    ![アダプターを使用した認証](media/ad-fs-build-custom-auth-method/Dn783423.c98d2712-cbd3-4cb9-ac03-2838b81c4f63(MSDN.10).jpg "アダプターを使用した認証")

    ![アダプターを使用した認証](media/ad-fs-build-custom-auth-method/Dn783423.fd3aefc0-ef6c-4a8c-a737-4914c78ff2d2(MSDN.10).jpg "アダプターを使用した認証")

インターフェイスの実装作業があるようになりましたし、モデルのしくみの知識があること。 Trym として、TryEndAuthentication と同様に、BeginAuthentication でブレークポイントを設定する例を追加できます。  BeginAuthentication の実行方法、ユーザーが MFA フォームを最初に入ると、フォームの各送信で TryEndAuthentication がトリガーされますが、注目してください。

## <a name="update-the-adapter-for-successful-authentication"></a>成功した認証用のアダプターを更新します。

待機 – アダプターの使用例を認証することができませんが、\!  これは、ため、TryEndAuthentication の null を返します、コードでは nothing です。

上記の手順を完了するは、アダプターの基本実装を作成し、AD FS サーバーに追加しました。  MFA のフォーム ページを表示できますが、まだするはまだ組み入れ、適切なロジック TryEndAuthentication 実装のため、認証することはできません。  追加してみましょう。

TryEndAuthentication 実装を思い出してください。

    public IAdapterPresentation TryEndAuthentication(IAuthenticationContext authContext, IProofData proofData, HttpListenerRequest request, out Claim[] outgoingClaims)
     {
     //return new instance of IAdapterPresentationForm derived class
     outgoingClaims = new Claim[0];
     return new MyPresentationForm();

     }

みましょう MyPresentationForm() を常に戻さないために、それを更新します。  このクラス内で 1 つの単純なユーティリティ メソッドを作成できます。

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

その後、次に示すよう TryEndAuthentication を更新します。

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

今すぐテストをボックスに、アダプターを更新する必要があります。  最初、AD FS のポリシーからの登録を解除 AD FS からを元に戻すと、AD FS を再起動し、.dll を GAC から削除し、新しい .dll を GAC に追加し、AD FS で登録、AD FS を再起動して AD FS のポリシーを再構成します。

## <a name="deploy-and-configure-the-updated-adapter-on-your-test-ad-fs-machine"></a>展開して、テスト コンピューターの AD FS に対して更新されたアダプターを構成します。

### <a name="clear-ad-fs-policy"></a>AD FS のポリシーをクリアします。

チェック ボックスをオフすべて MFA は、MFA の ui で、次に示すチェック ボックスをオンに関連し、[ok] をクリックします。

![ポリシーをオフに](media/ad-fs-build-custom-auth-method/Dn783423.c111b4e7-5b05-413c-8b0f-222a0e91ac1f(MSDN.10).jpg "ポリシーのクリア")

### <a name="unregister-provider-windows-powershell"></a>プロバイダー (Windows PowerShell) の登録を解除します。

`PS C:\> Unregister-AdfsAuthenticationProvider –Name “YourAuthProviderName”`

例:`PS C:\> Unregister-AdfsAuthenticationProvider –Name “MyMFAAdapter”`

Register-adfsauthenticationprovider コマンドレットに指定した値を"Name"は"Name"と同じ値を渡すことに注意してください。  Get AdfsAuthenticationProvider から出力される"Name"プロパティもです。

プロバイダーの登録を解除する前に削除することする必要があります、プロバイダー (または AD FS 管理スナップインで確認したチェック ボックスをオフにして Windows PowerShell を使用しています。) AdfsGlobalAuthenticationPolicy からに注意してください。

この操作の後、AD FS サービスを再起動する必要がありますに注意してください。

### <a name="remove-assembly-from-gac"></a>アセンブリを GAC から削除します。

1.  最初に、エントリの完全修飾の厳密な名前を検索するのに次のコマンドを使用します。`C:\>.\gacutil.exe /l <yourAdapterAssemblyName>`

    例:`C:\>.\gacutil.exe /l mfaadapter`

2.  次に、次のコマンドを使用して、GAC から削除します。`.\gacutil /u “<output from the above command>”`

    例:`C:\>.\gacutil /u “mfaadapter, Version=1.0.0.0, Culture=neutral, PublicKeyToken=e675eb33c62805a0, processorArchitecture=MSIL”`

### <a name="add-the-updated-assembly-to-gac"></a>更新されたアセンブリを GAC に追加します。

更新された .dll をローカルで最初に貼り付けることを確認します。 `C:\>.\gacutil.exe /if .\MFAAdapter.dll`

### <a name="view-assembly-in-the-gac-cmd-line"></a>ビュー アセンブリを GAC (コマンドライン)

`C:\> .\gacutil.exe /l mfaadapter`

### <a name="register-your-provider-in-ad-fs"></a>AD FS では、プロバイダーを登録します。

1.  `PS C:\>$typeName = "MFAadapter.MyAdapter, MFAadapter, Version=1.0.0.1, Culture=neutral, PublicKeyToken=e675eb33c62805a0, processorArchitecture=MSIL”`

2.  `PS C:\>Register-AdfsAuthenticationProvider -TypeName $typeName -Name “MyMFAAdapter1”`

3.  AD FS サービスを再起動します。

### <a name="create-the-authentication-policy-using-the-ad-fs-management-snap-in"></a>AD FS 管理スナップインを使用して、認証ポリシーを作成します。

1.  AD FS 管理スナップインを開きます (サーバー マネージャーから**ツール**メニュー)。

2.  クリックして**認証ポリシー**します。

3.  [ **Multi-factor Authentication**、] をクリックして、**編集**の右側にあるリンク**グローバル設定**します。

4.  **追加の認証方法を選択して**プロバイダーの AdminName のチェック ボックスをオンします。 **[適用]** をクリックします。

5.  「トリガー」を使用してアダプターを使用して、MFA を呼び出すために、場所 両方をチェック**エクストラネット**と**イントラネット**など。 **[OK]** をクリックします。

### <a name="authenticate-with-mfa-using-your-adapter"></a>アダプターを使用して MFA を使用した認証します。

最後に、アダプターをテストするのには、次の手順に従います。

1.  AD FS グローバル プライマリ認証の種類として構成されていることを確認**フォーム認証**エクストラネットとイントラネット (この簡単に特定のユーザーとして認証) の両方にします。

    1.  AD FS 管理スナップインで、**認証ポリシー**で、**プライマリ認証**領域で、をクリックして**編集**横に**のグローバル設定**.

        1.  クリックするだけですか、**プライマリ**多要素ポリシーの UI からタブ。

2.  確認**フォーム認証**が唯一のオプションを両方のチェック、**エクストラネット**と**イントラネット**認証方法。  **[OK]** をクリックします。

3.  開く、IDP 開始サインオン html ページ (https://\<fsname\>/adfs/ls/idpinitiatedsignon.htm) し、テスト環境で有効な AD のユーザーとしてサインインします。

4.  プライマリ認証の資格情報を入力します。

5.  チャレンジのテキストの例を含むページが表示される MFA フォームが表示されます。

    1.  複数のアダプターを構成した場合にフレンドリ名で MFA の選択 ページが表示されます。

MFA 認証ページ"adfabric"を入力するときに、成功したサインインが表示されます。

![アダプターを使用してサインイン](media/ad-fs-build-custom-auth-method/Dn783423.630d8a91-3bfe-4cba-8acf-03eae21530ee(MSDN.10).jpg "アダプターを使用してサインイン")

![アダプターを使用してサインイン](media/ad-fs-build-custom-auth-method/Dn783423.c340fa73-f70f-4870-b8dd-07900fea4469(MSDN.10).jpg "アダプターを使用してサインイン")

## <a name="see-also"></a>関連項目

#### <a name="other-resources"></a>その他のリソース

[追加の認証方法](https://msdn.microsoft.com/en-us/library/dn758113\(v=msdn.10\))  
[機密性の高いアプリケーションの追加の多要素認証によるリスクを管理します。](https://msdn.microsoft.com/en-us/library/dn280949\(v=msdn.10\))

