ホスト ガーディアン サービスは、別の Active Directory フォレストにインストールする必要があります。
HGS マシンがあることを確認**いない**を開始して、ローカル マシン現時点としてサインインする前に、ドメインに参加します。

ホスト ガーディアン サービスをインストールし、そのドメインを構成するには、次のコマンドを実行します。
ここで指定したパスワードに対してのみ適用されます、ディレクトリ サービス復元モード パスワードを Active Directory。*いない*管理者アカウントのログインのパスワードを変更します。
-HgsDomainName の独自の任意のドメイン名を提供できます。

```powershell
$adminPassword = ConvertTo-SecureString -AsPlainText '<password>' -Force

Install-HgsServer -HgsDomainName 'bastion.local' -SafeModeAdministratorPassword $adminPassword -Restart
```

<!-- Appears in guarded-fabric-install-hgs-default.md and set-up-hgs-for-always-encrypted-in-sql-server.md
-->
