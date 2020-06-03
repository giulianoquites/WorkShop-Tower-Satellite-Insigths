### Instalando o Red Hat Insigths Client

Para instalar o Red Hat insigths precisamos registar o RHEL no Salellite ou Cloud.redhat.com atraves do insights-client.

Podemos fazer o registro do hosts no satellite atraves do Activation Key ou Bootstrap.py:

~~~~

[root@client ~]# curl https://sat66.gquites.local/pub/bootstrap.py > bootstrap.py --insecure
[root@client ~]# chmod +x bootstrap.py

~~~~

Depois execute o comando para fazer o registro:

~~~~

[root@client ~]# ./bootstrap.py -l admin -s sat66.gquites.local -o 'gquites.local' -L 'gquites' -a rhel7

~~~~

Executando via Activation Key:

~~~~
[root@client ~]# rpm -Uvh http://sat66.gquites.local/pub/katello-ca-consumer-latest.noarch.rpm ;subscription-manager register --org="gquites" --activationkey="tower"
~~~~

Depois de registrar o hosts, precisamos validar se o repositorio foi ativado:

Para fazer pelo Satellite precisa do repositorio:

~~~~
[root@client ~]# yum repolist
Loaded plugins: enabled_repos_upload, package_upload, product-id, search-disabled-repos, subscription-manager
repo id                                                repo name                                                                      status
!rhel-7-server-insights-3-rpms/x86_64                  Red Hat Insights 3 (for RHEL 7 Server) (RPMs)                                        8
!rhel-7-server-rpms/x86_64                             Red Hat Enterprise Linux 7 Server (RPMs)                                        29,082
!rhel-7-server-satellite-tools-6.7-rpms/x86_64         Red Hat Satellite Tools 6.7 (for RHEL 7 Server) (RPMs)                              65
   
~~~~

Com o repositorio ativado. Vamos instalar o cliente o insigths e registrar.

~~~~
[root@client ~]# yum -y install insights-client  

[root@client ~]# insights-client --register 
This host has already been registered.
Automatic scheduling for Insights has been enabled.
Starting to collect Insights data for client.gquites.local
Uploading Insights data.
Successfully uploaded report from client.gquites.local to account 540155.
View the Red Hat Insights console at https://cloud.redhat.com/insights/

~~~~

