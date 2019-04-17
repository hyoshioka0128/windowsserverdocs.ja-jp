---
title: "第 3 レベル ドメイン名を追加します。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e5b4a362-1881-4024-ae4e-cc3b05e50103
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 64bf24e45155fdd981e2061b3de7ebce1c53b36c
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="add-third-level-domain-names"></a>第 3 レベル ドメイン名を追加します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

ユーザーが、設定 Up Domain Name ウィザードで第 3 レベル ドメイン名を要求する機能を追加することができます。 これを行う作成して、オペレーティング システム内のドメイン マネージャーによって使用されるコード アセンブリをインストールします。  
  
## <a name="create-a-provider-of-third-level-domain-names"></a>第 3 レベル ドメイン名のプロバイダーを作成します。  
 第 3 レベル ドメイン名を利用できるようにするには作成して、ウィザードにドメイン名を提供するコード アセンブリをインストールします。 これを行うには、次のタスクを実行します。  
  
-   [IDomainSignupProvider インターフェイスの実装のアセンブリへの追加します。](Add-Third-Level-Domain-Names.md#BKMK_DomainSignup)  
  
-   [IDomainMaintenanceProvider インターフェイスの実装のアセンブリへの追加します。](Add-Third-Level-Domain-Names.md#BKMK_DomainMaintenance)  
  
-   [Authenticode 署名によるアセンブリを署名します。](Add-Third-Level-Domain-Names.md#BKMK_SignAssembly)  
  
-   [参照コンピューターで、アセンブリをインストールします。](Add-Third-Level-Domain-Names.md#BKMK_InstallAssembly)  
  
-   [Windows Server Domain Name Management サービスを再起動します。](Add-Third-Level-Domain-Names.md#BKMK_RestartService)  
  
###  <a name="BKMK_DomainSignup"></a>IDomainSignupProvider インターフェイスの実装のアセンブリへの追加します。  
 IDomainSignupProvider インターフェイスを使用して、ウィザードをドメイン サービスを追加します。  
  
##### <a name="to-add-the-idomainsignupprovider-code-to-the-assembly"></a>IDomainSignupProvider コードをアセンブリに追加するには  
  
1.  Visual Studio 2008 でプログラムを右クリックして、管理者として開きます、**開始**メニューを選択して**管理者として実行**します。  
  
2.  をクリックして**ファイル**、] をクリックして**新規**、] をクリックし、**プロジェクト**します。  
  
3.  **新しいプロジェクト**ダイアログ ボックスで、] をクリックして**Visual c#**、] をクリックして**クラス ライブラリ**、ソリューションの名前を入力し、[クリックして**OK**します。  
  
4.  Class1.cs ファイルの名前を変更します。 たとえば、MyDomainNameProvider.cs  
  
5.  Wssg.Web.DomainManagerObjectModel.dll、CertManaged.dll、WssgCertMgmt.dll、WssgCommon.dll ファイルへの参照を追加します。  
  
6.  次の追加のステートメントを使用します。  
  
    ```c#  
  
    using System.Collections.ObjectModel;  
    using System.Net;  
    using System.Net.Sockets;  
    using Microsoft.WindowsServerSolutions.Certificates;  
    using Microsoft.WindowsServerSolutions.CertificateManagement;  
    using Microsoft.WindowsServerSolutions.Common;  
    using Microsoft.Win32;  
    ```  
  
7.  名前空間とクラス ヘッダーを次の例に示すように変更します。  
  
    ```c#  
    namespace Microsoft.WindowsServerSolutions.RemoteAccess.Domains  
    {  
        public class MyDomainNameProvider : IDomainSignupProvider  
        {  
        }  
    }  
    ```  
  
8.  ウィザードで示されているサービスを定義すると、クラスを Initialize メソッドと必要な変数を追加します。  
  
    > [!NOTE]
    >  Initialize メソッドは、一意である必要があるドメイン プロバイダーの識別子を定義します。 これを行う一般的な方法では、識別子として GUID を定義します。 GUID の作成の詳細については、次を参照してください。[Guid の作成 (guidgen.exe)](https://go.microsoft.com/fwlink/?LinkId=116098)します。  
  
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
  
9. 前の手順で初期化された製品の一覧を返す、GetOfferings メソッドを追加します。 次のコード例は、GetOfferings メソッドを示しています。  
  
    ```c#  
  
    public ReadOnlyCollection<Offering> GetOfferings()  
    {  
       return this.offerings.AsReadOnly();  
    }  
    ```  
  
10. 一覧からサービスを返す FindOfferingForDomain メソッドを追加します。 次のコード例は、FindOfferingForDomain メソッドを示します。  
  
    ```  
  
    public Offering FindOfferingForDomain(string domain)  
    {  
       // Return the offering that has the domain name.  
       return offerings[0];  
    }  
  
    ```  
  
11. サービスにアクセスするために必要な資格情報を定義する、SetCredentials メソッドを追加します。 次のコード例は、SetCredentials メソッドを示しています。  
  
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
  
12. SetCredentials で定義されている資格情報を検証する、ValidateCredentials メソッドを追加します。 次のコード例は、ValidateCredentials メソッドを示しています。  
  
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
  
13. 要求で指定されたサービスでサポートされているルート ドメイン名の一覧を返す、GetAvailableDomainRoots メソッドを追加します。 このルート ドメイン名の一覧を空にする必要がありますはできません。 次のコード例は、GetAvailableDomainRoots メソッドを示しています。  
  
    ```c#  
  
    public ReadOnlyCollection<string> GetAvailableDomainRoots(DomainNameRequest request)  
    {  
       List<string> list = new List<string>();  
       list.Add("domain1.com");  
       list.Add("domain1.org");  
  
       return list.AsReadOnly();  
    }  
    ```  
  
14. 現在のユーザーが既に所有して、現在のサービスを基準にしているドメイン名の一覧を返す、GetUserDomainNames メソッドを追加します。 このリストは空である可能性があります。 次のコード例は、GetUserDomainNames メソッドを示しています。  
  
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
  
15. 指定したサービスが許可するドメインの最大数を返す、GetUserDomainQuota メソッドを追加します。 最大値が適用されない場合は、このメソッドは 0 を返すはずです。 次の例では、GetUserDomainQuota メソッドを示します。  
  
    ```c#  
  
    public int GetUserDomainQuota(DomainNameRequest request)  
    {  
       return 0;  
    }  
    ```  
  
16. 要求されたドメイン名の可用性をチェックする、CheckDomainAvailability メソッドを追加し、候補の一覧を返すことができます。 次のコード例は、CheckDomainAvailability メソッドを示しています。  
  
    ```c#  
  
    public bool CheckDomainAvailability(DomainNameRequest request,   
       out ReadOnlyCollection<string> suggestions)  
    {  
       suggestions = null;  
  
       return true;  
    }  
    ```  
  
17. 要求されたドメイン名をコミットする、CommitDomain メソッドを追加します。 このメソッドが正常に完了を意味することは、ドメイン名がユーザー アカウントに関連付け、状態が FullyOperational の場合、およびプロバイダーとサービスがアクティブになる場合は、証明書を取得するメンテナンス プロバイダーがすぐに呼び出されます。 次のコード例は、CommitDomain メソッドを示しています。  
  
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
  
18. ユーザーがドメイン名の解放することをプロバイダー、ReleaseDomain メソッドを追加します。 次のコード例は、ReleaseDomain メソッドを示しています。  
  
    ```c#  
  
    public bool ReleaseDomain(DomainNameRequest request)  
    {  
       return true;  
    }  
    ```  
  
19. ドメイン サインアップ ワークフローのランディング ページの URL を返す、GetProviderLandingUrl メソッドを追加します。 次のコード例は、GetProviderLandingUrl メソッドを示しています。  
  
    ```c#  
  
    public Url GetProviderLandingUrl(DomainNameRequest request)  
    {  
       return new Url("www.contoso.com");  
    }  
    ```  
  
20. ドメイン保守タスクに使用される IDomainMaintenanceProvider のインスタンスを返す、GetDomainMaintenanceProvider メソッドを追加します。 このメソッドは、CommitDomain メソッドが成功した後、およびドメイン マネージャーを起動したときに呼び出されます。 次のコード例は、GetDomainMaintenanceProvider メソッドを示しています。  
  
    ```c#  
  
    public IDomainMaintenanceProvider GetDomainMaintenanceProvider()  
    {  
       return new MyDomainMaintenanceProvider();  
    }  
    ```  
  
21. プロジェクトを保存し、終了しませんので、次の手順に追加します。 次の手順を完了するまでプロジェクトをビルドできなきます。  
  
###  <a name="BKMK_DomainMaintenance"></a>IDomainMaintenanceProvider インターフェイスの実装のアセンブリへの追加します。  
 IDomainMaintenanceProvider が作成した後、ドメインを維持するために使用されます。  
  
##### <a name="to-add-the-idomainmaintenanceprovider-code-to-the-assembly"></a>IDomainMaintenanceProvider コードをアセンブリに追加するには  
  
1.  ドメイン メンテナンス プロバイダーのクラス ヘッダーを追加します。 プロバイダーに対して定義した名前が、以前に定義した GetDomainMaintenanceProvider メソッド内の名前と一致することを確認します。  
  
    ```c#  
  
    public class MyDomainMaintenanceProvider : IDomainMaintenanceProvider  
    {  
    }  
    ```  
  
2.  アクティブなプロバイダーを設定する、Activate メソッドを追加します。 次のコード例は、Activate メソッドを示しています。  
  
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
  
3.  すべてのアクションを非アクティブ化するために使用する、Deactivate メソッドを追加します。 次のコード例は、Deactivate メソッドを示しています。  
  
    ```  
  
    public void Deactivate()  
    {  
       //Deactivate all actions  
    }  
  
    ```  
  
4.  ユーザーの資格情報を更新する、SetCredentials メソッドを追加します。 たとえば、有効でなくなった資格情報を更新するこのメソッドを呼び出すことがあります。 次のコード例は、SetCredentials メソッドを示しています。  
  
    ```c#  
  
    protected DomainProviderCredentials Credentials { get; set; }  
  
    public bool SetCredentials(DomainProviderCredentials credentials)  
    {  
       this.Credentials = credentials;  
  
       return true;  
    }  
    ```  
  
5.  指定された資格情報を検証する、ValidateCredentials メソッドを追加します。 次のコード例は、ValidateCredentials メソッドを示しています。  
  
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
  
6.  サーバーの外部 IP アドレスを返す、GetPublicAddress メソッドを追加します。 次のコード例は、GetPublicAddress メソッドを示しています。  
  
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
  
7.  現在構成されているドメイン名の証明書の要求を送信する、SubmitCertificateRequest メソッドを追加します。  
  
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
  
8.  ドメインの状態が FullyOperational の場合は、証明書の応答を返す、GetCertificateResponse メソッドを追加します。 両方の新しい証明書要求と証明書更新要求は、このメソッドが呼び出されます。 次のコード例は、GetCertificateResponse メソッドを示しています。  
  
    ```c#  
  
    public string GetCertificateResponse(bool renew)  
    {  
       return cert;  
    }  
    ```  
  
9. 証明書の更新を処理する、SubmitRenewCertificateRequest メソッドを追加します。 次のコード例は、SubmitRenewCertificateRequest メソッドを示しています。  
  
    ```c#  
  
    public void SubmitRenewCertificateRequest()  
    {  
       // Add certificate renewal code   
    }  
    ```  
  
10. プロバイダーによって保存された DNS レコードを更新する、UpdateDNSRecords メソッドを追加します。 次のコード例は、UpdateDNS メソッドを示しています。  
  
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
  
11. バックエンド サービスへの接続を確立しようとする、TestConnection メソッドを追加します。 このメソッドは、認証を必要とする場合は、適切な例外がスローする必要があります。 次のコード例は、TestConnection メソッドを示しています。  
  
    ```c#  
  
    public bool TestConnection()  
    {  
       // Add code to test connection  
  
       return true;  
    }  
    ```  
  
12. ドメインの現在の状態を返す、GetDomainState メソッドを追加します。 次のコード例は、GetDomainState メソッドを示しています。  
  
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
  
13. 証明書の現在の状態を返す、GetCertificateState メソッドを追加します。 次のコード例は、GetCertificateState メソッドを示しています。  
  
    ```c#  
  
    public CertificateState GetCertificateState(bool renew)  
    {  
       return new CertificateState(CertificateStatus.Ready, string.Empty);  
    }  
    ```  
  
14. 保存し、ソリューションをビルドします。  
  
###  <a name="BKMK_SignAssembly"></a>Authenticode 署名によるアセンブリを署名します。  
 オペレーティング システムで使用されるようにアセンブリの Authenticode 署名する必要があります。 アセンブリの署名の詳細については、次を参照してください。[Authenticode によるコードのチェックの署名と](https://msdn.microsoft.com/library/ms537364\(VS.85\).aspx#SignCode)します。  
  
###  <a name="BKMK_InstallAssembly"></a>参照コンピューターで、アセンブリをインストールします。  
 アセンブリは、参照コンピューター上のフォルダーに配置します。 次の手順でレジストリに入力するためメモ、フォルダーのパス。  
  
### <a name="add-a-key-to-the-registry"></a>キーをレジストリに追加します。  
 特性とアセンブリの場所を定義するためにレジストリ エントリを追加します。  
  
##### <a name="to-add-a-key-to-the-registry"></a>レジストリ キーを追加するには  
  
1.  参照コンピューターで、をクリックして**開始**、入力**regedit**、キーを押します**Enter**します。  
  
2.  左側のウィンドウで [ **HKEY_LOCAL_MACHINE**、展開**ソフトウェア**、展開**Microsoft**、展開**Windows Server**、展開**Domain Managers**、し、展開**プロバイダー**します。  
  
3.  右クリック**プロバイダー**、] をポイント**新規**、] をクリックし、**キー**します。  
  
4.  プロバイダーの識別子をキーの名前として入力します。 手順 8 でプロバイダーに対して定義した GUID には、識別子[IDomainSignupProvider インターフェイスの実装のアセンブリへの追加](Add-Third-Level-Domain-Names.md#BKMK_DomainSignup)します。  
  
5.  作成したキーを右クリックし、をクリックして**文字列値**します。  
  
6.  種類**アセンブリ**文字列を検索し、キーを押しますの名前を**Enter**します。  
  
7.  新しいを右クリックして**アセンブリ**文字列の右側のウィンドウで、クリックして**変更**します。  
  
8.  をクリックして、以前に作成するアセンブリ ファイルへの完全パスを入力**OK**します。  
  
9. 再度、キーを右クリックし、をクリックして**文字列値**します。  
  
10. 種類**有効**文字列を検索し、キーを押しますの名前を**Enter**します。  
  
11. 新しいを右クリックして**有効**文字列の右側のウィンドウで、クリックして**変更**します。  
  
12. 種類**True**、] をクリックし、**OK**します。  
  
13. 再度、キーを右クリックし、をクリックして**文字列値**します。  
  
14. 種類**種類**文字列を検索し、キーを押しますの名前を**Enter**します。  
  
15. 新しいを右クリックして**種類**文字列の右側のウィンドウで、クリックして**変更**します。  
  
16. アセンブリで定義されているプロバイダーの完全なクラス名を入力し、クリックして**OK**します。  
  
###  <a name="BKMK_RestartService"></a>Windows Server Domain Name Management サービスを再起動します。  
 オペレーティング システムに使用可能になるプロバイダーの Windows Server Domain Management サービスを再起動する必要があります。  
  
##### <a name="restart-the-service"></a>サービスを再開します  
  
1.  をクリックして**開始**、種類**mmc**、キーを押します**Enter**します。  
  
2.  サービス スナップインがコンソールに表示されない場合は、次の手順を実行して追加します。  
  
    1.  をクリックして**ファイル**、] をクリックし、**スナップインの追加/削除**します。  
  
    2.  **利用できるスナップイン**一覧で、クリックして**サービス**、] をクリックし、**追加**します。  
  
    3.  **サービス**] ダイアログ ボックスで、いることを確認**ローカル コンピューター**をクリックして選択して**完了**します。  
  
    4.  をクリックして**OK**を閉じるには、**スナップインの追加/削除**] ダイアログ ボックス。  
  
3.  ダブルクリック**サービス**を下へスクロールして、選択**Windows Server Domain Management**、] をクリックし、**サービスを再起動**します。  
  
## <a name="see-also"></a>参照してください。  
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)