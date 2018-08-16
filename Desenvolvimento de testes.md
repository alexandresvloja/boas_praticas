## Desenvolvimento de testes

### Preparação do Ambiente (Visual Studio)

#### 1. Realizar o download da ferramenta _Unit Test Boilerplate Generator_
Essa ferramenta permite a geração de testes com o padrão Microsoft ou NUnit

##### 1.1 Abrindo a janela de extensões e atualizações
[imagem01]: https://image.ibb.co/jSPF8K/1.png "Abrindo a janela de extensões e atualizações"
![alt text][imagem01]

##### 1.2 Fazendo o download da ferramenta _Unit Test Boilerplate Generator_
[imagem02]: https://image.ibb.co/jVyQ8K/2.png "Fazendo o download da ferramenta"
![alt text][imagem02]

#### 2. Estrutura da WebAPI (Principais)
1. ServeLoja.Service/Interfaces
    * Contém as interfaces dos serviços a serem implementados
2. ServeLoja.Business
    * Contém as classes que implementam as interfaces criadas no projeto __ServeLoja.Service__
3. ServeLoja.Api
    * Contém os _Controllers_ que utilizam as classes da camada _Business_ para disponibilizar os métodos para os _Clients_
4. ServeLoja.Tests
    * Contém os testes das implemetações do projeto _ServeLoja.Business_
5. ServeLoja.DTO
    * Contém os objetos de transferência

Assim, o fluxo para implementar algum _Service_, é criar uma _Interface_ em _ServeLoja.Service_, implemetá-la em _ServeLoja.Business_ e disponibilizá-lo em _ServeLoja.Api_

#### 3. Exemplo de teste
* Demanda: Desenvolver um CRUD para a entidade __TB_PARAMETRO__

#### 3.1 Análise
* Realizar uma análise e dimensionar quais DTOs, métodos e outros requisitos são necessários

#### 3.2 Criação dos DTOs (se necessário)
* Criar uma pasta (caso não exista) referente ao serviço
* Dentro da pasta, criar todas as classes necessárias para o uso do _Service_
* Nomeclatura
    * Nome do objeto com sufixo DTO
    * Parametro + DTO
    * ParametroDTO

```cs
namespace ServeLoja.DTO.Parametro
{
    public class ParametroDTO
    {
        public Int64 Id { get; set; }
        public string Nome { get; set; }
        public string Valor { get; set; }
    }
}
```
#### 3.2 Criação da _Interface_
* Nomeclatura
    * Criar uma classe com o nome do serviço, com prefixo I e sufixo Service
    * I + Parametro + Service
    * IParametroService
* Realizar a documentação da _Interface_

```cs
namespace ServeLoja.Service.Interfaces
{
    public interface IParametroService
    {
        /// <summary>
        /// Realiza o cadastro do parâmetro em TB_PARAMETRO
        /// </summary>
        /// <param name="parametro">Dados completo do parâmetro</param>
        void CadastrarParametro(ParametroDTO parametro);

        /// <summary>
        /// Consulta o parametro conforme a Id informada
        /// </summary>
        /// <param name="id">Id do parâmetro</param>
        /// <returns>Parâmetro encontrado</returns>
        ParametroDTO ObterParametroPorId(Int64 id);

        /// <summary>
        /// Realiza a atualização do parâmetro
        /// </summary>
        /// <param name="parametro">Dados completo do parâmetro</param>
        void AtualizarParametro(ParametroDTO parametro);

        /// <summary>
        /// Realiza a remoção do parâmetro conforme a Id informada
        /// </summary>
        /// <param name="id">Id do parâmetro</param>
        void RemoverParametroPorId(Int64 id);
    }
}
```

#### 3.3 Implementação da _Interface_
* Nomeclatura
    * Criar uma classe com o mesmo nome da interface, sem o prefixo I e com sufixo Service
    * Parametro + Service
    * ParametroService

##### 3.3.1 Realizar o AutoGenereted dos métodos

[imagem03]: https://image.ibb.co/bLQuJK/3.png "Realizar o AutoGenereted dos métodos"
![alt text][imagem03]

##### 3.3.2 Classe Gerada

```cs
namespace ServeLoja.Business.Implementations
{
    public class ParametroService : IParametroService
    {
        public void AtualizarParametro(ParametroDTO parametro)
        {
            throw new NotImplementedException();
        }

        public void CadastrarParametro(ParametroDTO parametro)
        {
            throw new NotImplementedException();
        }

        public ParametroDTO ObterParametroPorId(long id)
        {
            throw new NotImplementedException();
        }

        public void RemoverParametroPorId(long id)
        {
            throw new NotImplementedException();
        }
    }
}
```

##### 3.3.3 Realizar o AutoGenereted de testes

##### 3.3.3.1
[imagem04]: https://image.ibb.co/fPzJCe/4.png "Realizar o AutoGenereted de testes"
![alt text][imagem04]

##### 3.3.3.2
[imagem05]: https://image.ibb.co/jPxS5z/5.png "Realizar o AutoGenereted de testes"
![alt text][imagem05]

##### 3.3.3.3 Classe gerada
```cs
namespace ServeLoja.Business.Implementations.Tests
{
    [TestClass()]
    public class ParametroServiceTests
    {
        [TestMethod()]
        public void AtualizarParametroTest()
        {
            Assert.Fail();
        }

        [TestMethod()]
        public void CadastrarParametroTest()
        {
            Assert.Fail();
        }

        [TestMethod()]
        public void ObterParametroPorIdTest()
        {
            Assert.Fail();
        }

        [TestMethod()]
        public void RemoverParametroPorIdTest()
        {
            Assert.Fail();
        }
    }
}
```
##### 3.3.3.4 Estrutura da Solution
[imagem06]: https://image.ibb.co/fu1gXe/6.png "Estrutua da Soluction"
![alt text][imagem06]

#### 3.3 Validando os testes 

#### 3.3.1 Build o projeto

[imagem07]: https://image.ibb.co/g6Btvz/7.png "Build o projeto"
![alt text][imagem07]

#### 3.3.2 Abrir a barra de testes (_Test Explorer_)

[imagem08]: https://image.ibb.co/jBbhoK/8.png "Abrir a barra de testes"
![alt text][imagem08]

#### 3.3.3 Importanto o Service e agrupando métodos por categoria

```cs
namespace ServeLoja.Business.Implementations.Tests
{    
    
    [TestClass()]
    public class ParametroServiceTests
    {
        private IParametroService parametroService;

        [TestInitialize]
        public void Init()
        {
            parametroService = new ParametroService();
        }

        [TestCategory("ParametroService")]
        [TestMethod()]
        public void AtualizarParametroTest()
        {
            Assert.Fail();
        }

        [TestCategory("ParametroService")]
        [TestMethod()]
        public void CadastrarParametroTest()
        {
            Assert.Fail();
        }

        [TestCategory("ParametroService")]
        [TestMethod()]
        public void ObterParametroPorIdTest()
        {
            Assert.Fail();
        }

        [TestCategory("ParametroService")]
        [TestMethod()]
        public void RemoverParametroPorIdTest()
        {
            Assert.Fail();
        }
    }
}
```

#### 3.3.3.1 _Test Explorer_ atualizado

[imagem09]: https://image.ibb.co/efMtvz/9.png "Barra de testes atualizado"
![alt text][imagem09]

#### 3.3.4 Executando todos os testes (inicialmente todos falharão)

[imagem10]: https://image.ibb.co/dNVBFz/12.png "Executando todos os testes"
![alt text][imagem10]

[imagem11]: https://image.ibb.co/njMAaz/10.png "Executando todos os testes"
![alt text][imagem11]

#### 3.3.5 Validando o teste de consulta (_ObterParametroPorIdTest_)

#### 3.3.5.1 Implementação do método ObterParametroPorId em ParametroService
```cs
public ParametroDTO ObterParametroPorId(long id)
{
    var parametro = _uow.TB_PARAMETRORepository.GetByID(id);

    if (parametro == null)
    { throw new CustomMessageException("Parâmetro não encontrado"); }

    return new ParametroDTO
    {
        Id = id,
        Nome = parametro.PAR_TX_DESCRICAO,
        Valor = parametro.PAR_TX
    };
}
```

#### 3.3.5.2 Vaidação do método ObterParametroPorId
```cs
[TestCategory("ParametroService")]
[TestMethod()]
public void ObterParametroPorIdTest()
{
    var id = 1;

    var parametro = parametroService.ObterParametroPorId(id);

    Assert.IsNotNull(parametro);
}

[TestCategory("ParametroService")]
[ExpectedException(typeof(CustomMessageException))]
[TestMethod()]
public void ObterParametroPorIdCustomMessageExceptionTest()
{
    var id = 9999;
    
    var parametro = parametroService.ObterParametroPorId(id);
}
```

#### 3.3.5.2 Executando todos os testes

![alt text][imagem10]

[imagem12]: https://image.ibb.co/jtpA8K/11.png "Executando todos os testes"
![alt text][imagem12]

