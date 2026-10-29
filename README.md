<p align="center">
  <img src="assets/banner.png" alt="BuyCart — Carrinho de Compras" width="100%">
</p>

<p align="center">
  Sistema web em ASP.NET Core MVC para organização de listas de compras por categoria, controle de usuários e geração de relatórios em PDF.
</p>

<p align="center">
  <img alt="ASP.NET Core" src="https://img.shields.io/badge/ASP.NET_Core-MVC-C52E36?style=for-the-badge&logo=dotnet&logoColor=white">
  <img alt="Entity Framework" src="https://img.shields.io/badge/EF_Core-SQL_Server-11120F?style=for-the-badge&logo=microsoftsqlserver&logoColor=C52E36">
  <a href="http://buy-cart.somee.com/"><img alt="Demo" src="https://img.shields.io/badge/Demo-Online-18181B?style=for-the-badge"></a>
</p>

## Sobre o projeto

O **BuyCart** (Carrinho-de-Compras) é uma aplicação web desenvolvida em **C# e ASP.NET Core MVC** para resolver a organização prática de compras cotidianas. Em vez de anotar itens de forma dispersa, o usuário autentica-se na plataforma, estrutura suas categorias, adiciona itens com quantidades e valores e acompanha o resumo consolidado do carrinho.

Além do fluxo completo de persistência relacional com **Entity Framework Core e SQL Server**, o sistema conta com um controlador dedicado para exportação da lista de compras em **PDF**, facilitando o compartilhamento ou impressão do orçamento planejado.

## Principais recursos

| Recurso | Como funciona |
|---|---|
| Autenticação de usuários | AccountController com LoginViewModel e RegisterViewModel para acesso individualizado. |
| Gestão de categorias | CategoriaController permite criar e organizar setores de produtos (mercado, casa, tecnologia, etc.). |
| Controle de itens e lista | ListaController gerencia a inclusão, edição, marcação e remoção de ItemCompra. |
| Resumo financeiro | ResumoViewModel consolida totais de itens e valores acumulados no carrinho. |
| Exportação para PDF | PDFController transforma os itens selecionados em um documento pronto para download. |
| Migrações versionadas | Histórico de banco de dados gerenciado pelo EF Core Migrations (AppDbContext). |

## Tecnologias

<p>
  <img alt="C#" src="https://img.shields.io/badge/C%23-C52E36?style=flat-square&logo=dotnet&logoColor=white">
  <img alt=".NET 8" src="https://img.shields.io/badge/.NET_8-11120F?style=flat-square&logo=dotnet&logoColor=C52E36">
  <img alt="ASP.NET Core MVC" src="https://img.shields.io/badge/ASP.NET_Core_MVC-C52E36?style=flat-square&logo=dotnet&logoColor=white">
  <img alt="Entity Framework Core" src="https://img.shields.io/badge/EF_Core-11120F?style=flat-square&logo=dotnet&logoColor=C52E36">
  <img alt="SQL Server" src="https://img.shields.io/badge/SQL_Server-C52E36?style=flat-square&logo=microsoftsqlserver&logoColor=white">
  <img alt="Razor" src="https://img.shields.io/badge/Razor_Views-11120F?style=flat-square&logo=html5&logoColor=C52E36">
</p>

- **C# e ASP.NET Core MVC** na arquitetura de controladores, modelos e páginas Razor;
- **Entity Framework Core (AppDbContext)** para mapeamento objeto-relacional e migrações;
- **SQL Server** como banco de dados relacional para usuários, categorias e itens;
- **ViewModels dedicadas** (LoginViewModel, RegisterViewModel, ResumoViewModel) para desacoplar as telas das entidades de banco.

## Arquitetura

`mermaid
flowchart LR
    A[Navegador / Razor Views] --> B[Controllers MVC]
    B --> C[Account · Categoria · Lista · PDF]
    C --> D[AppDbContext / EF Core]
    D --> E[(SQL Server)]
    C --> F[Documento PDF]
`

As requisições passam pelos controladores especializados, que validam os dados através de ViewModels e persistem o estado no SQL Server por meio do AppDbContext.

## Estrutura do repositório

`	ext
Carrinho-de-Compras/
├── assets/
│   ├── banner.png                  Banner principal BuyCart
│   └── project-animal.png          Símbolo do esquilo
├── Buy_Cart/
│   ├── Controllers/                Account, Categoria, Home, Lista e PDF
│   ├── Data/AppDbContext.cs        Contexto do Entity Framework Core
│   ├── Migrations/                 Esquema versionado do banco de dados
│   ├── Models/                     Usuario, Categoria, ItemCompra
│   ├── ViewModels/                 Modelos de transferência para as telas
│   ├── Views/                      Interfaces Razor (.cshtml)
│   └── Program.cs                  Configuração de serviços e pipeline HTTP
├── Buy_Cart.sln                    Solução Visual Studio
└── README.md
`

## Executando o código

1. Clone o repositório:
   `powershell
   git clone https://github.com/arthurlynow098/Carrinho-de-Compras.git
   cd Carrinho-de-Compras
   `
2. Configure a string de conexão do seu **SQL Server** em Buy_Cart/appsettings.json.
3. Aplique as migrações e inicie o servidor:
   `powershell
   dotnet ef database update --project Buy_Cart
   dotnet run --project Buy_Cart/Buy_Cart.csproj
   `

## Decisões técnicas

- **Separação entre Models e ViewModels:** impede overposting nos formulários de autenticação e entrega exatamente os dados agregados que a tela de resumo precisa.
- **Exportação integrada:** geração de PDF no próprio back-end garante fidelidade dos preços e quantidades registrados na sessão do usuário.

---

<p align="center"><sub>Estudo · construção · evolução</sub><br><a href="https://github.com/arthurlynow098">Perfil</a> · <a href="https://arthurentsev.vercel.app/">Portfólio</a> · <a href="https://www.linkedin.com/in/entsevarthur/">LinkedIn</a></p>
