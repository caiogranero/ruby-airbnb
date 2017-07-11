# Ruby Style Guide

O guia de estilo paras Ruby do Airbnb.

Inspirado por [GitHub's guide](https://web.archive.org/web/20160410033955/https://github.com/styleguide/ruby) e [Bozhidar Batsov's guide][bbatsov-ruby].

Airbnb também mantém o [Guia de estilo para JavaScript][airbnb-javascript].

## Índice
  1. [Espaços em branco](#espaços-em-branco)
    1. [Indentação](#indentação)
    1. [Linha única](#linha-única)
    1. [Novas linhas](#novas-linhas)
  1. [Tamanho das linhas](#tamanho-das-linhas)
  1. [Comentários](#comentários)
    1. [Comentários de arquivos/classes](#comentários-de-arquivosclasses)
    1. [Comentários de funções](#comentários-de-funções)
    1. [Comentários de blocos e linhas únicas](#comentários-de-blocos-e-linhas-únicas)
    1. [Pontuação, ortografia e gramática](#pontuação-ortografia-e-gramática)
    1. [Comentários de pendências](#comentários-de-pendências)
    1. [Códigos comentado](#códigos-comentado)
  1. [Métodos](#métodos)
    1. [Definição de métodos](#definição-de-métodos)
    1. [Chamada de métodos](#chamada-de-métodos)
  1. [Expressões condicionais](#expressões-condicionais)
    1. [Palavras condicionais](#palavras-condicionais)
    1. [Operador ternário](#operador-ternário)
    1. [Condições longas](#condições-longas) ////
  1. [Sintaxe](#sintaxe)
  1. [Nomenclatura](#nomenclatura)
  1. [Classes](#classes)
  1. [Exceções](#exceções)
  1. [Coleções](#coleções)
  1. [Textos](#textos)
  1. [Expressões regulares](#expressões-regulares)
  1. [Notação de porcentagem](#notação-de-porcentagem)
  1. [Rails](#rails)
    1. [Escopo](#escopo)
  1. [Seja consistente](#seja-consistente)
  1. [Tradução](#Tradução)

## Espaços em branco

### Indentação

* <a name="identacao-padrao"></a>Use tabs com dois espaçamento.<sup>[[link](#identacao-padrao)]</sup>

* <a name="indente-when-e-case"></a>Indente `when` da mesma forma que `case`.
    <sup>[[link](#indente-when-e-case)]</sup>

    ```ruby
    case
    when song.name == 'Misty'
      puts 'Not again!'
    when song.duration > 120
      puts 'Too long!'
    when Time.now.hour > 21
      puts "It's too late"
    else
      song.play
    end

    kind = case year
           when 1850..1889 then 'Blues'
           when 1890..1909 then 'Ragtime'
           when 1910..1929 then 'New Orleans Jazz'
           when 1930..1939 then 'Swing'
           when 1940..1950 then 'Bebop'
           else 'Jazz'
           end
    ```

* <a name="alinhar-parametros-de-funcao"></a>Alinhe todos os parâmetros de função ou na mesma linha ou um por linha.<sup>[[link](#alinhar-parametros-de-funcao)]</sup>

    ```ruby
    # ruim
    def self.create_translation(phrase_id, phrase_key, target_locale,
                                value, user_id, do_xss_check, allow_verification)
      ...
    end

    # bom
    def self.create_translation(phrase_id,
                                phrase_key,
                                target_locale,
                                value,
                                user_id,
                                do_xss_check,
                                allow_verification)
      ...
    end

    # bom
    def self.create_translation(
      phrase_id,
      phrase_key,
      target_locale,
      value,
      user_id,
      do_xss_check,
      allow_verification
    )
      ...
    end
    ```

* <a name="indente-multi-line-bool"></a>Indente continuamente múltiplas linhas de expressões condicionais.<sup>[[link](#indente-multi-linhas-bool)]</sup>

    ```ruby
    # ruim
    def is_eligible?(user)
      Trebuchet.current.launch?(ProgramEligibilityHelper::PROGRAM_TREBUCHET_FLAG) &&
      is_in_program?(user) &&
      program_not_expired
    end

    # bom
    def is_eligible?(user)
      Trebuchet.current.launch?(ProgramEligibilityHelper::PROGRAM_TREBUCHET_FLAG) &&
        is_in_program?(user) &&
        program_not_expired
    end
    ```

### Linha única

* <a name="espacos-perdido"></a>Nunca deixe espaços em branco soltos.
    <sup>[[link](#espacos-perdido)]</sup>

* <a name="espaco-antes-comentario"></a>Quando fizer comentários em apenas uma, inclua um espaço entre o fim do código e o começo do comentário.
    <sup>[[link](#espaco-antes-comentario)]</sup>

    ```ruby
    # ruim
    result = func(a, b)# Nós podemos alterar b para c

    # bom
    result = func(a, b) # Nós podemos alterar b para c
    ```

* <a name="operadores-espaco"></a> Use espaço ao redor de operadores e depois de virgulas, dois pontos, ponto e virgula e ao redor de `{` e antes de `}`. 
    <sup>[[link](#operadores-espaco)]</sup>

    ```ruby
    sum = 1 + 2
    a, b = 1, 2
    1 > 2 ? true : false; puts 'Hi'
    [1, 2, 3].each { |e| puts e }
    ```

* <a name="sem-espaco-antes-virgula"></a>Nunca inclua um espaço antes de uma virgula.
    <sup>[[link](#sem-espaco-antes-virgula)]</sup>

    ```ruby
    result = func(a, b)
    ```

* <a name="bloco-espaco-parametro"></a>Não inclua espaço dentro de blocos de parâmetros. Inclua um espaço entre parâmetros dentro de um bloco. Inclua um espaço fora do bloco de parâmetro.
    <sup>[[link](#bloco-espaco-parametro")]</sup>

    ```ruby
    # ruim
    {}.each { | x,  y |puts x }

    # bom
    {}.each { |x, y| puts x }
    ```

* <a name="sem-espaco-depois-!"></a>Não deixe espaço entre `!` e a variável. 
    <sup>[[link](#sem-espaco-depois-!)]</sup>

    ```ruby
    !something
    ```

* <a name="sem-espaco-chave"></a>Não use espaço depois de `(`,`[` ou antes de `]`, `)`.
    <sup>[[link](#sem-espaco-chave)]</sup>

    ```ruby
    some(arg).other
    [1, 2, 3].length
    ```

* <a name="sem-espaco-textos-variaveis"></a>Não use espaços quando utilizar textos com variáveis.<sup>[[link](#sem-espaco-textos-variaveis)]</sup>

    ```ruby
    # ruim
    var = "This #{foobar} is interpolated."

    # bom
    var = "This #{foobar} is interpolated."
    ```

* <a name="sem-espaco-range-numeros"></a>Não use espaços em range númericos.
    <sup>[[link](#sem-espaco-range-numeros)]</sup>

    ```ruby
    # ruim
    (0 ... coll).each do |item|

    # bom
    (0...coll).each do |item|
    ```

### Novas linhas

* <a name="if-multiplas-novas-linhas"></a>Adiciona uma nova linha depois da condição `if` usada com múltiplas linhas para ajudar diferenciar entre condições e o conteúdo.
    <sup>[[link](#if-multiplas-novas-linhas)]</sup>

    ```ruby
    if @reservation_alteration.checkin == @reservation.start_date &&
       @reservation_alteration.checkout == (@reservation.start_date + @reservation.nights)

      redirect_to_alteration @reservation_alteration
    end
    ```

* <a name="nova-linha-depois-de-condicionais"></a>Adiciona uma nova linha depois de condicionais, blocos, switch-case, etc.<sup>[[link](#nova-linha-depois-de-condicionais)]</sup>

    ```ruby
    if robot.is_awesome?
      send_robot_present
    end

    robot.add_trait(:human_like_intelligence)
    ```

* <a name="nova-linha-diferente-conteudos"></a>Não quebre linhas entre diferentes conteúdos (Como classes ou módulos).
    <sup>[[link](#nova-linha-diferente-conteudos)]</sup>

    ```ruby
    # ruim
    class Foo

      def bar
        # conteúdo omitido
      end

    end

    # bom
    class Foo
      def bar
        # conteúdo omitido
      end
    end
    ```

* <a name="nova-linha-entre-metodos"></a>Inclua *APENAS* uma nova linha entre métodos.
    <sup>[[link](#nova-linha-entre-metodos)]</sup>

    ```ruby
    def a
    end

    def b
    end
    ```

* <a name="linha-vazia-blocos-logicos"></a>Use apenas uma linha como espaçamento entre blocos lógicos.
    <sup>[[link](#linha-vazia-blocos-logicos)]</sup>

    ```ruby
    def transformorize_car
      car = manufacture(options)
      t = transformer(robot, disguise)

      car.after_market_mod!
      t.transform(car)
      car.assign_cool_name!

      fleet.add(car)
      car
    end
    ```

* <a name="finaliza-nova-linha"></a>Finalize cada linha com uma nova linha. Não inclua múltiplas linhas no fim do seu arquivo.
    <sup>[[link](#finaliza-nova-linha)]</sup>

## Tamanho das linhas

* Mantenha cada linha do código com um tamanho viável para leitura. A não ser que você tenha uma razão para não fazer, mantenha linhas com menos de 100 caracteres.
  ([rationale](./rationales.md#line-length))<sup>
  [[link](#line-length)]</sup>

## Comentários

> Apesar de ser chato de escrever, comentários são extremamente importantes para manter o código viável para leitura. As regras a seguir descrevem o que você devería comentar e aonde. Mas lembre-se: Enquanto comentários são muito importantes, um bom código é auto-documentável. Definir nomes com sentido para variáveis e métodos são melhores do que usar nomes sem significado que você precise explicar através de comentários.

> Enquanto estiver escrevendo seus comentários, escreva para o seu público: O próximo colaborador que irá precisar entender seu código. Seja generoso - o próximo pode ser você!

&mdash;[Google C++ Style Guide][google-c++]

Partes dessa seção foram fortemente emprestados dos guias de estilo do Google
[C++][google-c++-comments] e [Python][google-python-comments].

### Comentários de arquivos/classes

Toda definição de classe deve ter um comentário que descreve o que ela faz e como usa-la.

Um arquivo que contém nenhuma ou alguma classe deve ter um comentário no seu ínicio descrevendo o seu conteúdo.

```ruby
# Conversão automática de uma localização para outra que seja possível, como 
# América para Inglês britanico.
module Translation
  # Classe para conversão entre textos entre localizações similares.
  # Por enquanto, somente conversões entre inglês americano -> Britânico,
  # Canadense, Australiano, Nova Zelandia e variações são possíveis.
  class PrimAndProper
    def initialize
      @converters = { :en => { :"en-AU" => AmericanToAustralian.new,
                               :"en-CA" => AmericanToCanadian.new,
                               :"en-GB" => AmericanToBritish.new,
                               :"en-NZ" => AmericanToKiwi.new,
                             } }
    end

  ...

  # Permite transformar em inglês americano o que é comum entre 
  # todas as outras colonias inglesas.
  class AmericanToColonial
    ...
  end

  # Converte inglês americano para inglês britânico.
  # Para outras variações de colonias inglesas, altere "apartment" para "flat".
  class AmericanToBritish < AmericanToColonial
    ...
  end
```

Todos os arquivos, incluindo arquivos de configuração e base de dados, devem ter comentários.

```ruby
# Lista de variações de pronuncias de America-para-Britânico.
#
# Essa lista é feita com
# lib/tasks/list_american_to_british_spelling_variants.rake.
#
# Ela contém palavras com variações de pronuncias:
#   [trave]led/lled, [real]ize/ise, [flav]or/our, [cent]er/re, plus
# and these extras:
#   learned/learnt, practices/practises, airplane/aeroplane, ...

sectarianizes: sectarianises
neutralization: neutralisation
...
```

### Comentários de funções

Toda declaração de função deve ter comentários imediatamente antes de sua definição, que descreva o que a função faz e como deve ser usada. Esse comentário deve ser preferivel ("Abre os arquivos") ao invés de ("Abra o arquivo"); o comentário descreve a função, não diz para a função o que fazer. No geral, esse comentário não descreve como a função funciona. Por outro lado, isso deve ser deixado para comentários dentro do código da função.

Toda função deve mencionar o que são as variáveis de entrada e saída, a não ser que siga todos os critérios abaixo:

* Não é visivel externamente
* Muito pequena
* Óbvio

Você pode usar o formato que desejaar. Em Ruby, duas documentações populares de função são: [TomDoc](http://tomdoc.org/) e
[YARD](http://rubydoc.info/docs/yard/file/docs/GettingStarted.md). Você também pode apenas escrever algo conciso:

```ruby
# Retorna o localização de fallback para a variável the_locale.
# Se opts[:exclude_default] estiver setado, a localização padrão, 
# que sempre é a ultima posição da lista, será excluída.
#
# Por exemplo:
#   fallbacks_for(:"pt-BR")
#     => [:"pt-BR", :pt, :en]
#   fallbacks_for(:"pt-BR", :exclude_default => true)
#     => [:"pt-BR", :pt]
def fallbacks_for(the_locale, opts = {})
  ...
end
```

### Comentários de blocos e linhas únicas

Outro lugar para ter comentários é em partes importantes do seu código. Se você vai ter que explicar durante o code review, é melhor comentar agora.
Operações complicadas merecem algumas linhas de comentários antes do seu começo. Operações não óbvias, ganham comentários no fim da linha.

```ruby
def fallbacks_for(the_locale, opts = {})
  # dup() produz um array que podemos alterar
  ret = @fallbacks[the_locale].dup

  # Temos que assumir duas coisas aqui:
  # 1) Há apenas uma localização padrão.
  # 2) O localização padrão é um idioma. (Como :pt, e não :"pt-BR".)
  if opts[:exclude_default] &&
      ret.last == default_locale &&
      ret.last != language_from_locale(the_locale)
    ret.pop
  end

  ret
end
```

Por outro lado, nunca descreva seu comentário. Assuma que a pessoa lendo o código conhece a linguagem (e não o que você está fazendo) melhor que você.

<a name="sem-blocos-de-comentarios"></a>Relacionado: Não use blocos de comentários. Eles não podem ser precedidos por espaços e não são fáceis de encaixar no código se comparado a comentários padrões.
  <sup>[[link](#sem-blocos-de-comentarios)]</sup>

  ```ruby
  # ruim
  =begin
  comment line
  another comment line
  =end

  # bom
  # comentários aqui
  # mais comentários
  ```

### Pontuação, ortografia e gramática

Preste atenção para pontuação, ortografia e gramática; é mais fácil ler comentários bem escritos do que comentários mal escritos.

Comentários devem ser tão fáceis de ler quanto textos de narrativa, com suas definidas pontuações e letras maiusculas. Em muitos casos, completar as frases é mais fácil de ler do que pedaços de textos. Comentários pequenos, como comentários no fim da linha do código, podem muitas vezes serem menos formais, mas você deve ser consistente com seu padrão.

Apesar que pode ser frustante ter passar por um code review que aponte que você está usando virgula ao invés de ponto e virgula, é muito importante que seu código mantenha um nível alto de clareza e leitura. Pontuação, gramática e ortografia adequadas, ajudam a alcançar o objetivo.

### Comentários de pendências

Comentários de pendências no código são temporários, uma solução a curto prazo.

Comentários de pendências devem incluir a palavra TODO, seguido pelo nome completo da pessoa que conhece mais do problema. Dois pontos é opcional. Um comentário explicando qual o requisito dessa tarefa é obrigatório. A principal motivação de ter um comentário de pendência é ser fácil de encontrar a pessoa que está sendo mencionada. Esse comentário não é um compromisso para a pessoa  resolver o problema. Tanto que, quando você cria um comentário de pendência, costuma ser o seu nome que será mencionado.

```ruby
  # ruim
  # TODO(RS): Use o devido nome para essa variável.

  # ruim
  # TODO(drumm3rz4lyfe): Use o devido nome para essa variável.

  # bom
  # TODO(Ringo Starr): Use o devido nome para essa variável.
```

### Códigos comentado

* <a name="codigo-comentado"></a>NUNCA deixe trechos de códigos comentados no seu código.
    <sup>[[link](#codigo-comentado)]</sup>

## Métodos

### Definição de métodos

* <a name="parenteses-def-metodos"></a>Crie `def` com parênteses quando contém parâmetros. Não use parênteses quando o metodo não aceita parâmetros.
  <sup>[[link](#parenteses-def-metodos)]</sup>

     ```ruby
     def metodo
       # sem conteudo
     end

     def metodo_com_parametros(arg1, arg2)
       # sem conteudo
     end
     ```

* <a name="sem-argumentos-padrao"></a> Não use argumentos de definição de valores. Use argumentos (se disponível - Ruby 2.0 ou posterior) ou um hash de opções.<sup>[[link](#sem-argumentos-padrao)]</sup>

    ```ruby
    # ruim
    def obliterate(things, gently = true, except = [], at = Time.now)
      ...
    end

    # bom
    def obliterate(things, gently: true, except: [], at: Time.now)
      ...
    end

    # bom
    def obliterate(things, options = {})
      options = {
        :gently => true, # remove com um soft-delete
        :except => [], # não remove esses itens
        :at => Time.now, # define o horário de remoção
      }.merge(options)

      ...
    end
    ```

* <a name="metodo-de-linha-unica"></a>Evite escrever metodos em uma linha só. Apesar de ser populares, existe algumas pecularidades que fazem dessa abordagem indesejável.
    <sup>[[link](#metodo-de-linha-unica)]</sup>

    ```ruby
    # ruim
    def too_much; something; something_else; end

    # bom
    def some_method
      # conteudo
    end
    ```

### Chamada de métodos

**Uso do parênteses** para uma chamada de método:

* <a name="retorna-valor-parenteses"></a>Se o método retorna um valor.
    <sup>[[link](#retorna-valor-parenteses)]</sup>

    ```ruby
    # ruim
    @current_user = User.find_by_id 1964192

    # bom
    @current_user = User.find_by_id(1964192)
    ```

* <a name="parenteses-primeiro-argumento"></a>Se o primeiro argumento do método necessita de parenteses.<sup>[[link](#parenteses-primeiro-argumento)]</sup>

    ```ruby
    # ruim
    put! (x + y) % len, value

    # bom
    put!((x + y) % len, value)
    ```

* <a name="espaco-chamada-metodo"></a>Nunca coloque espaço entre o nome do método e parenteses.<sup>[[link](#espaco-chamada-metodo)]</sup>

    ```ruby
    # bad
    f (3 + 2) + 1

    # good
    f(3 + 2) + 1
    ```

* <a name="sem-parenteses-argumentos"></a>**Não use parênteses** para uma chamada de método se o método aceita argumentos.<sup>[[link](#sem-parenteses-argumentos)]</sup>

    ```ruby
    # ruim
    nil?()

    # bom
    nil?
    ```

* <a name="sem-parenteses-no-retorno"></a>Se o método não retorna um valor (ou não nos importamos com o retorno), o parênteses é opcional. (Com exceção se o argumento ocupa múltiplas linhas, parênteses podem ajudar a leitura.)
    <sup>[[link](#sem-parenteses-no-retorno)]</sup>

    ```ruby
    # bom
    render(:partial => 'foo')

    # bom
    render :partial => 'foo'
    ```

Em ambos os casos:

* <a name="hash-sem-chaves"></a>Se o método aceita um hash de opções como último argumento, não use `{` `}` durante a chamada.
    <sup>[[link](#hash-sem-chaves)]</sup>

    ```ruby
    # ruim
    get '/v1/reservations', { :id => 54875 }

    # bom
    get '/v1/reservations', :id => 54875
    ```

## Expressões condicionais

### Palavras condicionais

* <a name="multi-if-then"></a>Nunca use `then` com `if/unless` em múltiplas linhas.
    <sup>[[link](#multi-if-then)]</sup>

    ```ruby
    # ruim
    if some_condition then
      ...
    end

    # bom
    if some_condition
      ...
    end
    ```

* <a name="multi-while-until"></a>Nunca use `do` com `while` ou `until` em múltiplas linhas. <sup>[[link](#multi-while-until)]</sup>

    ```ruby
    # ruim
    while x > 5 do
      ...
    end

    until x > 5 do
      ...
    end

    # bom
    while x > 5
      ...
    end

    until x > 5
      ...
    end
    ```

* <a name="no-and-or"></a>As palavras `and`, `or`, e `not` estão banidas. Não as use. Ao invés, sempre use `&&`, `||`, e `!`.
    <sup>[[link](#no-and-or)]</sup>

* <a name="somente-use-simples-if-unless"></a>Modificar `if/unless` é válido quando o conteúdo é pequeno, a condição é simples e tudo se encaixa em uma linha. Caso contrário, evite modificar `if/unless`.
    <sup>[[link](#somente-use-simples-if-unless)]</sup>

    ```ruby
    # ruim - isso não se encaixa em uma linha
    add_trebuchet_experiments_on_page(request_opts[:trebuchet_experiments_on_page]) if request_opts[:trebuchet_experiments_on_page] && !request_opts[:trebuchet_experiments_on_page].empty?

    # okay
    if request_opts[:trebuchet_experiments_on_page] &&
         !request_opts[:trebuchet_experiments_on_page].empty?

      add_trebuchet_experiments_on_page(request_opts[:trebuchet_experiments_on_page])
    end

    # ruim - isso é complexo e merece multiplas linhas e comentários
    parts[i] = part.to_i(INTEGER_BASE) if !part.nil? && [0, 2, 3].include?(i)

    # okay
    return if reconciled?
    ```

* <a name="nao-use-unless-com-else"></a>Nunca use `unless` com `else`. Reescreva com o uso de `if`.<sup>[[link](#nao-use-unless-com-else)]</sup>

    ```ruby
    # ruim
    unless success?
      puts 'failure'
    else
      puts 'success'
    end

    # bom
    if success?
      puts 'success'
    else
      puts 'failure'
    end
    ```

* <a name="unless-com-multiplas-condicoes"></a>Evite usar `unless``com múltiplas condições.<sup>[[link](#unless-com-multiplas-condicoes)]</sup>

    ```ruby
      # bad
      unless foo? && bar?
        ...
      end

      # okay
      if !(foo? && bar?)
        ...
      end
    ```

* <a name="unless-com-operador-de-comparacao"></a>Evite usar `unless` com operadores de comparação. Use `if`  nesse caso.<sup>[[link](#unless-com-operador-de-comparacao)]</sup>

    ```ruby     
      # ruim
      unless x == 10
        ...
      end
      
      # bom
      if x != 10
        ...
      end
      
      # ruim
      unless x < 10
        ...
      end
      
      # bom
      if x >= 10
        ...
      end
      
      # ok
      unless x === 10
        ...
      end
    ```

* <a name="parenteses-com-condicoes"></a>Não use parênteses nas condições em `if/unless/while`.
    <sup>[[link](#parenteses-com-condicoes)]</sup>

    ```ruby
    # ruim
    if (x > 10)
      ...
    end

    # bom
    if x > 10
      ...
    end

    ```

### Operador ternário

* <a name="evite-operadores-ternarios-complexos"></a>Evite utilizar operadores ternários (`?:`) a não ser que a condição seja extremamente trivial. Por outro lado, use o operador ternário (`?:`) ao invés de `if/then/else/end` para condições de linhas únicas.<sup>[[link](#evite-operadores-ternarios-complexos)]</sup>

    ```ruby
    # ruim
    result = if some_condition then something else something_else end

    # bom
    result = some_condition ? something : something_else
    ```

* <a name="sem-operadores-ternarios-longos"></a>Use uma expressão por bloco em operadores ternários. Isso significa que operadores ternários não devem ser longos. Prefira `if/else` nesses casos.<sup>[[link](#sem-operadores-ternarios-longos)]</sup>

    ```ruby
    # ruim
    some_condition ? (nested_condition ? nested_something : nested_something_else) : something_else

    # bom
    if some_condition
      nested_condition ? nested_something : nested_something_else
    else
      something_else
    end
    ```

* <a name="operador-ternario-condicoes-simples"></a>Evite multiplas condições em operadores ternários. Operadores ternários são melhor usados em condições simples. <sup>[[link](#operador-ternario-condicoes-simples)]</sup>

* <a name="sem-multiplas-linhas-ternario"></a>Evite multiplas linhas com o operador ternário `?:`, nesses casos, use `if/then/else/end`.
    <sup>[[link](#sem-multiplas-linhas-ternario)]</sup>

    ```ruby
    # ruim
    some_really_long_condition_that_might_make_you_want_to_split_lines ?
      something : something_else

    # bom
    if some_really_long_condition_that_might_make_you_want_to_split_lines
      something
    else
      something_else
    end
    ```

### Condições longas

* <a name="sem-condicoes-longas"></a>
  Evite utilizar condições muito longas para controle do fluxo.
  ([Leia mais sobre isso][avoid-else-return-early].) <sup>[[link](#sem-condicoes-longas)]</sup>
  
  Prefira utilizar uma clause guard quando pode receber um dado inválida. Uma guard clause é uma condição no topo de uma função que retorna assim que possível. 
  
  Os principios dessa clausula, são:
  * Retorna assim que sua função sabe que não pode fazer mais nada.
  * Diminui o tamanho do código. Isso faz o código ser mais fácil de ler e necessita menos atenção em relação a blocos `if/else`.
  * O fluxo principal deve ser o último a ser validado.

  ```ruby
  # ruim
  def compute
    server = find_server
    if server
      client = server.client
      if client
        request = client.make_request
        if request
           process_request(request)
        end
      end
    end
  end

  # bom
  def compute
    server = find_server
    return unless server
    client = server.client
    return unless client
    request = client.make_request
    return unless request
    process_request(request)  
  end
  ```

  Durante os laços, prefira utilizar `next` ao invés de blocos condicionais.

  ```ruby
  # ruim
  [0, 1, 2, 3].each do |item|
    if item > 1
      puts item
    end
  end

  # bom
  [0, 1, 2, 3].each do |item|
    next unless item > 1
    puts item
  end
  ```

  Veja também a seção "Guard Clause", p68-70 in Beck, Kent.
  *Implementation Patterns*. Upper Saddle River: Addison-Wesley, 2008, que inspirou o conteúdo acima.

## Sintaxe

* <a name="nao-use-for"></a>Nunca use `for`, a não ser que você saiba o por que. Utilize outros interatores. `for` é implementado da mesma forma que o `each`, porém com uma divergência, `for` não introduz um novo escopo e variáveis definidas dentro do seu bloco serão vistas fora dele.<sup>[[link](#nao-use-for)]</sup>

    ```ruby
    arr = [1, 2, 3]

    # ruim
    for elem in arr do
      puts elem
    end

    # bom
    arr.each { |elem| puts elem }
    ```

* <a name="blocos-de-linhas-unicas"></a>Prefira `{...}` ao invés de `do...end` para blocos únicos. Evite usar `{...}` para blocos de múltiplas linhas (Chaves com multiplas linhas sempre são mal vistos). Sempre use `do...end` para "controle do fluxo" e "definição de métodos" (Exemplo: em Rakefiles e alguns DSLs).  Evite `do...end` com encadeamento.<sup>[[link](#blocos-de-linhas-unicas)]</sup>

    ```ruby
    names = ["Bozhidar", "Steve", "Sarah"]

    # bom
    names.each { |name| puts name }

    # ruim
    names.each do |name| puts name end

    # bom
    names.each do |name|
      puts name
      puts 'yay!'
    end

    # ruim
    names.each { |name|
      puts name
      puts 'yay!'
    }

    # bom
    names.select { |name| name.start_with?("S") }.map { |name| name.upcase }

    # ruim
    names.select do |name|
      name.start_with?("S")
    end.map { |name| name.upcase }
    ```

    Algumas pessoas irão argumentar que chaves com multiplas linhas são bem vistas com o uso do `{...}`, mas elas devem perguntar a si mesmo se esse código é de fácil leitura e também se o conteúdo pode ser extraído em algum método.

* <a name="forma-abreviada"></a>Sempre que possível, use a forma abreviada dos operadores.<sup>[[link](#forma-abreviada)]</sup>

    ```ruby
    # ruim
    x = x + y
    x = x * y
    x = x**y
    x = x / y
    x = x || y
    x = x && y

    # bom
    x += y
    x *= y
    x **= y
    x /= y
    x ||= y
    x &&= y
    ```

* <a name="ponto-e-virgula"></a>Evite usar ponto e vírgula, com exceção de declarações de classes em uma linha. Quando for apropriado utilizar ponto e vírgula, utilize apenas quando o bloco lógico estiver terminado: Não deve ter espaço antes do ponto e vírgula.<sup>[[link](#ponto-e-virgula)]</sup>

    ```ruby
    # ruim
    puts 'foobar'; # Desnecessário uso do ponto e vírgula
    puts 'foo'; puts 'bar' # Duas expressões na mesma linha.

    # bom
    puts 'foobar'

    puts 'foo'
    puts 'bar'

    puts 'foo', 'bar' # Isso se aplica a puts em particular
    ```

* <a name="dois-pontos"></a>Use :: apenas para referenciar constantes (Isso inclui classes e módulos) e construtores (Array() ou Nakogiri::HTML()).
    Não use :: para inicialização de métodos. <sup>[[link](#dois-pontos)]</sup>

    ```ruby
    # ruim
    SomeClass::some_method
    some_object::some_method

    # bom
    SomeClass.some_method
    some_object.some_method
    SomeModule::SomeClass::SOME_CONST
    SomeModule::SomeClass()
    ```

* <a name="return-redundante"></a>Evite usar `return` quando não for necessário.
    <sup>[[link](#return-redundante)]</sup>

    ```ruby
    # ruim
    def some_method(some_arr)
      return some_arr.size
    end

    # bom
    def some_method(some_arr)
      some_arr.size
    end
    ```

* <a name="atribuicao-em-condicao"></a>Não faça condições com o uso de `=`.<sup>[[link](#atribuicao-em-condicao)]</sup>

    ```ruby
    # ruim - deixa explicito o uso da condição
    if (v = array.grep(/foo/))
      ...
    end

    # ruim
    if v = array.grep(/foo/)
      ...
    end

    # bom
    v = array.grep(/foo/)
    if v
      ...
    end

    ```

* <a name="barras-duplas-para-inicializar"></a>Está liberado o uso de `||=` na inicialização das variáveis.
    <sup>[[link](#barras-duplas-para-inicializar)]</sup>

    ```ruby
    # Define o nome para Bozhidar, somente se ele for nil ou false
    name ||= 'Bozhidar'
    ```

* <a name="sem-barra-dupla-para-bool"></a>Não use `||=` para inicializar variáveis do tipo boolean, ao invés disso, considere o que deve ser feito caso a variável esteja definida como `false`)<sup>[[link](#sem-barra-dupla-para-bool)]</sup>

    ```ruby
    # ruim - vai definir como true, caso seja false
    enabled ||= true

    # bom
    enabled = true if enabled.nil?
    ```

* <a name="chamada-lambda"></a>Use `.call` explicitamente quando for usar lambdas.
    <sup>[[link](#chamada-lambda)]</sup>

    ```ruby
    # ruim
    lambda.(x, y)

    # bom
    lambda.call(x, y)
    ```

* <a name="sem-perl-estilo"></a>Evite usar o estilo Perl para variáveis especiais (como, `$0-9`, `$`, etc. ). Seu uso é meio enigmático e desincorajado. Prefira formas mais completas, como: `$PROGRAM_NAME`.<sup>[[link](#sem-perl-estilo)]</sup>

* <a name="blocos-de-acao-simples"></a>Quando um metodo contém apenas um argumento, e seu conteúdo é apenas uma leitura ou chamada de outro método sem argumentos, use a abreviação `&:`.
    <sup>[[link](#blocos-de-acao-simples)]</sup>

    ```ruby
    # ruim
    bluths.map { |bluth| bluth.occupation }
    bluths.select { |bluth| bluth.blue_self? }

    # bom
    bluths.map(&:occupation)
    bluths.select(&:blue_self?)
    ```

* <a name="self-redundante"></a>Prefira utilizar `some_method` do que `self.some_method` quando usar outro método da mesma instancia.<sup>[[link](#self-redundante)]</sup>

    ```ruby
    # ruim
    def end_date
      self.start_date + self.nights
    end

    # bom
    def end_date
      start_date + nights
    end
    ```

    Nos casos de uso a seguir, `self.` é obrigatório na linguagem e uma boa prática:

    1. Quando está definindo um método de uma classe: `def self.some_method`.
    2. O *lado esquerdo da igualdade*, quando chamar o método de atribuição, incluindo atribuição de um atributo e `self` sendo uma model do ActiveRecord: `self.guest = user`.
    3. Referenciando a instance da classe atual: `self.class`.

* <a name="constante-freeze"></a>Quando for definir algum objeto de um tipo que pode ser alterado, mas com a intenção de ser uma constante, não esqueça de utilizar o método `freeze`. Exemplos comuns são: strings, arrays, e hashes.
    ([Leia mais sobre isso][ruby-freeze].)<sup>[[link](#constante-freeze)]</sup>

    Isso acontece por que no Ruby, constantes não tem um tipo único. Utilizando `freeze` nós garantimos que o tipo não será mudado e portanto será uma constante de fato, qualquer tentativa de mudança irá gerar uma exceção. 

    ```ruby
    # ruim
    class Color
      RED = 'red'
      BLUE = 'blue'
      GREEN = 'green'
      
      ALL_COLORS = [
        RED,
        BLUE,
        GREEN,
      ]
    
      COLOR_TO_RGB = {
        RED => 0xFF0000,
        BLUE => 0x0000FF,
        GREEN => 0x00FF00,
      }
    end

    # bom    
    class Color
      RED = 'red'.freeze
      BLUE = 'blue'.freeze
      GREEN = 'green'.freeze

      ALL_COLORS = [
        RED,
        BLUE,
        GREEN,
      ].freeze
    
      COLOR_TO_RGB = {
        RED => 0xFF0000,
        BLUE => 0x0000FF,
        GREEN => 0x00FF00,
      }.freeze
    end
    ```

## Nomenclatura

* <a name="snake-case"></a>Para métodos e variáveis, utilize o padrão `snake_case`.
    <sup>[[link](#snake-case)]</sup>

* <a name="camel-case"></a>Para classes ou módulos, utilize o padrão `CamelCase`. (Mantenha singlas, como: HTTP, RFC, XML `UPPERCASE`.)
    <sup>[[link](#camel-case)]</sup>

* <a name="screaming-snake-case"></a>Para outras constantes, utilize o padrão: `SCREAMING_SNAKE_CASE`.<sup>[[link](#screaming-snake-case)]</sup>

* <a name="nome-predicado-de-metodos"></a>Nome dos predicados dos métodos (Método que retorna um valor boolean) devem terminar com ponto de interrogação (exemplo: `Array#empty?`).<sup>[[link](#nome-predicado-de-metodos)]</sup>

* <a name="metodo-bang"></a>Nome de métodos que são potenciallmente "perigosos" (exemplo: métodos que modificam `self` ou argumentos, `exit!`, etc.) devem terminar com um ponto de exclamação. Um `bang method` só deve existir caso haja um `non-bang` correspondente. ([Leia mais sobre isso][ruby-naming-bang].)
    <sup>[[link](#metodo-bang)]</sup>

* <a name="variaveis-temporararia"></a>Nomeie variáveis temporarias com `_`.
    <sup>[[link](#variaveis-temporararia)]</sup>

    ```ruby
    version = '3.2.1'
    major_version, minor_version, _ = version.split('.')
    ```

## Classes

* <a name="evite-variaveis-de-classe"></a>Evite usar (`@@`) em classes devido ao seu comportamento desagradável em heranças.
    <sup>[[link](#evite-variaveis-de-classe)]</sup>

    ```ruby
    class Parent
      @@class_var = 'parent'

      def self.print_class_var
        puts @@class_var
      end
    end

    class Child < Parent
      @@class_var = 'child'
    end

    Parent.print_class_var # => Irá imprimir "child"
    ```

  Como você pode ver, todas as classes em um sistema de hierarquia irão compartilhar uma variável em comum. As variáveis da classe instanciada são preferíveis a variáveis da classe atual.

* <a name="metodo-singleton"></a>Use `def self.method` para definir métodos com o padrão singleton. Isso faz com que o método seja mais resistente a mudanças.
    <sup>[[link](#metodo-singleton)]</sup>

    ```ruby
    class TestClass
      # ruim
      def TestClass.some_method
        ...
      end

      # bom
      def self.some_other_method
        ...
      end
    ```
* <a name="no-class-self"></a>Evite `class << self`, exceto quando necessário.
    exemplo: Atributos auxiliares.
    <sup>[[link](#no-class-self)]</sup>

    ```ruby
    class TestClass
      # ruim
      class << self
        def first_method
          ...
        end

        def second_method_etc
          ...
        end
      end

      # bom
      class << self
        attr_accessor :per_page
        alias_method :nwo, :find_by_name_with_owner
      end

      def self.first_method
        ...
      end

      def self.second_method_etc
        ...
      end
    end
    ```

* <a name="acessando-modificadores"></a>Indente métodos `public`, `protected`, e
    `private` tanto quanto a definição do método é aplicada. Deixe uma linha vazia antes e depois.<sup>[[link](#acessando-modificadores)]</sup>

    ```ruby
    class SomeClass
      def public_method
        # ...
      end

      private

      def private_method
        # ...
      end
    end
    ```

## Exceções

* <a name="fluxo-controle-excecao"></a>Não use exceções para controle de fluxo.
    <sup>[[link](#fluxo-controle-excecao)]</sup>

    ```ruby
    # ruim
    begin
      n / d
    rescue ZeroDivisionError
      puts "Cannot divide by 0!"
    end

    # bom
    if d.zero?
      puts "Cannot divide by 0!"
    else
      n / d
    end
    ```

* <a name="sem-excecao-generica"></a>Evite capturar a classe `Exception`.
    <sup>[[link](#sem-excecao-generica)]</sup>

    ```ruby
    # ruim
    begin
      # uma exceção acontece aqui
    rescue Exception
      # lidando com a exceção
    end

    # bom
    begin
      # uma exceção acontece aqui
    rescue StandardError
      # lidando com a exceção
    end

    # aceitável
    begin
      # uma exceção acontece aqui
    rescue
      # lidando com a exceção
    end
    ```

* <a name="excecoes-redundantes"></a>Não declare a exceção `RuntimeError` com dois argumentos. Prefira erros de sub-classes e erros explicítos de criação.<sup>[[link](#excecoes-redundantes)]</sup>

    ```ruby
    # ruim
    raise RuntimeError, 'message'

    # melhor - RuntimeError está implicito aqui
    raise 'message'

    # ótimo
    class MyExplicitError < RuntimeError; end
    raise MyExplicitError
    ```


* <a name="messagem-de-classe-de-excecao"></a>
    Ao invés de uma instancia para tratar a exceção,'prefira fornecer uma classe e uma mensagem para exceção em dois argumentos separados com `raise`. <sup>[[link](#messagem-de-classe-de-excecao)]</sup>

    ```Ruby
    # ruim
    raise SomeException.new('message')
    # Note que não há uma forma de fazer: `raise SomeException.new('message'), backtrace`.

    # bom
    raise SomeException, 'message'
    # Consistente com `raise SomeException, 'message', backtrace`.
    ```


* <a name="rescue-modificado"></a>Evite usar `rescue` na sua forma modificada.
    <sup>[[link](#rescue-modificado)]</sup>

    ```ruby
    # ruim
    read_file rescue handle_error($!)

    # bom
    begin
      read_file
    rescue Errno:ENOENT => ex
      handle_error(ex)
    end
    ```

## Coleções

* <a name="map-ao-inves-collect"></a>Prefira o método `map` ao
    `collect`.<sup>[[link](#map-ao-inves-collect)]</sup>

* <a name="detect-ao-inves-find"></a>Prefira o método `detect` ao invés de `find`. `find` tem um uso ambiguo por causa do método do ActiveRecord's `find` - Utilizar `detect` deixa claro que você está trabalhando com uma coleção em Ruby, não um objeto ActiveRecord.
    <sup>[[link](#detect-ao-inves-find)]</sup>

* <a name="reduce-ao-inves-inject"></a>Prefira o método `reduce` ao invés de `inject`.
    <sup>[[link](#reduce-ao-inves-inject)]</sup>

* <a name="size-ao-inves-count"></a>Prefira o método `size` ao invés de `length` ou `count` por motivos performáticos.<sup>[[link](#size-ao-inves-count)]</sup>

* <a name="colecoes-vazias"></a>Prefira criar array e hash de forma literal, a não ser que você passe parâmetros para seus construtores.
    <sup>[[link](#colecoes-vazias)]</sup>

    ```ruby
    # ruim
    arr = Array.new
    hash = Hash.new

    # bom
    arr = []
    hash = {}

    # bom por que o construtor necessita de parâmetros
    x = Hash.new { |h, k| h[k] = {} }
    ```

* <a name="array-join"></a>Prefira `Array#join` do que `Array#*` por clareza.
    <sup>[[link](#array-join)]</sup>

    ```ruby
    # ruim
    %w(one two three) * ', '
    # => 'one, two, three'

    # bom
    %w(one two three).join(', ')
    # => 'one, two, three'
    ```

* <a name="simbolo-chaves-hash"></a>Nas hash key, use simbolos ao invés de strings.
    <sup>[[link](#simbolo-chaves-hash)]</sup>

    ```ruby
    # ruim
    hash = { 'one' => 1, 'two' => 2, 'three' => 3 }

    # bom
    hash = { :one => 1, :two => 2, :three => 3 }
    ```

* <a name="simbolos-literais"></a>Use simbolos ao invés de strings sempre que possível.<sup>[[link](#simbolos-literais)]</sup>

    ```ruby
    # ruim
    :"symbol"

    # bom
    :symbol
    ```

* <a name="metodo-hash-desatualizado"></a>Use `Hash#key?` ao invés de
    `Hash#has_key?` e `Hash#value?` ao invés de `Hash#has_value?`. De acordo com Matz, as formas longas são consideradas desatualizadas.
    <sup>[[link](#metodo-hash-desatualizado)]</sup>

    ```ruby
    # ruim
    hash.has_key?(:test)
    hash.has_value?(value)

    # bom
    hash.key?(:test)
    hash.value?(value)
    ```

* <a name="hash-multiplas-linhas"></a>Declare hashes em multiplas linhas quando for deixar o código mais fácil para leitura e utilize virgula para garantir que o parâmetro mudou.
    <sup>[[link](#hash-multiplas-linhas)]</sup>

    ```ruby
    hash = {
      :protocol => 'https',
      :only_path => false,
      :controller => :users,
      :action => :set_password,
      :redirect => @redirect_url,
      :secret => @secret,
    }
    ```

* <a name="array-virgula-multiplas-linhas"></a>Use vírgula em `Array` que abrange mais de uma linha <sup>[[link](#array-virgula-multiplas-linhas)]</sup>

    ```ruby
    # bom
    array = [1, 2, 3]

    # bom
    array = [
      "car",
      "bear",
      "plane",
      "zoo",
    ]
    ```

## Textos

* <a name="interpolacao-string"></a>Prefira interpolar strings ao invés de concatena-las: <sup>[[link](#interpolacao-string)]</sup>

    ```ruby
    # ruim
    email_with_name = user.name + ' <' + user.email + '>'

    # bom
    email_with_name = "#{user.name} <#{user.email}>"
    ```

  Além disso, mantenha em mente que Ruby 1.9 liberou a interpolação. Digamos que você está usando cache keys como este:

    ```ruby
    CACHE_KEY = '_store'

    cache.write(@user.id + CACHE_KEY)
    ```

    Prefira interpolar strings ao invés de concatena-las

    ```ruby
    CACHE_KEY = '%d_store'

    cache.write(CACHE_KEY % @user.id)
    ```

* <a name="concatenacao-string"></a>Evite usar `String#+` quando você precisa criar grandes pedaços de dado. Ao invés disso, use `String#<<`. Concatenação altera o conteúdo da string e é sempre mais rápido que `String#+`, que cria um novo objeto de strings.<sup>[[link](#concatenacao-string)]</sup>

    ```ruby
    # bom e rápido
    html = ''
    html << '<h1>Page title</h1>'

    paragraphs.each do |paragraph|
      html << "<p>#{paragraph}</p>"
    end
    ```

* <a name="strings-de-multiplas-linhas"></a>Para concatenar multiplas linhas de string use `\` no fim das linhas ao invés de `+` ou `<<`
    <sup>[[link](#strings-de-multiplas-linhas)]</sup>

    ```ruby
    # ruim
    "Some string is really long and " +
      "spans multiple lines."

    "Some string is really long and " <<
      "spans multiple lines."

    # bom
    "Some string is really long and " \
      "spans multiple lines."
    ```

## Expressões regulares

* <a name="nomeando-regex"></a>Evite usar `$1-9` por que pode ser difícil de localizar o seu conteṕudo. Prefira usar variáveis.
    <sup>[[link](#nomeando-regex)]</sup>

    ```ruby
    # ruim
    /(regexp)/ =~ string
    ...
    process $1

    # bom
    /(?<meaningful_var>regexp)/ =~ string
    ...
    process meaningful_var
    ```

* <a name="tio-acento-dolar-regex"></a>Tenha cuidado com `^` e `$` quando eles se encaixam no começo o no fim das linhas e não fim das strings. Se você quer localizar todo o texto, use: `\A` e `\z`.<sup>[[link](#tio-acento-dolar-regex)]</sup>

    ```ruby
    string = "some injection\nusername"
    string[/^username$/]   # encontrou
    string[/\Ausername\z/] # não encontrou
    ```

* <a name="comentarios-regex"></a>Para regex complexos, use `x`. Isso faz com que seja mais fácil de ler e você pode adicionar alguns comentários. Só tenha cuidado com os espaços que podem ser ignorados. <sup>[[link](#comentarios-regex)]</sup>

    ```ruby
    regexp = %r{
      start         # algum texto
      \s            # caracter de espaço em branco
      (group)       # primeiro grupo
      (?:alt1|alt2) # alguma alternativa
      end
    }x
    ```

## Notação de porcentagem

* <a name="porcentagem-notacao-delimitador"></a>Prefira parenteses ao invés de chaves, colchetes ou traço quando utilizar `%` para consistencia e pelo comportamento do `%` ser mais próximos da chamada de métodos.<sup>[[link](#porcentagem-notacao-delimitador)]</sup>

    ```ruby
    # ruim
    %w[date locale]
    %w{date locale}
    %w|date locale|

    # bom
    %w(date locale)
    ```

* <a name="w-porcentagem"></a>Use `%w` livremente.<sup>[[link](#w-porcentagem)]</sup>

    ```ruby
    STATES = %w(draft open closed)
    ```

* <a name="parenteses-porcentagem"></a>Use `%()` para textos de linhas únicas que necessite tanto interpolação quando aspas duplas. Para multiplas linhas, prefira heredoc.<sup>[[link](#parenteses-porcentagem)]</sup>

    ```ruby
    # ruim - sem necessidade de interpolação
    %(<div class="text">Some text</div>)
    # devería ser '<div class="text">Some text</div>'

    # ruim - sem aspas duplas
    %(This is #{quality} style)
    # Devería ser "This is #{quality} style"

    # ruim - multiplas linhas
    %(<div>\n<span class="big">#{exclamation}</span>\n</div>)
    # devería ser em heredoc.

    # bom - necessita de interpolação, tem aspas duplas e está em linha única.
    %(<tr><td class="name">#{name}</td>)
    ```

* <a name="r-porcentagem"></a>Use `%r` somente para expressões regulares localizando mais de um caracter '/'.<sup>[[link](#r-porcentagem)]</sup>

    ```ruby
    # ruim
    %r(\s+)

    # ainda ruim
    %r(^/(.*)$)
    # devería ser /^\/(.*)$/

    # bom
    %r(^/blog/2011/(.*)$)
    ```

* <a name="x-porcentagem"></a>Evite o uso de `%x`, a não ser que você esteja invocando um comando com aspas invertidas (O que é indesejável).
    <sup>[[link](#x-porcentagem)]</sup>

    ```ruby
    # ruim
    date = %x(date)

    # bom
    date = `date`
    echo = %x(echo `date`)
    ```

## Rails

* <a name="return-proxima-linha"></a>Quando retornar imediatamente depois de
    `render` ou `redirect_to`, coloque `return` na próxima linha, não na mesma.
    <sup>[[link](#return-proxima-linha)]</sup>

    ```ruby
    # ruim
    render :text => 'Howdy' and return

    # bom
    render :text => 'Howdy'
    return

    # ainda ruim
    render :text => 'Howdy' and return if foo.present?

    # bom
    if foo.present?
      render :text => 'Howdy'
      return
    end
    ```

### Escopo
* <a name="escopo-lambda"></a>Quando definir model no ActiveRecord, encaixe a relação em `lambda`.  Sem isso, a relação força o banco de dados a estabelezer a conexão quando a classe é carregada, não no ínicio.
    <sup>[[link](#escopo-lambda)]</sup>

    ```ruby
    # ruim
    scope :foo, where(:bar => 1)

    # bom
    scope :foo, -> { where(:bar => 1) }
    ```

## Seja consistente.

>Se você está editando o código, invista um tempo olhando-o e determinando seu estio. Se ele usa espaço ao redor de todos os operadores aritméticos, você deve fazer também. Se os comentários contém pequenas caixas cercadas de barras, faça seus comentários da mesma forma.

> A motivação de ter um guia de estilo é ter um vocabulário comum para que as pessoas possam se concentrar no que está sendo tido e não como está sendo tido. Nós apresentamos um estilo global para que as pessoas saibam esse vocabulário, mas vocabulários regionais também são importantes. Se você fizer um código completamente diferente dos códigos ao seu redor, irá causar intriga entre os leitores que forem ler ele. Evite isso.

&mdash;[Google C++ Style Guide][google-c++]

[airbnb-javascript]: https://github.com/airbnb/javascript
[bbatsov-ruby]: https://github.com/bbatsov/ruby-style-guide
[github-ruby]: https://github.com/styleguide/ruby
[google-c++]: https://google.github.io/styleguide/cppguide.html
[google-c++-comments]: https://google.github.io/styleguide/cppguide.html#Comments
[google-python-comments]: https://google.github.io/styleguide/pyguide.html#Comments
[ruby-naming-bang]: http://dablog.rubypal.com/2007/8/15/bang-methods-or-danger-will-rubyist
[ruby-freeze]: http://blog.honeybadger.io/when-to-use-freeze-and-frozen-in-ruby/
[avoid-else-return-early]: http://blog.timoxley.com/post/47041269194/avoid-else-return-early

## Tradução

  Este guia também está disponível em outros idiomas:

  - ![cn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/China.png) **Chinês (Simplificado)**: [1c7/ruby-airbnb](https://github.com/1c7/ruby-airbnb)
  - ![usa](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/United-States.png) **Inglês**: [airbnb/ruby](https://github.com/airbnb/ruby)
