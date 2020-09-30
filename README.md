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
Para iniciar uma implementação de consumo das API, será necessário solicitar um cadastro e acesso ao Recurso via (https://jeap.rio.rj.gov.br), após conseguir o :
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

O serviço da API fica no servidor 10.70.15.16 na porta 8899, se o sistema que vai consumir a API estiver na rede da PCRJ não será preciso solicitar liberação de acesso no Firewall, porém se o sistema estiver na nuvem, será necessário solicitar um acesso via IP externo (IP Externo : 187.111.110.174) a equipe da DOP.

O primeiro passo apos conseguir os devidos acessos, é implementar o metodo de autenticação

```sh
http://10.70.15.16:8899/api/autenticacao
```

Para realizar a autenticação será necessário a seguinte estrutura para o peyload 

```sh
Request URL : http://10.70.15.16:8899/api/autenticacao 
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
Request URL : http://10.70.15.16:8899/api/sigma/grupo 
Method      : GET
Headers     : 
   - token      : token
```  

# Grupo
http://10.70.15.16:8899/api/sigma/grupo/:grupo_id/classe/:classe_id/subclasse/:subclasse_id
<p align="center">
     <img src="https://github.com/onsac/APIs/blob/master/AutenticacaoGrupo.PNG" alt="Tela-autenticação Grupo" >
</p>

<p align="center">
     <img src="https://github.com/onsac/APIs/blob/master/Grupo.PNG" alt="Tela-Grupo" >
</p>
# Material

http://10.70.15.16:8899/api/sigma/material/:grupo_id+classe_id+subclasse_id
http://10.70.15.16:8899/api/sigma/material/:material_id
<p align="center">
     <img src="https://github.com/onsac/APIs/blob/master/AutenticacaoMaterial.PNG" alt="Tela-autenticação Material" >
</p>
<p align="center">
     <img src="https://github.com/onsac/APIs/blob/master/Material.PNG" alt="Tela-Material" >
</p>
# Unidade de Compra
http://10.70.15.16:8899/api/sigma/unidade/:unidade_id
<p align="center">
     <img src="https://github.com/onsac/APIs/blob/master/AutenticacaoUnidadeCompra.PNG" alt="Tela-autenticação Unidade de Compra" >
</p>

<p align="center">
     <img src="https://github.com/onsac/APIs/blob/master/UnidadeCompra.PNG" alt="Tela-Unidade de Compra" >
</p>

# Fornecedor

http://10.70.15.16:8899/api/sigma/fornecedor/:fornecedor_id
<p align="center">
     <img src="https://github.com/onsac/APIs/blob/master/AutenticacaoFornecedor.PNG" alt="Tela-autenticação Fornecedor" >
</p>
<p align="center">
     <img src="https://github.com/onsac/APIs/blob/master/Fornecedor.PNG" alt="Tela-Fornecedor" >
</p>

# Movimento

http://10.70.15.16:8899/api/sigma/movimento/:fornecedor_id/emissao/:emissao_id/nota/:nota_id/serie/:serie_id
<p align="center">
     <img src="https://github.com/onsac/APIs/blob/master/AutenticacaoMovimento.PNG" alt="Tela-autenticação Movimento" >
</p>

<p align="center">      
    <img src="https://github.com/onsac/APIs/blob/master/Movimento.PNG" alt="Tela-Movimento" >
</p>
