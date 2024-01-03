# Legibilidade

### 1\. Propósito

O propósito de legibilidade é tornar o código compreensível e fácil de ser mantido por outros desenvolvedores. A legibilidade é crucial porque, na maioria das vezes, um código será lido e modificado por diversas pessoas durante seu ciclo de vida.

### 2\. Problemas

A falta de legibilidade no código, decorrente da não aplicação de práticas de Clean Code, apresenta desafios significativos para desenvolvedores e equipes de software. Primeiramente, torna-se complexo realizar manutenções, pois a compreensão e modificação do código se tornam obstáculos. Isso não só prolonga o tempo de desenvolvimento, mas também aumenta os custos associados ao projeto. Além disso, a probabilidade de introduzir erros inadvertidamente aumenta consideravelmente, comprometendo a estabilidade e funcionalidade do sistema. Essa falta de clareza não apenas desacelera a implementação de novas funcionalidades, mas também dificulta a colaboração eficaz entre os membros da equipe. Assim, a legibilidade é crucial para a eficiência, qualidade e sustentabilidade de qualquer projeto de software.

Neste trecho de código temos a convenção chamada de Camel Case inserida. Porém, apesar de ser uma convenção bem aceita na comunidade, o que traz impacto é que neste projeto estamos utilizando Snake Case, que teria um estilo um pouco diferente. A solução tomada para agregar na legibilidade é alterar o código para padronizar com o resto do projeto.

```
class User(AbstractUser):
    email = models.EmailField(max_length=255,unique=True)
    userName = models.CharField(max_length=255,default="user")
    passWord = models.CharField(max_length=255)
    firstName = models.CharField(max_length=255)
    lastName = models.CharField(max_length=255)
    isStaff = models.BooleanField(default=False)
    isActive = models.BooleanField(default=True) 
    tel = models.CharField(max_length=11,null=False,blank=False)
    type = models.ForeignKey(Type, on_delete= models.CASCADE,default="1")
```

### 3\. Solução

Note que a declaração de variáveis é diferente da figura anterior.

```
class User(AbstractUser):
    email = models.EmailField(max_length=255,unique=True)
    username = models.CharField(max_length=255,default="user")
    password = models.CharField(max_length=255)
    first_name = models.CharField(max_length=255)
    last_name = models.CharField(max_length=255)
    is_staff = models.BooleanField(default=False)
    is_active = models.BooleanField(default=True) 
    tel = models.CharField(max_length=11,null=False,blank=False)
    type = models.ForeignKey(Type, on_delete= models.CASCADE,default="1")
```

# Simplicidade

### 1\. Propósito

A simplicidade do Clean Code está diretamente relacionada à escrita de software que seja não apenas enxuto, mas também acessível e fácil de compreender. Essa abordagem simplificada é crucial não apenas durante a fase de desenvolvimento inicial, mas também ao longo do ciclo de vida do software. Simplificar o código não é apenas uma prática recomendada; é uma necessidade que se traduz em eficiência operacional e qualidade aprimorada. Além de facilitar a leitura e compreensão, a simplicidade no Clean Code contribui para a redução da complexidade intrínseca, minimizando elementos como nomes de variáveis confusos e estruturas condicionais aninhadas excessivamente. Dessa forma, promove-se uma maior manutenibilidade do código, facilitando atualizações, correções e evoluções futuras do software. Ao adotar princípios de simplicidade, as equipes de desenvolvimento estão posicionadas para criar sistemas mais robustos, escaláveis e sustentáveis.

### 2\. Problemas

A simplicidade no Clean Code mitiga uma série de problemas relacionados ao desenvolvimento de software. Ao usar dessas práticas de simplificação de código, os desenvolvedores podem enfrentar e resolver vários desafios, incluindo: Dificuldade de leitura e compreensão, dificuldade de manutenção, aumento de bugs e erros, baixa reutilização de código e tempo de desenvolvimento prolongado.

### 3\. Solução

Vamos considerar um exemplo simples em JavaScript para calcular o fatorial de um número. Primeiro, uma implementação menos clara e depois a refatoração seguindo o princípio de simplicidade do Clean Code.

```
function calculateFactorial(number) {
    if (number < 0) return -1; // Retorna -1 para indicar erro
    if (number === 0 || number === 1) return 1;

    let result = 1;
    for (let i = 2; i <= number; i++) {
        result = result * i;
    }
    return result;
}
```

Ao refatorar, focamos em tornar cada parte do código mais legível e autodescritiva, reduzindo complexidades desnecessárias e adicionando comentários para maior clareza.

```
function calculateFactorial(number) {
    // Verifica se o número fornecido é negativo
    if (number < 0) {
        throw new Error('O fatorial não é definido para números negativos.');
    }

    // Casos base: 0! e 1! são 1
    if (number === 0 || number === 1) {
        return 1;
    }

    // Calcula o fatorial usando um loop
    let factorialResult = 1;
    for (let currentNumber = 2; currentNumber <= number; currentNumber++) {
        factorialResult *= currentNumber;
    }

    return factorialResult;
}
```

# Consistência

### 1\. Propósito

Tornar o código forte contribui para a legibilidade, manutenibilidade, colaboração dos desenvolvedores do time e acelera o processo de gestão do projeto. Adotar convenções comuns entre a equipe para nomenclaturas de variáveis/métodos facilita a leitura e compreensão do código. O produto também deve seguir um estilo de codificação consistente (isso inclui a formatação do código, organização de estruturas de controle de fluxo, uso de espaços em branco etc) para manter uma organização de código favorável para futuras manutenções, inclusive, a adoção de padrões de código favorecem esse cenário trazendo um padrão que deve ser seguido e mantido.

### 2\. Problemas

A ausência de simplicidade no código pode trazer vários cenários que atrapalham a saúde do processo de codificação do software. Quando não há preocupação em manter o código simples temos problemas comuns que tem origem em diversas partes do processo de desenvolvimento. Escrita complexa/desnecessária de instruções no sistema podem acarretar a indisponibilidades e consumo elevado de recursos de máquina, provocando necessidades constantes de refatoração. Não seguir convenções de codificação e princípios SOLID causam aumento na dificuldade de interpretação do código produzido (principalmente quando há ausência de comentários significativos), aumentando o tempo levado para as customizações ou operações.

### 3\. Solução

Vamos considerar um exemplo em JavaScript onde temos uma função que calcula o preço total de uma lista de produtos. Primeiro, mostrarei uma implementação que não segue os princípios de consistência do Clean Code e, em seguida, farei a refatoração para torná-la mais consistente.

```
function calculateTotalPrice(productList) {
    let finalPrice = 0;
    for (let i = 0; i < productList.length; i++) {
        const currentProduct = productList[i];
        if (!currentProduct.price) {
            throw new Error('Produto sem preço definido.');
        }
        finalPrice = finalPrice + currentProduct.price;
    }
    return finalPrice.toFixed(2);
}
```

Ao refatorar o código, focamos em adotar consistência na forma como as variáveis são nomeadas, simplificar a lógica para torná-la mais direta e aplicar práticas consistentes em toda a função.

```
function calculateTotalPrice(products) {
    let totalPrice = 0;

    for (const product of products) {
        if (typeof product.price !== 'number') {
            throw new Error('Um dos produtos não possui um preço válido.');
        }
        totalPrice += product.price;
    }

    // Formata o preço total com duas casas decimais
    return totalPrice.toFixed(2);
}
```

Pontos realizados na refatoração:

* Renomeamos a variável productList para products para ser mais conciso e claro.
* Utilizamos um loop for...of para iterar sobre os produtos, o que implifica a lógica e torna o código mais legível.
* Melhoramos a mensagem de erro e a lógica de verificação para garantir que o preço de cada produto seja numérico antes de adicioná-lo ao preço total.

# Comentários

### 1\. Propósito

Os comentários no Clean Code têm função de fornecer informações adicionais que não são claras no código. Eles são usados para orientar sobre a intenção do código, explicar decisões e dar contextos importantes. O principal objetivo do comentário é melhorar a compreensão do código, tornando-o mais legível e facilitando a manutenção.

### 2\. Problemas

Os comentários no código resolvem ou ajudam a mitigar diversos problemas, proporcionando informações adicionais que não são evidentes diretamente no código-fonte. Aqui estão alguns problemas comuns que os comentários podem resolver:

* Explicação da lógica complexa
* Documentação de requisitos não evidentes
* Explicação de decisões
* Alerta sobre possíveis problemas (uso do TODO ou FIXME)
* Esclarecer código complexo ou não intuitivo

### 3\. Solução

Vamos considerar um exemplo em JavaScript que contém comentários que não seguem as práticas recomendadas do Clean Code. Primeiramente, apresentarei o código original com comentários inadequados e, em seguida, farei uma refatoração para torná-los mais eficazes e significativos.

```
// Função para adicionar dois números
function addNumbers(num1, num2) {
    // Inicializa a variável para armazenar a soma
    let result = 0;

    // Verifica se ambos os números são válidos
    if (isNaN(num1) || isNaN(num2)) {
        // Se algum dos números não for válido, retorne 0
        return 0;
    }

    // Realiza a adição dos números
    result = num1 + num2;

    // Retorna o resultado da adição
    return result; // Retorna o resultado
}
```

Ao refatorar os comentários, focaremos em remover redundâncias, tornar os comentários mais descritivos e evitar comentários que não adicionam valor ao entendimento do código.

```
/**
 * Adiciona dois números e retorna o resultado.
 *
 * @param {number} num1 - O primeiro número para adicionar.
 * @param {number} num2 - O segundo número para adicionar.
 * @returns {number} A soma dos dois números fornecidos.
 * @throws {Error} Se algum dos números fornecidos não for um número válido.
 */
function addNumbers(num1, num2) {
    // Verifica se ambos os números são válidos
    if (isNaN(num1) || isNaN(num2)) {
        throw new Error('Ambos os números devem ser válidos para realizar a adição.');
    }

    // Realiza a adição dos números e retorna o resultado
    return num1 + num2;
}
```

Pontos realizados na refatoração:

* Removemos comentários redundantes que apenas repetiam o que o código já claramente indicava.
* Adotamos a utilização de comentários JSDoc para documentar a função, seus parâmetros e seu retorno de maneira clara e padronizada.
* Simplificamos o comentário relacionado à verificação dos números, tornando-o mais conciso e informativo.
* Substituímos o comentário final por uma declaração de retorno mais clara e direta, eliminando a necessidade de um comentário separado para indicar a operação de retorno.

# Evitar duplicação de código

### 1\. Propósito

Evitar a duplicação de código é uma prática benéfica no desenvolvimento de software, visando melhorar a qualidade e eficiência do código. Este princípio tem múltiplos usos e pode ter um impacto positivo na manutenção do código, na legibilidade e na produtividade do desenvolvimento. Evitar a duplicação de código não é apenas uma prática técnica, mas também uma forma estratégica de melhorar a qualidade, a manutenibilidade e a eficiência do desenvolvimento de software. Ao centralizar a lógica e a funcionalidade, os desenvolvedores podem criar códigos mais confiáveis, mais fáceis de entender e de se adaptar às mudanças, resultando em sistemas mais robustos e sustentáveis.

### 2\. Problemas

A falha em eliminar a duplicação de código pode levar a uma série de problemas significativos no desenvolvimento de software. Um dos desafios mais proeminentes é a dificuldade de manutenção do código. Quando partes de lógica iguais ou semelhantes são copiadas para diferentes partes do código, quaisquer modificações, correções de bugs ou atualizações de requisitos exigem muito trabalho porque cada instância duplicada precisa ser tratada individualmente. Isto não só aumenta a probabilidade da criação de erros, mas também torna o processo de manutenção demorado e sujeito a inconsistências.

### 3\. Solução

Para esse fundamento foi realizado a inserção do Resource no código, esse comando é responsável por condensar um conjunto de rotas em apenas uma linha no AdonisJS.

```
  Route.post('/vehicles', 'Vehicles/VehiclesController.store')
  Route.put('/vehicles', 'Vehicles/VehiclesController.update')
  Route.get('/vehicles', 'Vehicles/VehiclesController.index')
  Route.get('/vehicles', 'Vehicles/VehiclesController.show')
  Route.delete('/vehicles', 'Vehicles/VehiclesController.destroy')
```

Abaixo temos o uso do comando para evitar a duplicação de código.

```
  Route.resource('/vehicles', 'Vehicles/VehiclesController')
```

# Testabilidade

### 1\. Propósito

Integrar a testabilidade em código limpo é uma forma fundamental de garantir que o código seja fácil de testar, melhorando a robustez e a confiabilidade do desenvolvimento de software. O objetivo principal desta prática é facilitar a criação e execução eficaz de testes, promovendo uma série de benefícios que impactam diretamente na qualidade e manutenção do código. Além disso, a testabilidade em código limpo visa melhorar a capacidade de manutenção do código. Estruturas de código testáveis tendem a ser mais modulares e menos acopladas, o que facilita a manutenção contínua ao longo do tempo. A possibilidade de criar e executar testes de forma eficaz permite que modificações de código sejam feitas com confiança, proporcionando assim uma evolução segura do software.

### 2\. Problemas

A falta de ênfase na testabilidade, especialmente quando os princípios de código limpo não são implementados, pode levar a uma série de desafios no desenvolvimento de software. Torna-se difícil criar testes automatizados de forma eficiente, resultando em cobertura insuficiente e dificuldade na detecção precoce de problemas. O código que não foi projetado para testabilidade tem maior probabilidade de se tornar frágil, complexo e difícil de manter, aumentando o risco de bugs não detectados durante o desenvolvimento. Isso pode causar problemas na produção, prejudicar a experiência do usuário e exigir soluções rápidas e arriscadas.

Os ciclos de desenvolvimento podem sofrer e tornar-se mais lentos devido à necessidade de extensos testes manuais. Além disso, sem uma estrutura de testes eficiente, a refatoração de código e a rápida identificação de problemas tornam-se uma tarefa difícil. A confiabilidade do software fica comprometida, o que se reflete na reputação do sistema e na confiança dos usuários. O aumento dos custos de manutenção é inevitável, tornando as correções de bugs e a introdução de novos recursos mais caras e arriscadas. A implementação eficaz de práticas como integração e entrega contínuas é difícil porque a automação de testes é fundamental para garantir a qualidade contínua do software. Em resumo, enfatizar a estabilidade desde o início do desenvolvimento é fundamental para mitigar esses problemas e promover um ciclo de desenvolvimento mais ágil, confiável e sustentável.

### 3\. Solução

Adotar bibliotecas de testagem como PHPUnit para PHP, pytest para Python, JUnit para Java entre outros semelhantes.

# Responsabilidade única

### 1\. Propósito

O Princípio de Responsabilidade Única (SRP) em código limpo é crucial para o desenvolvimento de software de qualidade. Defende que cada classe deve ter uma responsabilidade única e claramente definida, simplificando assim a compreensão e manutenção do código. Ao seguir o SRP, as classes tornam-se mais gerenciáveis, reduzindo a complexidade e facilitando alterações futuras. Isso resulta em funcionalidade mais limpa e código mais legível. Além disso, a aplicação do SRP melhora a reutilização, isolando as alterações para evitar efeitos colaterais.

### 2\. Problemas

A não aplicação do Princípio de Responsabilidade Única (SRP) em código limpo pode levar a vários desafios no desenvolvimento de software. Quando uma classe acumula múltiplas responsabilidades, fica complexo entender o código, aumenta o risco de erros e dificulta a manutenção. A falta de clareza afeta a reutilização de código e prejudica a modularidade. Além disso, as interconexões entre diferentes responsabilidades aumentam o acoplamento e tornam o código menos flexível. Resumindo, a não adesão ao SRP resultará em código complexo que será difícil de manter e desenvolver, afetando assim a eficiência do desenvolvimento de software.

### 3\. Solução

Vamos considerar um exemplo onde temos uma função JavaScript que realiza duas responsabilidades: verificar se um número é par e, ao mesmo tempo, imprimir uma mensagem relacionada ao número fornecido. Primeiramente, apresentarei o código original que não segue o princípio da Responsabilidade Única, e depois farei a refatoração para alinhar-se com as práticas do Clean Code.

```
// Função para verificar se um número é par e imprimir uma mensagem
function checkAndPrintNumber(number) {
    if (number % 2 === 0) {
        console.log(`O número ${number} é par.`);
    } else {
        console.log(`O número ${number} não é par.`);
    }
}
```

Para aplicar o princípio da Responsabilidade Única, podemos dividir a função em duas partes distintas: uma função para verificar se o número é par e outra função para imprimir a mensagem correspondente. Isso torna cada função responsável por apenas uma tarefa específica.

```
/**
 * Verifica se um número é par.
 *
 * @param {number} number - O número a ser verificado.
 * @returns {boolean} True se o número for par, caso contrário, false.
 */
function isEven(number) {
    return number % 2 === 0;
}

/**
 * Imprime uma mensagem relacionada ao status de paridade de um número.
 *
 * @param {number} number - O número para o qual a mensagem será impressa.
 */
function printParityMessage(number) {
    if (isEven(number)) {
        console.log(`O número ${number} é par.`);
    } else {
        console.log(`O número ${number} não é par.`);
    }
}
```