<p align="center">
  <a href="https://onsac.com/">
    <img src="https://onsac.com/wp-content/uploads/2020/08/tl.png" alt="Bootstrap logo" width="200" height="180">
  </a>
</p>

<h3 align="center">AIO Integrador</h3>

<p align="center">
  Automações e Integrações sem limitações (AIops/DEVops)
  <br>
  <a href="https://onsac.com/"><strong>Conheça mais sobre nosso serviço »</strong></a>
  </p>
  
  
## API SIGMA

A API SIGMA foi desenvolvida para viabilizar e controlar o acesso as views da base de dados stage em Oracle que é atualizada diáriamente via datagrid com informações da base de dados DB2.
Para iniciar uma implementação de consumo das API, será necessário solicitar um cadastro e acesso ao Recurso no via (https://jeap.rio.rj.gov.br), após conseguir o :
ID consumidor e Chave de Acesso

Siga as instruções abaixo. 

As APIs disponibiliza acesso as views abaixo, e entrega os resultados no padrão JSON.

```sh 
sigma.vw_grupo tb_grupo
sigma.vw_classe tb_classe
sigma.vw_subclasse tb_subclasse
sigma.vw_unidade tb_unidade
sigma.vw_material tb_material
sigma.vw_fornecedor tb_fornecedor
sigma.vw_movimentacao
```

O serviço da API fica no servidor 10.70.15.16 na porta 8989, se o sistema que vai consumir a API estiver na rede da PCRJ não será preciso solicitar liberação de acesso no Firewall, porém se o sistema estiver na nuvem, será necessário solicitar um acesso via IP externo a equipe da DOP.

O primeiro passo apos conseguir os devidos acessos, é implementar o metodo de autenticação

```sh
http://10.70.15.16:8989/api/autenticacao
```

Para realizar a autenticação será necessário a seguinte estrutura para o peyload 

```sh
Request URL : http://10.70.15.16:8989/api/autenticacao 
Method      : POST
Headers     : 
   - consumidor : <id do consumidor informada pelo cerberus>
     chaveacesso: <chave informada pelo cerberus>
     recurso    : autenticacao
     ambiente   : <DESENVOLVIMENTO ou PRODUCAO>
```  
Esse request vai retornar um token, esse token é valido por 24hs e deve ser informado nos requests para os endpoints desejados, relacionados abaixo

Grupos - Relação de grupos de materiais

/api/sigma/grupo

```sh
Request URL : http://10.70.15.16:8989/api/sigma/grupo 
Method      : GET
Headers     : 
   - consumidor : <id do consumidor informada pelo cerberus>
     chaveacesso: <chave informada pelo cerberus>
     recurso    : grupo
     ambiente   : <DESENVOLVIMENTO ou PRODUCAO>
     token      : token
```  



```sh 
/autenticacao
/api/sigma/grupo/:grupo_id/classe/:classe_id/subclasse/:subclasse_id/unidade/:unidade_id
/api/sigma/material/:grupo_id/classe/:classe_id/subclasse/:subclasse_id/unidade/:unidade_id
/api/sigma/fornecedor/:fornecedor_id
/api/sigma/movimentacao/os/:os_id/nota/:nota_id/serie/:serie_id
/api/sigma/movimentacao/fornecedor/:fornecedor_id/nota/:nota_id/serie/:serie_id
/api/sigma/os/:os_id
```
```sh 
app.use('/sigma/', grupoRouter);
```
```sh
app.use('/sigma/grupo/:grupo_id/classe', classeRouter);
```
```sh
app.use('/sigma/grupo/:grupo_id/classe/:classe_id/subClasse', subClasseRouter);
```
```sh
app.use('/sigma/grupo/:grupo_id/classe/:classe_id/subClasse/:subClasse_id/unidade', unidadeRouter);
```


https://jeap.rio.rj.gov.br/cerberus/seam/resource/v1/permissoes 
</br> 
E informar os seguintes headers na mesma. 
* ambiente: Ambiente que deseja efetuar a requisição DESENVOLVIMENTO, HOMOLOGACAO ou PRODUCAO sem acentos ou cedilha.
* provedor: Identificador do Sistema que você deseja validar as permissões do Usuário.
* consumidor: Identificador do Consumidor(Sistema ou Usuário) que está efetuando a chamada à API do Cerberus.
* chaveAcesso: Chave de Acesso do Consumidor.
* usuario: Usuário que terá as permissões verificadas.
* senhaUsuario: Senha do usuário que terá as permissões verificadas.

```sh
HttpGet request = new HttpGet("https://jeap.rio.rj.gov.br/cerberus/seam/resource/v1/integracoes/NOME_RECURSO");
        
request.addHeader("ambiente", "DESENVOLVIMENTO");
    
request.addHeader("provedor", "EXEMPLO");
    
request.addHeader("consumidor", "EXEMPLO");
        
request.addHeader("chaveAcesso", "d4fec2a2-7f41-43bd-9c0c-c00afe8f4858");
```
consumidor: 3186
Verona2011
Verona2011

http://10.70.15.16:8899/api/sigma/grupo



osinfo 3186
2f9b49dd-518c-4d7a-93d9-50aec569279b

cosme.silveira.rio@gmail.com

mysql -u root -p"sdt11000"



DGB2115
```sh
        objetos += "    ctr.ctrt_nr_contrato       contratoNumero,      ";
        objetos += "    ctr.ctrt_nr_processo       contratoProcesso,    ";
        objetos += "    dos.orga_ds_nome_fantasia  nomeOs,              ";
        objetos += "    doc.COD_UNIDADE            codUnidade,          ";
        objetos += "    uni.unid_ds_nome_fantasia  nomeUnidade,         ";
```

User : DGB2115 Password : $2a$08$8MRD2uCvZw4R1DPi7bhMhusmOGC62QbDLhvDzXPD6cV6dmdSX7fTW


http://10.70.15.16:8899/api/sigma/grupo/:grupo_id/classe/:classe_id/subclasse/:subclasse_id
http://10.70.15.16:8899/api/sigma/material/:grupo_id+classe_id+subclasse_id
http://10.70.15.16:8899/api/sigma/material/:material_id
http://10.70.15.16:8899/api/sigma/unidade/:unidade_id
http://10.70.15.16:8899/api/sigma/fornecedor/:fornecedor_id
http://10.70.15.16:8899/api/sigma/movimento/:fornecedor_id/emissao/:emissao_id/nota/:nota_id/serie/:serie_id

http://10.70.15.16:8889/api/sigma/movimento/06970328000117/emissao/20190830/nota/602/serie/1
http://10.70.15.16

:8899/authenticate

:8889/autenticacao

Banco BI

Servidor 10.2.221.20
 
Servidor Linux

IP 10.70.15.16

```sh
mongo 191.232.237.220/OSINFO_FILES -u userbi -p 5423ut
```
```sh
mongodb://userbi:5423ut@191.232.237.220:27017/OSINFO_FILES
```
```sh
mongo -host 191.232.194.150 -u userbi -p 5423ut
```
```sh
mongo -host 191.232.237.220 -u userbi -p 5423ut
```
```sh
mongo -host 10.70.15.16/aio -u userbi -p 5423ut
```
```sh
mongo 191.232.194.150/OSINFO_FILES -u user_bi -p
```
```sh
mongo 191.232.194.150 -u "user_bi" -p "5423ut" --authenticationDatabase "OSINFO_FILES"
```
```sh
mongo 191.232.194.150 -u "user_bi" -p "5423ut" --authenticationDatabase "osinfo_files"
```
```sh
mongo 191.232.194.150/OSINFO_FILES -u "user_bi" -p "5423ut" 
```
osinfo :
191.232.194.153


ORIGENS :
iplan-osinfo.dev.solutis.xyz
iplan-osinfo.test.solutis.xyz

DESTINO :
IP Interno 10.70.15.16

PORTA   :
8899

PROTOCOLO:
HTTP

IP Externo : 187.111.110.174


A partir do dia 25/11/2019 (segunda-feira), o acesso ao serviço de VPN Checkpoint será alterado para novo endereço IP 187.111.111.2
O endereço IP antigo 200.20.66.189 deixará de funcionar, leia o documento de orientações de como realizar a alteração do cliente VPN em anexo.
Não haverá alteração nas credenciais de acesso (usuário e senha)
</br>
Conforme solicitado ontem, seguem as URIs das APIs :
</br>
http://10.70.15.16:8899/api/sigma/grupo/:grupo_id/classe/:classe_id/subclasse/:subclasse_id
http://10.70.15.16:8899/api/sigma/material/:grupo_id+classe_id+subclasse_id
http://10.70.15.16:8899/api/sigma/material/:material_id
http://10.70.15.16:8899/api/sigma/unidade/:unidade_id
http://10.70.15.16:8899/api/sigma/fornecedor/:fornecedor_id
http://10.70.15.16:8899/api/sigma/movimento/:fornecedor_id/nota/:nota_id/serie/:serie_id

<p align="center">
     <img src="https://github.com/onsac/AIO-Integrador/blob/master/Telas-Configura%C3%A7%C3%A3o/Tela-Autentica%C3%A7%C3%A3o%20API%20SIGMA.jpeg" alt="Tela-autenticação API SIGMA" >
</p>
