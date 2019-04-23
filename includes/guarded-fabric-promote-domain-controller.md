1.  実行[インストール HgsServer](https://technet.microsoft.com/itpro/powershell/windows/hgsserver/install-hgsserver)ドメインに参加し、ドメイン コント ローラーにノードを昇格します。

    ```powershell
    $adSafeModePassword = ConvertTo-SecureString -AsPlainText '<password>' -Force

    $cred = Get-Credential 'relecloud\Administrator'

    Install-HgsServer -HgsDomainName 'bastion.local' -HgsDomainCredential $cred -SafeModeAdministratorPassword $adSafeModePassword -Restart
    ```

2.  サーバーが再起動すると、ドメイン管理者アカウントでログインします。

<!-- Appears twice in guarded-fabric-configure-additional-hgs-nodes.md 
-->