# CEPFinder

Pacote que use a API do ViaCEP para busca de logradouro usando CEP.

## Começando

Pra começar a usar este pacote tenha certeza de ter instalado composer na sua maquina,
e que seu projeto siga os padrões de autoload da psr-4.

### Pre Requisitos

[Composer](https://getcomposer.org/download/)

### Instalação

Um passo a passo de como fazer pra funcionar no seu projeto

Instale o pacote dentro do seu projeto usando

```
composer require https://github.com/GustavoFenilli/CEPFinder.git
```

Com o projeto ja registrado no seu autoload

```
use GustavoFenilli\CEPFinder\CEPFinder;

$cepFinder = new CEPFinder();

$cep = '00000000';
if($cepFinder->consult($cep) == 200){
    $cepFinder->getResultJson();
}else{
    throw new \Exception("Erro ao buscar no cep");
}
```

A resposta pode ser recebida em JSON ou XML nos formatos

```
// getResultJson()

{
    "cep":"00000-000",
    "logradouro":"Rua Teste De Resultado",
    "complemento":"",
    "bairro":"Bairro Teste De Resultado",
    "localidade":"Teste",
    "uf":"TT",
    "unidade":"",
    "ibge":"0000000",
    "gia":"0000"
}

// getResultXML() retorna um objeto de \SimpleXMLElement

```

## Uso Avançado

É possivel modificar ou ver os valores recebidos separadamente.

```
use GustavoFenilli\CEPFinder\CEPFinder;

// É possivel instanciar o objeto CEPFinder ja com o CEP desejado

$cepFinder = new CEPFinder(00000000);
if($cepFinder->consult() != 200){
    throw new \Exception("Erro ao buscar no cep");
}

/* Ou em variavel e usar no consult, tenha em mente que usando dentro do consult
** o valor tem prioridade em cima da instancia do objeto, porem ele não sobrescreve
** o valor do objeto
*/

$cep = '00000000';
if($cepFinder->consult($cep) != 200){
    throw new \Exception("Erro ao buscar no cep");
}

// Também é possivel usar o setCep() depois do objeto instanciado
$cepFinder->setCep(00000000);
if($cepFinder->consult() != 200){
    throw new \Exception("Erro ao buscar no cep");
}

// Para pegar valores separadamente use get{NomeAtributo}()

$cep = $cepFinder->getCep();
// 00000000

// Para modificar valores depois de recebidos use set{NomeAtributo}($valor)

$cepFinder->setCep(11111111);
// 11111111

```

Todo e qualquer metodo ou propriedade errada, vai retornar uma \Exception indicando o problema.


## Autores

* **Gustavo Fenilli** - *Criador* - [GustavoFenilli](https://github.com/GustavoFenilli)

## License

Este projeto esta licenciado dentro da licença MIT - Veja em [LICENSE.md](LICENSE.md) arquivo para mais detalhes