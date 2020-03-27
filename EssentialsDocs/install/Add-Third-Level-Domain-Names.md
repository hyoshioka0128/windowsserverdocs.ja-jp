---
title: 第 3 レベル ドメイン名の追加
description: Windows Server Essentials の使用方法について説明します。
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e5b4a362-1881-4024-ae4e-cc3b05e50103
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 5608fb5417b9e958b45d150879daccc3b7767e59
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80310235"
---
# <a name="add-third-level-domain-names"></a>第 3 レベル ドメイン名の追加

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

ユーザーが Set Up Domain Name ウィザードで第 3 レベル ドメイン名を要求する機能を追加できます。 これには、オペレーティング システムのドメイン マネージャーによって使用されるコード アセンブリを作成してインストールします。  
  
## <a name="create-a-provider-of-third-level-domain-names"></a>第 3 レベル ドメイン名のプロバイダーの作成  
 第 3 レベル ドメイン名を使用できるようにするには、ドメイン名をウィザードに提供するコード アセンブリを作成してインストールします。 これを行うには、次のタスクを完了します。  
  
-   [IDomainSignupProvider インターフェイスの実装をアセンブリに追加します。](Add-Third-Level-Domain-Names.md#BKMK_DomainSignup)  
  
-   [IDomainMaintenanceProvider インターフェイスの実装をアセンブリに追加します。](Add-Third-Level-Domain-Names.md#BKMK_DomainMaintenance)  
  
-   [Authenticode 署名を使用してアセンブリに署名する](Add-Third-Level-Domain-Names.md#BKMK_SignAssembly)  
  
-   [参照コンピューターにアセンブリをインストールする](Add-Third-Level-Domain-Names.md#BKMK_InstallAssembly)  
  
-   [Windows Server ドメインネーム管理サービスを再起動する](Add-Third-Level-Domain-Names.md#BKMK_RestartService)  
  
###  <a name="add-an-implementation-of-the-idomainsignupprovider-interface-to-the-assembly"></a><a name="BKMK_DomainSignup"></a>IDomainSignupProvider インターフェイスの実装をアセンブリに追加します。  
 ドメイン サービスをウィザードに追加するには、IDomainSignupProvider インターフェイスが使用されます。  
  
##### <a name="to-add-the-idomainsignupprovider-code-to-the-assembly"></a>IDomainSignupProvider コードをアセンブリに追加するには  
  
1.  **[スタート]** メニューのプログラムを右クリックし、 **[管理者として実行]** を選択して、Visual Studio 2008 を管理者として開きます。  
  
2.  **[ファイル]** をクリックし、 **[新規作成]** をクリックし、 **[プロジェクト]** をクリックします。  
  
3.  **[新しいプロジェクト]** ダイアログ ボックスで、 **[Visual C#]** 、次に **[クラス ライブラリ]** をクリックし、ソリューションの名前を入力して、 **[OK]** をクリックします。  
  
4.  Class1.cs ファイルの名前を変更します。 たとえば、MyDomainNameProvider.cs  
  
5.  Wssg.Web.DomainManagerObjectModel.dll、CertManaged.dll、WssgCertMgmt.dll、WssgCommon.dll ファイルへの参照を追加します。  
  
6.  ステートメントを使用して以下を追加します。  
  
    ```c#  
  
    using System.Collections.ObjectModel;  
    using System.Net;  
    using System.Net.Sockets;  
    using Microsoft.WindowsServerSolutions.Certificates;  
    using Microsoft.WindowsServerSolutions.CertificateManagement;  
    using Microsoft.WindowsServerSolutions.Common;  
    using Microsoft.Win32;  
    ```  
  
7.  次の例に合わせて、名前空間とクラス ヘッダーを変更します。  
  
    ```c#  
    namespace Microsoft.WindowsServerSolutions.RemoteAccess.Domains  
    {  
        public class MyDomainNameProvider : IDomainSignupProvider  
        {  
        }  
    }  
    ```  
  
8.  Initialize メソッドと必要な変数をクラスに追加します。これにより、ウィザードで示されているサービスを定義します。  
  
    > [!NOTE]
    >  Initialize メソッドは、ドメイン プロバイダーの識別子を定義します。識別子は一意でなければなりません。 通常の方法では、識別子として GUID を定義します。 GUID の作成の詳細については、「 [Guid の作成 (guidgen.exe)](https://go.microsoft.com/fwlink/?LinkId=116098)」を参照してください。  
  
     次のコード例は、Initialize メソッドを示します。  
  
    ```c#  
  
    static readonly Guid MyID = new Guid("8C999DF5-696A-47af-822D-94F1673D3397");  
    public Guid ID { get { return MyID; } }  
    public string Name { get { return "My Provider"; } }  
    List<Offering> offerings = new List<Offering>();  
  
    public void Initialize(DomainProviderSettings config)  
    {  
       var offer1 = new Offering()  
       {  
          Description = "My Domain Provider",  
          Name = "Offering 1",  
          ProviderID = ID,  
          MoreInfoUrl = new Uri("http://www.contoso.com"),  
          MembershipServiceName = "My Membership",  
          EulaUrl = new Uri("http://www.contoso.com"),  
       };  
  
       this.offerings.Add(offer1);  
       RegistryKey key =   
          Registry.LocalMachine.CreateSubKey(@"Software\Microsoft\Windows Server\Domain Manager\Settings");  
       key.Close();  
    }  
    ```  
  
9. 前の手順で初期化されたサービスの一覧を返す、GetOfferings メソッドを追加します。 次のコード例は、GetOfferings メソッドを示します。  
  
    ```c#  
  
    public ReadOnlyCollection<Offering> GetOfferings()  
    {  
       return this.offerings.AsReadOnly();  
    }  
    ```  
  
10. リストからサービスを返す FindOfferingForDomain メソッドを追加します。 次のコード例は、FindOfferingForDomain メソッドを示します。  
  
    ```  
  
    public Offering FindOfferingForDomain(string domain)  
    {  
       // Return the offering that has the domain name.  
       return offerings[0];  
    }  
  
    ```  
  
11. サービスにアクセスするために必要な資格情報を定義する、SetCredentials メソッドを追加します。 次のコード例は、SetCredentials メソッドを示します。  
  
    ```c#  
  
    private string currentUser { get; set; }  
    private string currentPassword { get; set; }  
  
    public bool SetCredentials(DomainNameRequest request,   
       DomainProviderCredentials credentials, bool validate)  
    {  
       currentUser = credentials.UserName;  
       currentPassword = credentials.Password;  
       if (validate)  
       {  
          return ValidateCredentials();  
       }  
  
       return true;  
    }  
    ```  
  
12. SetCredentials で定義されている資格情報を検証する、ValidateCredentials メソッドを追加します。 次のコード例は、ValidateCredentials メソッドを示します。  
  
    ```c#  
  
    public static readonly string offerUser = "user1@contoso.com";  
    public static readonly string offerPassword = "password1";  
  
    public bool ValidateCredentials()  
    {  
       if (IsUser())  
          return string.Equals(currentPassword, offerPassword);  
       else  
          return false;  
    }   
  
    private bool IsUser()  
    {  
       return string.Equals(currentUser, offerUser, StringComparison.OrdinalIgnoreCase);  
    }  
    ```  
  
13. 要求で指定されたサービスによってサポートされるルート ドメイン名の一覧を返す、GetAvailableDomainRoots メソッドを追加します。 このルート ドメイン名の一覧を空にすることはできません。 次のコード例は、GetAvailableDomainRoots メソッドを示します。  
  
    ```c#  
  
    public ReadOnlyCollection<string> GetAvailableDomainRoots(DomainNameRequest request)  
    {  
       List<string> list = new List<string>();  
       list.Add("domain1.com");  
       list.Add("domain1.org");  
  
       return list.AsReadOnly();  
    }  
    ```  
  
14. 現在のサービスを基準として、現在のユーザーが既に所有しているドメイン名の一覧を返す、GetUserDomainNames メソッドを追加します。 この一覧は空にすることができます。 次のコード例は、GetUserDomainNames メソッドを示します。  
  
    ```c#  
  
    public static readonly string AvailableDomain1 = "available.domain1.com",  
       AvailableDomain2 = "available.domain2.com";  
    public static readonly string OccupiedDomain1 = "occupied.domain1.com",  
       OccupiedDomain2 = "occupied.domain2.com";  
  
    public ReadOnlyCollection<string> GetUserDomainNames(DomainNameRequest request)  
    {  
       var userDomains = new List<string>();  
       userDomains.Add(OccupiedDomain1);  
       userDomains.Add(AvailableDomain1);  
  
       return userDomains.AsReadOnly();  
    }  
    ```  
  
15. 指定されたサービスが許可する最大ドメイン数を返す、GetUserDomainQuota メソッドを追加します。 最大数が適用されない場合、このメソッドは 0 を返します。 次のコード例は、GetUserDomainQuota メソッドを示します。  
  
    ```c#  
  
    public int GetUserDomainQuota(DomainNameRequest request)  
    {  
       return 0;  
    }  
    ```  
  
16. 要求されたドメイン名の可用性をチェックし、提案の一覧を返すことができる、CheckDomainAvailability メソッドを追加します。 次のコード例は、CheckDomainAvailability メソッドを示します。  
  
    ```c#  
  
    public bool CheckDomainAvailability(DomainNameRequest request,   
       out ReadOnlyCollection<string> suggestions)  
    {  
       suggestions = null;  
  
       return true;  
    }  
    ```  
  
17. 要求されたドメイン名を確定する、CommitDomain メソッドを追加します。 このメソッドが正常に完了すると、ドメイン名がユーザー アカウントに関連付けられ、状態が FullyOperational の場合、証明書を取得するためにメンテナンス プロバイダーが直ちに呼び出され、プロバイダーとサービスがアクティブになります。 次のコード例は、CommitDomain メソッドを示します。  
  
    ```c#  
  
    public DomainStatus CommitDomain(DomainNameRequest request)  
    {              
       ReadOnlyCollection<string> suggestions;  
       if (!CheckDomainAvailability(request, out suggestions))  
       {  
          throw new DomainException(FailureReason.InvalidDomainName, null, null);  
       }  
  
       return DomainStatus.Ready;  
    }  
    ```  
  
18. ユーザーがドメイン名の解放を希望していることをプロバイダーに知らせる、ReleaseDomain メソッドを追加します。 次のコード例は、ReleaseDomain メソッドを示します。  
  
    ```c#  
  
    public bool ReleaseDomain(DomainNameRequest request)  
    {  
       return true;  
    }  
    ```  
  
19. ドメイン サインアップ ワークフローのランディング ページの URL を返す、GetProviderLandingUrl メソッドを追加します。 次のコード例は、GetProviderLandingUrl メソッドを示します。  
  
    ```c#  
  
    public Url GetProviderLandingUrl(DomainNameRequest request)  
    {  
       return new Url("www.contoso.com");  
    }  
    ```  
  
20. ドメイン保守タスクに使用される IDomainMaintenanceProvider のインスタンスを返す、GetDomainMaintenanceProvider メソッドを追加します。 このメソッドは、CommitDomain メソッドが成功した後、およびドメイン マネージャーの起動時に呼び出されます。 次のコード例は、GetDomainMaintenanceProvider メソッドを示します。  
  
    ```c#  
  
    public IDomainMaintenanceProvider GetDomainMaintenanceProvider()  
    {  
       return new MyDomainMaintenanceProvider();  
    }  
    ```  
  
21. プロジェクトを保存したら、次の手順でプロジェクトへの追加を行うため、プロジェクトを閉じないでください。 次の手順を完了するまでプロジェクトをビルドすることはできません。  
  
###  <a name="add-an-implementation-of-the-idomainmaintenanceprovider-interface-to-the-assembly"></a><a name="BKMK_DomainMaintenance"></a>IDomainMaintenanceProvider インターフェイスの実装をアセンブリに追加します。  
 作成した後にドメインを維持するには、IDomainMaintenanceProvider が使用されます。  
  
##### <a name="to-add-the-idomainmaintenanceprovider-code-to-the-assembly"></a>IDomainMaintenanceProvider コードをアセンブリに追加するには  
  
1.  ドメイン メンテナンス プロバイダーのクラス ヘッダーを追加します。 プロバイダーに対して定義した名前が、前に定義した GetDomainMaintenanceProvider メソッド内の名前と一致することを確認します。  
  
    ```c#  
  
    public class MyDomainMaintenanceProvider : IDomainMaintenanceProvider  
    {  
    }  
    ```  
  
2.  アクティブなプロバイダーを設定する、Activate メソッドを追加します。 次のコード例は、Activate メソッドを示します。  
  
    ```c#  
  
    string DomainName { get; set; }  
    protected DomainProviderSettings Settings { get; set; }  
  
    public void Activate(DomainProviderSettings settings,   
       DomainNameConfiguration config, DomainProviderCredentials credentials)  
    {  
       Settings = settings;  
       SetCredentials(credentials);  
       DomainName = config.AutoConfiguredAnywhereAccessFullName.Punycode;  
    }  
    ```  
  
3.  すべてのアクションを無効化するのに使用する、Deactivate メソッドを追加します。 次のコード例は、Deactivate メソッドを示します。  
  
    ```  
  
    public void Deactivate()  
    {  
       //Deactivate all actions  
    }  
  
    ```  
  
4.  ユーザーの資格情報を更新する、SetCredentials メソッドを追加します。 たとえば、このメソッドは、有効でなくなった資格情報を更新するために呼び出すことができます。 次のコード例は、SetCredentials メソッドを示します。  
  
    ```c#  
  
    protected DomainProviderCredentials Credentials { get; set; }  
  
    public bool SetCredentials(DomainProviderCredentials credentials)  
    {  
       this.Credentials = credentials;  
  
       return true;  
    }  
    ```  
  
5.  指定された資格情報を検証する、ValidateCredentials メソッドを追加します。 次のコード例は、ValidateCredentials メソッドを示します。  
  
    ```c#  
  
    public static readonly string offerUser = "user1@contoso.com";  
    public static readonly string offerPassword = "password1";  
  
    public bool ValidateCredentials()  
    {  
       if (string.Equals(this.Credentials.UserName,   
          offerUser,   
          StringComparison.OrdinalIgnoreCase) &&   
             string.Equals(this.Credentials.Password, offerPassword))  
          return true;  
  
       return false;  
    }  
    ```  
  
6.  サーバーの外部 IP アドレスを返す、GetPublicAddress メソッドを追加します。 次のコード例は、GetPublicAddress メソッドを示します。  
  
    ```c#  
  
    public IPAddress GetPublicIPAddress()  
    {  
       string PublicIP = "0.0.0.0";  
       using (RegistryKey key = ProductInfo.RegKey.OpenSubKey("Domain Manager\\Settings", true))  
       {  
          PublicIP = (key == null) ? "0.0.0.0" : key.GetValue("PublicIP", "0.0.0.0").ToString();  
       }  
       IPAddress ip = IPAddress.Parse(PublicIP);  
  
       if (PublicIP == "0.0.0.0")  
       {  
          string strHostName = Dns.GetHostName();  
          IPHostEntry ipEntry = Dns.GetHostEntry(strHostName);  
  
          IPAddress[] addr = ipEntry.AddressList;  
          foreach (IPAddress add in addr)  
          {  
             if (add.AddressFamily == AddressFamily.InterNetwork)  
             {  
                return add;  
             }  
          }  
       }  
       else  
       {  
          return IPAddress.Parse(PublicIP);  
       }  
  
       return null;    
    }  
    ```  
  
7.  現在構成されているドメイン名の証明書要求を送信する、SubmitCertificateRequest メソッドを追加します。  
  
    ```c#  
  
    string cert=null;  
  
    public void SubmitCertificateRequest(string certificateRequest)  
    {  
       cert = CertManaged.SubmitRequest(certificateRequest, CertCommon.CAServerFQDN + "\\" +      
          CertCommon.CAName,   
          Microsoft.WindowsServerSolutions.CertificateManagement.CRFlags.Base64Header,   
          CertCommon.CATemplate,   
          EncodingFlags.Base64);  
    }  
    ```  
  
8.  ドメインの状態が FullyOperational の場合に証明書応答を返す、GetCertificateResponse メソッドを追加します。 このメソッドは、新しい証明書要求と証明書の更新要求の両方に対して呼び出されます。 次のコード例は、GetCertificateResponse メソッドを示します。  
  
    ```c#  
  
    public string GetCertificateResponse(bool renew)  
    {  
       return cert;  
    }  
    ```  
  
9. 証明書の更新を処理する、SubmitRenewCertificateRequest メソッドを追加します。 次のコード例は、SubmitRenewCertificateRequest メソッドを示します。  
  
    ```c#  
  
    public void SubmitRenewCertificateRequest()  
    {  
       // Add certificate renewal code   
    }  
    ```  
  
10. プロバイダーによって保存された DNS レコードを更新する、UpdateDNSRecords メソッドを追加します。 次のコード例は、UpdateDNS メソッドを示します。  
  
    ```c#  
  
    public bool UpdateDnsRecords(IList<DnsRecord> records)  
    {  
       string UpdateDNS = "true";  
       using (RegistryKey key = ProductInfo.RegKey.OpenSubKey("Domain Manager\\Settings", true))  
       {  
          UpdateDNS = (key == null) ? "true" : key.GetValue("UpdateDNS", "true").ToString();  
       }  
  
       return UpdateDNS == "true";  
    }  
  
    ```  
  
11. バックエンド サービスへの接続を確立しようとする、TestConnection メソッドを追加します。 このメソッドに認証が必要な場合は、適切な例外をスローする必要があります。 次のコード例は、TestConnection メソッドを示します。  
  
    ```c#  
  
    public bool TestConnection()  
    {  
       // Add code to test connection  
  
       return true;  
    }  
    ```  
  
12. ドメインの現在の状態を返す、GetDomainState メソッドを追加します。 次のコード例は、GetDomainState メソッドを示します。  
  
    ```c#  
  
    public DomainState GetDomainState()  
    {  
       string domainstatus = "FullyOperational";  
       long expirationDate = 365;  
       using (RegistryKey key = ProductInfo.RegKey.OpenSubKey("Domain Manager\\Settings", true))  
       {  
          domainstatus = (key == null) ? "Ready" : key.GetValue("DomainStatus", "Ready").ToString();  
          expirationDate = Int64.Parse(key.GetValue("ExpirationDate", "365").ToString());  
       }  
  
       switch (domainstatus)  
       {  
          case "Failed":  
             return new DomainState(DomainStatus.Failed,   
                null,   
                DateTime.Now.AddDays(expirationDate));  
          case "Ready":  
             return new DomainState(DomainStatus.Ready,   
                null,   
                DateTime.Now.AddDays(expirationDate));  
          case "InRenewal":  
             return new DomainState(DomainStatus.InRenewal,   
                null,   
                DateTime.Now.AddDays(expirationDate));  
          case "InRenewalCustomerInterventionRequired":  
             return new DomainState(DomainStatus.InRenewalCustomerInterventionRequired,   
                null,   
                DateTime.Now.AddDays(expirationDate));  
          case "Pending":  
             return new DomainState(DomainStatus.Pending,   
                null,   
                DateTime.Now.AddDays(expirationDate));  
          case "PendingCustomerInterventionRequired":  
             return new DomainState(DomainStatus.PendingCustomerInterventionRequired,   
                null,   
                DateTime.Now.AddDays(expirationDate));  
          case "RenewalFailed":  
             return new DomainState(DomainStatus.RenewalFailed,   
                null,   
                DateTime.Now.AddDays(expirationDate));  
          default:  
             return new DomainState(DomainStatus.Unknown,   
                null,   
                DateTime.Now.AddDays(expirationDate));                   
          }  
    }  
    ```  
  
13. 証明書の現在の状態を返す、GetCertificateState メソッドを追加します。 次のコード例は、GetCertificateState メソッドを示します。  
  
    ```c#  
  
    public CertificateState GetCertificateState(bool renew)  
    {  
       return new CertificateState(CertificateStatus.Ready, string.Empty);  
    }  
    ```  
  
14. 保存し、ソリューションをビルドします。  
  
###  <a name="sign-the-assembly-with-an-authenticode-signature"></a><a name="BKMK_SignAssembly"></a>Authenticode 署名を使用してアセンブリに署名する  
 オペレーティング システムで使用するために、アセンブリを Authenticode で署名する必要があります。 アセンブリの署名の詳細については、「 [Authenticode によるコードの署名と確認 (英語の場合があります)](https://msdn.microsoft.com/library/ms537364\(VS.85\).aspx#SignCode)」を参照してください。  
  
###  <a name="install-the-assembly-on-the-reference-computer"></a><a name="BKMK_InstallAssembly"></a>参照コンピューターにアセンブリをインストールする  
 アセンブリを参照コンピューターのフォルダーに配置します。 次の手順でレジストリに入力するため、フォルダーのパスをメモしておきます。  
  
### <a name="add-a-key-to-the-registry"></a>キーのレジストリへの追加  
 アセンブリの特性と場所を定義するためにレジストリ エントリを追加します。  
  
##### <a name="to-add-a-key-to-the-registry"></a>キーをレジストリに追加するには  
  
1.  参照コンピューターで、 **[スタート]** ボタンをクリックし、「**regedit**」と入力して、**Enter** キーを押します。  
  
2.  左のウィンドウで、 **[HKEY_LOCAL_MACHINE]** 、 **[SOFTWARE]** 、 **[Microsoft]** 、 **[Windows Server]** 、 **[Domain Managers]** 、 **[Providers]** の順に展開します。  
  
3.  **[Providers]** を右クリックし、 **[新規作成]** をクリックして、 **[キー]** をクリックします。  
  
4.  プロバイダーの識別子をキーの名前として入力します。 識別子は、「[IDomainSignupProvider インターフェイスの実装のアセンブリへの追加](Add-Third-Level-Domain-Names.md#BKMK_DomainSignup)」の手順 8 でプロバイダーに対して定義した GUID です。  
  
5.  先ほど作成したキーを右クリックし、 **[文字列値]** をクリックします。  
  
6.  文字列の名前に対して「**Assembly**」と入力し、**Enter** キーを押します。  
  
7.  右側のウィンドウで、新しい **Assembly** 文字列を右クリックし、 **[変更]** をクリックします。  
  
8.  前に作成したアセンブリ ファイルへの完全なパスを入力し、 **[OK]** をクリックします。  
  
9. キーを再度右クリックし、 **[文字列値]** をクリックします。  
  
10. 文字列の名前に対して「**Enabled**」と入力し、**Enter** キーを押します。  
  
11. 右側のウィンドウで、新しい **Enabled** 文字列を右クリックし、 **[変更]** をクリックします。  
  
12. 「**True**」と入力し、 **[OK]** をクリックします。  
  
13. キーを再度右クリックし、 **[文字列値]** をクリックします。  
  
14. 文字列の名前に対して「**Type**」と入力し、**Enter** キーを押します。  
  
15. 右側のウィンドウで、新しい **Type** 文字列を右クリックし、 **[変更]** をクリックします。  
  
16. アセンブリで定義されたプロバイダーの完全なクラス名を入力し、 **[OK]** をクリックします。  
  
###  <a name="restart-the-windows-server-domain-name-management-service"></a><a name="BKMK_RestartService"></a>Windows Server ドメインネーム管理サービスを再起動する  
 プロバイダーがオペレーティング システムに対して使用できるようになるには、Windows Server Domain Management サービスを再起動する必要があります。  
  
##### <a name="restart-the-service"></a>サービスの再開  
  
1.  **[スタート]** ボタンをクリックし、「**mmc**」と入力して、**Enter** キーを押します。  
  
2.  サービス スナップインがコンソールの一覧に表示されていない場合、サービス スナップインを追加するために次の手順を完了します。  
  
    1.  **[ファイル]** メニューの **[スナップインの追加と削除]** をクリックします。  
  
    2.  **[利用できるスナップイン]** の一覧で、 **[サービス]** 、 **[追加]** の順にクリックします。  
  
    3.  **[サービス]** ダイアログ ボックスで、 **[ローカル コンピューター]** が選択されていることを確認し、 **[完了]** をクリックします。  
  
    4.  **[OK]** をクリックして **[スナップインの追加と削除]** ダイアログ ボックスを閉じます。  
  
3.  **[サービス]** をダブルクリックし、 **[Windows Server Domain Management]** までスクロールして選択し、 **[サービスを再開]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [イメージ  の作成とカスタマイズ](Creating-and-Customizing-the-Image.md)  
 [追加のカスタマイズ](Additional-Customizations.md)   
 [展開  のイメージの準備](Preparing-the-Image-for-Deployment.md)  
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)