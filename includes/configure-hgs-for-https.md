最初に、HGS を SSL 証明書を使用する証明機関から取得します。 各ホスト コンピューターは、SSL 証明書を信頼するので、会社の公開キー インフラストラクチャまたはサード パーティの CA から SSL 証明書を発行することをお勧めする必要があります。 ただし IIS でサポートされているすべての SSL 証明書は、HGS でサポートされて**証明書のサブジェクト名が HGS の完全修飾サービス名と一致する必要があります**(クラスターの分散ネットワーク名)。 たとえば、HGS ドメインで"bastion.local"あり HGS サービス名は"hgs"場合、"hgs.bastion.local"の SSL 証明書を発行する必要があります。 必要に応じて、証明書のサブジェクト代替名フィールドには、追加の DNS 名を追加できます。

SSL 証明書は、管理者特権での PowerShelll セッションを開くしを実行すると証明書のパスを指定するか[セット HgsServer](https://technet.microsoft.com/itpro/powershell/windows/host-guardian-service/server/set-hgsserver):


```powershell
$sslPassword = Read-Host -AsSecureString -Prompt "SSL Certificate Password"
Set-HgsServer -Http -Https -HttpsCertificatePath 'C:\temp\HgsSSLCertificate.pfx' -HttpsCertificatePassword $sslPassword
```

または、ローカルの証明書ストアに既に証明書をインストールした場合は、拇印で参照できます。

```powershell
Set-HgsServer -Http -Https -HttpsCertificateThumbprint 'A1B2C3D4E5F6...'
```

> [!IMPORTANT]
> SSL 証明書での HGS の構成には、HTTP エンドポイントが無効にしません。
> のみの HTTPS エンドポイントの使用を許可する場合は、ポート 80 への着信接続をブロックする Windows ファイアウォールを構成します。
> **IIS バインディングを変更しないでください**そのためには、HTTP エンドポイントを削除する HGS の web サイトのサポートは。
