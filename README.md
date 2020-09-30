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

O serviço da API fica no servidor 10.70.15.16 na porta 8989, se o sistema que vai consumir a API estiver na rede da PCRJ não será preciso solicitar liberação de acesso no Firewall, porém se o sistema estiver na nuvem, será necessário solicitar um acesso via IP externo (IP Externo : 187.111.110.174) a equipe da DOP.

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
     recurso    : <recurso>
     ambiente   : <DESENVOLVIMENTO ou PRODUCAO>
```  
Esse request vai retornar um token, esse token é valido por 24hs e deve ser informado nos requests para os endpoints desejados, relacionados abaixo

Grupos - Relação de grupos de materiais

/api/sigma/grupo

```sh
Request URL : http://10.70.15.16:8989/api/sigma/grupo 
Method      : GET
Headers     : 
   - token      : token
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
