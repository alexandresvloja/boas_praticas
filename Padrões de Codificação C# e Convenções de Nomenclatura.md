## Padrões de Codificação C# e Convenções de Nomenclatura

### 1. Notação
    * Camel case (camelCase): A primeira letra da palavra sempre em letra minúscula e depois cada palavra iniciada com letra maiúscula
    * Pascal case (PascalCase): A primeira letra de cada palavra é maiúscula

### 2. Regras de capitalização para identificadores

| Tipo                    |   Notação  | Plural | Prefixo | Sufixo | Abreviação |
|-------------------------|:----------:|:------:|:-------:|:------:|:----------:|
| Classe                  | PascalCase |   não  |   não   |   sim  |     não    |
| Construtor              | PascalCase |   não  |   não   |   sim  |     não    |
| Método                  | PascalCase |   sim  |   não   |   não  |     não    |
| Argumento               |  camelCase |   sim  |   não   |   não  |     sim    |
| Variável local          |  camelCase |   sim  |   não   |   não  |     sim    |
| Constantes              | PascalCase |   não  |   não   |   não  |     não    |
| Atributo (Propriedades) | PascalCase |   sim  |   não   |   não  |     sim    |
| Atributo (Campo)        |  camelCase |   sim  |   não   |   não  |     sim    |
| Enum                    | PascalCase |   não  |   não   |   não  |     não    |
| Enum atributos          | PascalCase |   não  |   não   |   não  |     não    |


#### 2.1 Uso do PascalCase para classe e nome dos método

```cs
public class Calculadora 
{
    
    public void Somar()
    {
        // 
    }

    public void ObterNumeros()
    {
        // 
    }

}

public class CalculadoraDTO { }
```

#### 2.2 Uso do camelCase para argumento e variável local

```cs
public class Calculadora 
{
    
    public void Somar(NumeroInteiro numeroInteiro)
    {
        var resultado = numeroInteiro + 1 
    }

}
```

#### 2.3 Evitar letras maiúsculas para variável do tipo const ou readonly

```cs
// correto
public static const string ParamNotificacao = "PARAM_NOTIFICACAO";

// incorreto
public static const string PARAM_NOTIFICACAO = "PARAM_NOTIFICACAO";
```

#### 2.4 Evitar abreviações desnecessárias, salvo em alguns caso: Id, Xml, Ftp, Uri

```cs
// correto
UsuarioServeloja usuarioServeloja;
Usuario usuarioVendedor;

// incorreto
UsuarioServeloja usuServeloja;

// salvo em alguns casos
UsuarioId usuarioId;
XmlDocument xmlDocument;
```

#### 2.5 Evitar sublinhados em identificadores, salvo no caso de variável privada

```cs
// correto
public UnitOfWork unitOfWork;
private UnitOfWork unitOfWork;

// incorreto
public string nome_aluno;
public string _nomeAluno;

// salvo em alguns casos
private UnitOfWork _unitOfWork;
```

#### 2.6 Use substantivos para nomear as classes e verbos para os métodos

```cs
public class Pessoa 
{

    public void Transar() {

    }

}

public class EnderecoService 
{
   
   public Endereco ObterEnderecoPorPessoa()
   {
       
   }

}

public class Telefone {}
```

#### 2.7 Use prefixo I para nomes de interface


```cs
public interface INotificacaoService {}

public interface IPessoaService {}
```

#### 2.8 Classe completa

```cs
public class Pessoa
{
    public string Nome { get; set; }
    public string Sobrenome { get; set; }

    public Pessoa()
    {
        // 
    }
}
```

#### 2.9 Não utilizar o prefixo e/ou sufixo Enum para criação de Enums

```cs
// correto
public enum TipoTransacao
{
    Debito = 1,
    Credito = 2
}

// incorreto
public enum TipoTransacaoEnum { }
public enum EnumTipoTransacao { }
```

### 3. Organização das classes

#### 3.1 Ordenação

Cada bloco abaixo, deverá ser delimitado por _regions_

1. Constantes
2. Campos
3. Propriedades
4. Construtores
5. Métodos Públicos
6. Métodos Privados

#### 3.2 Documentação dos métodos (se possível)

```cs
/// <summary>
/// Descrição do método público.
/// Este documento permite mostrar como documentar um método
/// </summary>
/// <remarks>
/// Através deste método, é notável quais tipos de itens podemos documentar em um método
/// </remarks>
public void MetodoPublico1()
{

}

/// <summary>
/// Descrição do método público.
/// Este documento permite mostrar como documentar um método
/// </summary>
/// <remarks>
/// Através deste método, é notável quais tipos de itens podemos documentar em um método
/// </remarks>
/// <returns>
/// Também é possível informar a descrição do retorno
/// </returns>
/// <param name="a">Primeiro número</param>
/// <param name="b">Segundo número</param>
public int MetodoPublico2(int a, int b)
{
    return 0;
}
```

#### 3.3 Limitação de argumentos no construtor e método
Evitar (se possível) utilizar mais de 4 argumentos para método e construtor

#### 3.4 Limitação por linhas de código (cada linha)
Evitar que cada linha de código ultrapasse 120 caracteres ou o tamanho padrão da __Tela__.

##### 3.4.1 Exemplo 1
```cs
// correto
public void Metodo(
    int atributo1, int atributo1, int atributo1, 
    int atributo1, int atributo1, int atributo1, int atributo1
)
{

}

// incorreto (caso ultrapasse o tamano de caracteres ou tela)
public void Metodo(int atributo1, int atributo1, int atributo1, int atributo1, int atributo1, int atributo1, int atributo1)
{

}
```

##### 3.4.2 Exemplo 2
```cs
// correto
public void ConsumirOutroMetodo()
{
    var result = Somatorio(
        variabel1, variabel1, variabel1, variabel1, 
        variabel1, variabel1, variabel1, variabel1
    );
}

// incorreto (caso ultrapasse o tamano de caracteres ou tela)
public void ConsumirOutroMetodo()
{
    var result = Somatorio(variabel1, variabel1, variabel1, variabel1, variabel1, variabel1, variabel1, variabel1);
}
```

#### 3.5 Utilização dos regions
* Não utilizar #region ou comentário dentro de métodos. Isso é um sintoma que o bloco comentado é um candidato a se tornar um método privado. Para explicar o método, utilizar a documentação padrão do .NET.
* Não utilizar um #region por método

#### 3.6 Exemplo completo

```cs
public class Classe1
{
    #region Constantes

    private readonly string Const1 = "C1";
    private readonly string Const2 = "C2";
    private readonly string Const3 = "C3";

    #endregion

    #region Campos

    private string campo1;
    private string campo2;
    private string campo3;

    #endregion

    #region Propriedades

    // atributos (propriedades)
    /// <summary>
    /// Descrição de propriedade
    /// </summary>
    public string Prop1 { get; set; }
    public string Prop2 { get; set; }
    public string Prop3 { get; set; }

    #endregion

    #region Construtores

    public TransacaoDTO()
    {

    }

    public TransacaoDTO(int i)
    {

    }

    public TransacaoDTO(int i, int j)
    {

    }

    #endregion

    #region Métodos Públicos

    /// <summary>
    /// Descrição do método público.
    /// Este documento permite mostrar como documentar um método
    /// </summary>
    /// <remarks>
    /// Através deste método, é notável quais tipos de itens podemos documentar em um método
    /// </remarks>
    public void MetodoPublico1()
    {

    }

    /// <summary>
    /// Descrição do método público.
    /// Este documento permite mostrar como documentar um método
    /// </summary>
    /// <remarks>
    /// Através deste método, é notável quais tipos de itens podemos documentar em um método
    /// </remarks>
    /// <returns>
    /// Também é possível informar a descrição do retorno
    /// </returns>
    /// <param name="a">Primeiro número</param>
    /// <param name="b">Segundo número</param>
    public int MetodoPublico2(int a, int b)
    {
        return 0;
    }

    #endregion

    #region Métodos Privados

    private void MetodoPrivado1()
    {

    }

    private void MetodoPrivado2()
    {

    }

    #endregion
}
```



### Referências
* [C# Coding Standards and Naming Conventions](https://github.com/ktaranov/naming-convention/blob/master/C%23%20Coding%20Standards%20and%20Naming%20Conventions.md)
* [The Official raywenderlich.com Swift Style Guide](https://github.com/raywenderlich/swift-style-guide)


