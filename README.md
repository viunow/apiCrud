# apiCrud
CRUD simples de API feito com Asp.NET Core, EF Core e com JWT Tokens para a segurança da API.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Instalar os NuGet Packages necessários para rodar esse projeto:

- Microsoft.VisualStudio.Web.CodeGeneration.Design -Version 3.1.4
- Microsoft.EntityFrameworkCore.Tools -Version 3.1.8
- Microsoft.EntityFrameworkCore.SqlServer -Version 3.1.8
- System.IdentityModel.Tokens.Jwt -Version 5.6.0
- Microsoft.AspNetCore.Authentication.JwtBearer -Version 3.1.8

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

SQL Server

Criar o Banco de Dados no SQL Server chamado 'Inventory'

Colar a seguinte Query SQL na janela de Query para criar as tabelas necessárias 'Products' e 'UserInfo':
 
###### Create Table Products(
###### ProductId Int Identity(1,1) Primary Key,
###### Name Varchar(100) Not Null,
###### Category Varchar(100),
###### Color Varchar(20),
###### UnitPrice Decimal Not Null,
###### AvailableQuantity Int Not Null)
###### GO
###### Create Table UserInfo(
###### UserId Int Identity(1,1) Not null Primary Key,
###### FirstName Varchar(30) Not null,
###### LastName Varchar(30) Not null,
###### UserName Varchar(30) Not null,
###### Email Varchar(50) Not null,
###### Password Varchar(20) Not null,
###### CreatedDate DateTime Default(GetDate()) Not Null)
###### GO
###### Insert Into UserInfo(FirstName, LastName, UserName, Email, Password) 
###### Values ('Inventory', 'Admin', 'InventoryAdmin', 'InventoryAdmin@abc.com', '$admin@2017')

- Após isso, conectar o Banco de Dados na aplicação.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Package Manager Console

Colar e rodar o seguinte comando no PMC para criar o contexto do banco de dados e entidades das tabelas. Esse comendo vai criar apenas as classes para as tabelas que possuem a primary key:

Scaffold-DbContext “Server=******;Database=Inventory;Integrated Security=True” Microsoft.EntityFrameworkCore.SqlServer -OutputDir Models

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Endpoints no Postman:

[POST] Create product
######  URL: https://localhost:44346/api/products
  No Body selecionar RAW e o tipo JSON
  ```
  {
      "name" : "Product Name",
      "category" : "Category ABC",
      "color" : "blue",
      "unitPrice" : 1000,
      "availableQuantity" : 50
  }
  ```
-------------------------------------------------------------
[GET] Return product
  URL: https://localhost:44346/api/products
-------------------------------------------------------------
[PUT] Update product
  URL: https://localhost:44346/api/products/{id}
  No Body selecionar RAW e o tipo JSON
  ```
  {
    "productId": {id}
    "name": "Other Product Name",
    "category": "Category ABC",
    "color": "yellow",
    "unitPrice": 1000,
    "availableQuantity": 50
  }
  ```
-------------------------------------------------------------  
[DEL] Delete product
  URL: https://localhost:44346/api/products/2
-------------------------------------------------------------  
[POST] Access token
  URL: https://localhost:44346/api/token
  No Body selecionar RAW e o tipo JSON\
  ```
  {
    "Email" : "InventoryAdmin@abc.com",
    "Password" : "$admin@2017"
  }
  ```

Copiar o Token gerado e passar no Authorization do GET de Return product para autenticar o usuário, senão é retornado Status 401 Unauthorized.
 
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 
  
  
  
  
  
  
  
