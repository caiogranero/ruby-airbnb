# Ruby Style Guide

O guia de estilo para Ruby do Airbnb.

Inspirado por [GitHub's guide](https://web.archive.org/web/20160410033955/https://github.com/styleguide/ruby) e [Bozhidar Batsov's guide][bbatsov-ruby].

Airbnb também mantém o [Guia de estilo para JavaScript][airbnb-javascript].

## Indíce
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
    1. [Comentários de pendencias](#comentários-de-pendencias)
    1. [Códigos comentado](#códigos-comentado)
  1. [Métodos](#métodos)
    1. [Definição de métodos](#definição-de-métodos)
    1. [Chamada de métodos](#chamada-de-métodos)
  1. [Expressões condicionais](#expressões-condicionais)
    1. [Palavras condicionais](#palavras-condicionais)
    1. [Operador ternário](#operador-ternário)
    1. [Condições longas](#condições-longas) ////
  1. [Syntax](#syntax)
  1. [Naming](#naming)
  1. [Classes](#classes)
  1. [Exceções](#excecoes)
  1. [Coleções](#colecoes)
  1. [Strings](#strings)
  1. [Expressões regulares](#regular-expressions)
  1. [Percent Literals](#percent-literals)
  1. [Rails](#rails)
    1. [Scopes](#scopes)
  1. [Seja consistente](#be-consistent)
  1. [Tradução](#translation)

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

* <a name="alinhar-parametros-de-funcao"></a>Alinhe todos os parametros de função ou na mesma linha ou um por linha.<sup>[[link](#alinhar-parametros-de-funcao)]</sup>

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

* <a name="indente-multi-line-bool"></a>Indente continuamente multiplas linhas de expressões condicionais.<sup>[[link](#indente-multi-linhas-bool)]</sup>

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

* <a name="espaco-antes-comentario"></a>Quando fizer comentários de linha única, inclua um espaço entre o fim do código e o começo do comentário.
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

* <a name="bloco-espaco-parametro"></a>Não inclua espaço dentro de blocos de parâmetros. Inclua um espaço entre parametros dentro de um bloco. Inclua um espaço fora do bloco de parametro.
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

* <a name="if-multiplas-novas-linhas"></a>Adiciona uma nova linha depois da condição `if` usada com multiplicas linhas, para ajudar diferenciar entre condições e o conteúdo.
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

* <a name="nova-linha-diferente-conteudos"></a>Não quebre linhas entre diferentes conteúdos (Como classes ou modulos).
    <sup>[[link](#nova-linha-diferente-conteudos)]</sup>

    ```ruby
    # ruim
    class Foo

      def bar
        # conteudo omitido
      end

    end

    # bom
    class Foo
      def bar
        # conteudo omitido
      end
    end
    ```

* <a name="nova-linha-entre-metodos"></a>Inclua APENAS uma nova linha entre metodos.
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

* <a name="finaliza-nova-linha"></a>Finalize cada linha com uma nova linha. Não inclua multiplas linhas no fim do seu arquivo.
    <sup>[[link](#finaliza-nova-linha)]</sup>

## Tamanho das linhas

* Mantenha cada linha do código com um tamanho viável para leitura. A não ser, você tenha uma razão para não fazer, mantenha linhas com menos de 100 caractéres.
  ([rationale](./rationales.md#line-length))<sup>
  [[link](#line-length)]</sup>

## Comentários

> Apesar de ser chato de escrever, comentários são extremamente importantes para manter o código viável para leitura. As regras a seguir descrevem o que você devería comentar e aonde. Mas lembre-se: Enquanto comentários são muito importantes, um bom código é auto-documentável. Nome com sentido para variáveis e métodos são melhores do que usar nomes sem significado que você precise explicar através de comentários.

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
  # dup() produzi um array que podemos alterar
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

<a name="sem-blocos-de-comentarios"></a>Relacionado: Não use blocos de comentários. Eles não podem ser precedidos por espaços e não são faceis de encaixar se comparado a comentários padrões.
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

Comentários de pendências devem incluir a palavra TODO, seguido pelo nome completo da pessoa que conhece mais do problema. Dois pontos é opcional. Um comentário explicando qual o requisito dessa tarefa é o obrigatório. O principal motivo de ter um comentário de pendência consistente é ser fácil de encontrar a pessoa que está sendo mencionada. Esse comentário não é um compromisso para a pessoa mencionada resolver o problema. Tanto que, quando você cria um comentário de pendência, costuma ser o seu nome que será mencionado.

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

* <a name="parenteses-def-metodos"></a>Use `def` com parênteses quando contém parâmetros. Nã use parênteses quando o metodo não aceita parâmetros.
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

* <a name="metodo-de-linha-unica"></a>Evite escrever metodos em uma linha só. Apesar de serem populares, existe algumas pecularidades que fazem dessa abordagem indesejável.
    <sup>[[link](#nometodo-de-linha-unica)]</sup>

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

* <a name="sem-parenteses-no-retorno"></a>Se o método não retorna um valor (ou não nos importamos com o retorno), o parenteses é opcional. (Com exceção se o argumento ocupa multiplas linhas, parênteses podem ajudar a leitura.)
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

* <a name="evite-operadores-ternarios-complexos"></a>Evite utilizar operadores ternários (`?:`) a não ser que a condĩção seja extremamente trivial. Por outro lado, use o operador ternário (`?:`) ao invés de `if/then/else/end` para condições de linhas únicas.<sup>[[link](#evite-operadores-ternarios-complexos)]</sup>

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

* <a name="operador-ternario-condicoes-simples"></a>Evite multiplas condições em operadores ternários.
    Operadores ternários são melhor usados em condições simples.
    <sup>[[link](#operador-ternario-condicoes-simples)]</sup>

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

    Some will argue that multiline chaining would look okay with the use of
    `{...}`, but they should ask themselves if this code is really readable and
    whether the block's content can be extracted into nifty methods.

* <a name="self-assignment"></a>Use shorthand self assignment operators
    whenever applicable.<sup>[[link](#self-assignment)]</sup>

    ```ruby
    # bad
    x = x + y
    x = x * y
    x = x**y
    x = x / y
    x = x || y
    x = x && y

    # good
    x += y
    x *= y
    x **= y
    x /= y
    x ||= y
    x &&= y
    ```

* <a name="semicolons"></a>Avoid semicolons except for in single line class
    definitions. When it is appropriate to use a semicolon, it should be
    directly adjacent to the statement it terminates: there should be no
    space before the semicolon.<sup>[[link](#semicolons)]</sup>

    ```ruby
    # bad
    puts 'foobar'; # superfluous semicolon
    puts 'foo'; puts 'bar' # two expressions on the same line

    # good
    puts 'foobar'

    puts 'foo'
    puts 'bar'

    puts 'foo', 'bar' # this applies to puts in particular
    ```

* <a name="colon-use"></a>Use :: only to reference constants(this includes
    classes and modules) and constructors (like Array() or Nokogiri::HTML()).
    Do not use :: for regular method invocation.<sup>[[link](#colon-use)]</sup>

    ```ruby
    # bad
    SomeClass::some_method
    some_object::some_method

    # good
    SomeClass.some_method
    some_object.some_method
    SomeModule::SomeClass::SOME_CONST
    SomeModule::SomeClass()
    ```

* <a name="redundant-return"></a>Avoid `return` where not required.
    <sup>[[link](#redundant-return)]</sup>

    ```ruby
    # bad
    def some_method(some_arr)
      return some_arr.size
    end

    # good
    def some_method(some_arr)
      some_arr.size
    end
    ```

* <a name="assignment-in-conditionals"></a>Don't use the return value of `=` in
    conditionals<sup>[[link](#assignment-in-conditionals)]</sup>

    ```ruby
    # bad - shows intended use of assignment
    if (v = array.grep(/foo/))
      ...
    end

    # bad
    if v = array.grep(/foo/)
      ...
    end

    # good
    v = array.grep(/foo/)
    if v
      ...
    end

    ```

* <a name="double-pipe-for-uninit"></a>Use `||=` freely to initialize variables.
    <sup>[[link](#double-pipe-for-uninit)]</sup>

    ```ruby
    # set name to Bozhidar, only if it's nil or false
    name ||= 'Bozhidar'
    ```

* <a name="no-double-pipes-for-bools"></a>Don't use `||=` to initialize boolean
    variables. (Consider what would happen if the current value happened to be
    `false`.)<sup>[[link](#no-double-pipes-for-bools)]</sup>

    ```ruby
    # bad - would set enabled to true even if it was false
    enabled ||= true

    # good
    enabled = true if enabled.nil?
    ```

* <a name="lambda-calls"></a>Use `.call` explicitly when calling lambdas.
    <sup>[[link](#lambda-calls)]</sup>

    ```ruby
    # bad
    lambda.(x, y)

    # good
    lambda.call(x, y)
    ```

* <a name="no-cryptic-perl"></a>Avoid using Perl-style special variables (like
    `$0-9`, `$`, etc. ). They are quite cryptic and their use in anything but
    one-liner scripts is discouraged. Prefer long form versions such as
    `$PROGRAM_NAME`.<sup>[[link](#no-cryptic-perl)]</sup>

* <a name="single-action-blocks"></a>When a method block takes only one
    argument, and the body consists solely of reading an attribute or calling
    one method with no arguments, use the `&:` shorthand.
    <sup>[[link](#single-action-blocks)]</sup>

    ```ruby
    # bad
    bluths.map { |bluth| bluth.occupation }
    bluths.select { |bluth| bluth.blue_self? }

    # good
    bluths.map(&:occupation)
    bluths.select(&:blue_self?)
    ```

* <a name="redundant-self"></a>Prefer `some_method` over `self.some_method` when
    calling a method on the current instance.<sup>[[link](#redundant-self)]</sup>

    ```ruby
    # bad
    def end_date
      self.start_date + self.nights
    end

    # good
    def end_date
      start_date + nights
    end
    ```

    In the following three common cases, `self.` is required by the language
    and is good to use:

    1. When defining a class method: `def self.some_method`.
    2. The *left hand side* when calling an assignment method, including assigning
       an attribute when `self` is an ActiveRecord model: `self.guest = user`.
    3. Referencing the current instance's class: `self.class`.

* <a name="freeze-constants"></a>When defining an object of any mutable
    type meant to be a constant, make sure to call `freeze` on it. Common 
    examples are strings, arrays, and hashes.
    ([More on this][ruby-freeze].)<sup>[[link](#freeze-constants)]</sup>

    The reason is that Ruby constants are actually mutable. Calling `freeze`
    ensures they are not mutated and are therefore truly constant and 
    attempting to modify them will raise an exception. For strings, this allows
    older versions of Ruby below 2.2 to intern them.

    ```ruby
    # bad
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

    # good    
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

## Naming

* <a name="snake-case"></a>Use `snake_case` for methods and variables.
    <sup>[[link](#snake-case)]</sup>

* <a name="camel-case"></a>Use `CamelCase` for classes and modules. (Keep
    acronyms like HTTP, RFC, XML uppercase.)
    <sup>[[link](#camel-case)]</sup>

* <a name="screaming-snake-case"></a>Use `SCREAMING_SNAKE_CASE` for other
    constants.<sup>[[link](#screaming-snake-case)]</sup>

* <a name="predicate-method-names"></a>The names of predicate methods (methods
    that return a boolean value) should end in a question mark.
    (i.e. `Array#empty?`).<sup>[[link](#predicate-method-names)]</sup>

* <a name="bang-methods"></a>The names of potentially "dangerous" methods
    (i.e. methods that modify `self` or the arguments, `exit!`, etc.) should
    end with an exclamation mark. Bang methods should only exist if a non-bang
    method exists. ([More on this][ruby-naming-bang].)
    <sup>[[link](#bang-methods)]</sup>

* <a name="throwaway-variables"></a>Name throwaway variables `_`.
    <sup>[[link](#throwaway-variables)]</sup>

    ```ruby
    version = '3.2.1'
    major_version, minor_version, _ = version.split('.')
    ```

## Classes

* <a name="avoid-class-variables"></a>Avoid the usage of class (`@@`) variables
    due to their "nasty" behavior in inheritance.
    <sup>[[link](#avoid-class-variables)]</sup>

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

    Parent.print_class_var # => will print "child"
    ```

  As you can see all the classes in a class hierarchy actually share one
  class variable. Class instance variables should usually be preferred
  over class variables.

* <a name="singleton-methods"></a>Use `def self.method` to define singleton
    methods. This makes the methods more resistant to refactoring changes.
    <sup>[[link](#singleton-methods)]</sup>

    ```ruby
    class TestClass
      # bad
      def TestClass.some_method
        ...
      end

      # good
      def self.some_other_method
        ...
      end
    ```
* <a name="no-class-self"></a>Avoid `class << self` except when necessary,
    e.g. single accessors and aliased attributes.
    <sup>[[link](#no-class-self)]</sup>

    ```ruby
    class TestClass
      # bad
      class << self
        def first_method
          ...
        end

        def second_method_etc
          ...
        end
      end

      # good
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

* <a name="access-modifiers"></a>Indent the `public`, `protected`, and
    `private` methods as much the method definitions they apply to. Leave one
    blank line above and below them.<sup>[[link](#access-modifiers)]</sup>

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

## Exceptions

* <a name="exception-flow-control"></a>Don't use exceptions for flow of control.
    <sup>[[link](#exception-flow-control)]</sup>

    ```ruby
    # bad
    begin
      n / d
    rescue ZeroDivisionError
      puts "Cannot divide by 0!"
    end

    # good
    if d.zero?
      puts "Cannot divide by 0!"
    else
      n / d
    end
    ```

* <a name="dont-rescue-exception"></a>Avoid rescuing the `Exception` class.
    <sup>[[link](#dont-rescue-exception)]</sup>

    ```ruby
    # bad
    begin
      # an exception occurs here
    rescue Exception
      # exception handling
    end

    # good
    begin
      # an exception occurs here
    rescue StandardError
      # exception handling
    end

    # acceptable
    begin
      # an exception occurs here
    rescue
      # exception handling
    end
    ```

* <a name="redundant-exception"></a>Don't specify `RuntimeError` explicitly in
    the two argument version of raise. Prefer error sub-classes for clarity and
    explicit error creation.<sup>[[link](#redundant-exception)]</sup>

    ```ruby
    # bad
    raise RuntimeError, 'message'

    # better - RuntimeError is implicit here
    raise 'message'

    # best
    class MyExplicitError < RuntimeError; end
    raise MyExplicitError
    ```


* <a name="exception-class-messages"></a>
    Prefer supplying an exception class and a message as two separate arguments
    to `raise`, instead of an exception instance.
    <sup>[[link](#exception-class-messages)]</sup>

    ```Ruby
    # bad
    raise SomeException.new('message')
    # Note that there is no way to do `raise SomeException.new('message'), backtrace`.

    # good
    raise SomeException, 'message'
    # Consistent with `raise SomeException, 'message', backtrace`.
    ```


* <a name="rescue-as-modifier"></a>Avoid using rescue in its modifier form.
    <sup>[[link](#rescue-as-modifier)]</sup>

    ```ruby
    # bad
    read_file rescue handle_error($!)

    # good
    begin
      read_file
    rescue Errno:ENOENT => ex
      handle_error(ex)
    end
    ```

## Collections

* <a name="map-over-collect"></a>Prefer `map` over
    `collect`.<sup>[[link](#map-over-collect)]</sup>

* <a name="detect-over-find"></a>Prefer `detect` over `find`. The use of `find`
    is ambiguous with regard to ActiveRecord's `find` method - `detect` makes
    clear that you're working with a Ruby collection, not an AR object.
    <sup>[[link](#detect-over-find)]</sup>

* <a name="reduce-over-inject"></a>Prefer `reduce` over `inject`.
    <sup>[[link](#reduce-over-inject)]</sup>

* <a name="size-over-count"></a>Prefer `size` over either `length` or `count`
    for performance reasons.<sup>[[link](#size-over-count)]</sup>

* <a name="empty-collection-literals"></a>Prefer literal array and hash creation
    notation unless you need to pass parameters to their constructors.
    <sup>[[link](#empty-collection-literals)]</sup>

    ```ruby
    # bad
    arr = Array.new
    hash = Hash.new

    # good
    arr = []
    hash = {}

    # good because constructor requires parameters
    x = Hash.new { |h, k| h[k] = {} }
    ```

* <a name="array-join"></a>Favor `Array#join` over `Array#*` for clarity.
    <sup>[[link](#array-join)]</sup>

    ```ruby
    # bad
    %w(one two three) * ', '
    # => 'one, two, three'

    # good
    %w(one two three).join(', ')
    # => 'one, two, three'
    ```

* <a name="symbol-keys"></a>Use symbols instead of strings as hash keys.
    <sup>[[link](#symbol-keys)]</sup>

    ```ruby
    # bad
    hash = { 'one' => 1, 'two' => 2, 'three' => 3 }

    # good
    hash = { :one => 1, :two => 2, :three => 3 }
    ```

* <a name="symbol-literals"></a>Relatedly, use plain symbols instead of string
    symbols when possible.<sup>[[link](#symbol-literals)]</sup>

    ```ruby
    # bad
    :"symbol"

    # good
    :symbol
    ```

* <a name="deprecated-hash-methods"></a>Use `Hash#key?` instead of
    `Hash#has_key?` and `Hash#value?` instead of `Hash#has_value?`. According
    to Matz, the longer forms are considered deprecated.
    <sup>[[link](#deprecated-hash-methods)]</sup>

    ```ruby
    # bad
    hash.has_key?(:test)
    hash.has_value?(value)

    # good
    hash.key?(:test)
    hash.value?(value)
    ```

* <a name="multiline-hashes"></a>Use multi-line hashes when it makes the code
    more readable, and use trailing commas to ensure that parameter changes
    don't cause extraneous diff lines when the logic has not otherwise changed.
    <sup>[[link](#multiline-hashes)]</sup>

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

* <a name="array-trailing-comma"></a>Use a trailing comma in an `Array` that
    spans more than 1 line<sup>[[link](#array-trailing-comma)]</sup>

    ```ruby
    # good
    array = [1, 2, 3]

    # good
    array = [
      "car",
      "bear",
      "plane",
      "zoo",
    ]
    ```

## Strings

* <a name="string-interpolation"></a>Prefer string interpolation instead of
    string concatenation:<sup>[[link](#string-interpolation)]</sup>

    ```ruby
    # bad
    email_with_name = user.name + ' <' + user.email + '>'

    # good
    email_with_name = "#{user.name} <#{user.email}>"
    ```

  Furthermore, keep in mind Ruby 1.9-style interpolation. Let's say you are
  composing cache keys like this:

    ```ruby
    CACHE_KEY = '_store'

    cache.write(@user.id + CACHE_KEY)
    ```

    Prefer string interpolation instead of string concatenation:

    ```ruby
    CACHE_KEY = '%d_store'

    cache.write(CACHE_KEY % @user.id)
    ```

* <a name="string-concatenation"></a>Avoid using `String#+` when you need to
    construct large data chunks. Instead, use `String#<<`. Concatenation mutates
    the string instance in-place  and is always faster than `String#+`, which
    creates a bunch of new string objects.<sup>[[link](#string-concatenation)]</sup>

    ```ruby
    # good and also fast
    html = ''
    html << '<h1>Page title</h1>'

    paragraphs.each do |paragraph|
      html << "<p>#{paragraph}</p>"
    end
    ```

* <a name="multi-line-strings"></a>Use `\` at the end of the line instead of `+`
    or `<<` to concatenate multi-line strings.
    <sup>[[link](#multi-line-strings)]</sup>

    ```ruby
    # bad
    "Some string is really long and " +
      "spans multiple lines."

    "Some string is really long and " <<
      "spans multiple lines."

    # good
    "Some string is really long and " \
      "spans multiple lines."
    ```

## Regular Expressions

* <a name="regex-named-groups"></a>Avoid using `$1-9` as it can be hard to track
    what they contain. Named groups can be used instead.
    <sup>[[link](#regex-named-groups)]</sup>

    ```ruby
    # bad
    /(regexp)/ =~ string
    ...
    process $1

    # good
    /(?<meaningful_var>regexp)/ =~ string
    ...
    process meaningful_var
    ```

* <a name="caret-and-dollar-regexp"></a>Be careful with `^` and `$` as they
    match start/end of line, not string endings.  If you want to match the whole
    string use: `\A` and `\z`.<sup>[[link](#caret-and-dollar-regexp)]</sup>

    ```ruby
    string = "some injection\nusername"
    string[/^username$/]   # matches
    string[/\Ausername\z/] # don't match
    ```

* <a name="comment-regexes"></a>Use `x` modifier for complex regexps. This makes
    them more readable and you can add some useful comments. Just be careful as
    spaces are ignored.<sup>[[link](#comment-regexes)]</sup>

    ```ruby
    regexp = %r{
      start         # some text
      \s            # white space char
      (group)       # first group
      (?:alt1|alt2) # some alternation
      end
    }x
    ```

## Percent Literals

* <a name="percent-literal-delimiters"></a>Prefer parentheses over curly
    braces, brackets, or pipes when using `%`-literal delimiters for
    consistency, and because the behavior of `%`-literals is closer to method
    calls than the alternatives.<sup>[[link](#percent-literal-delimiters)]</sup>

    ```ruby
    # bad
    %w[date locale]
    %w{date locale}
    %w|date locale|

    # good
    %w(date locale)
    ```

* <a name="percent-w"></a>Use `%w` freely.<sup>[[link](#percent-w)]</sup>

    ```ruby
    STATES = %w(draft open closed)
    ```

* <a name="percent-parens"></a>Use `%()` for single-line strings which require
    both interpolation and embedded double-quotes. For multi-line strings,
    prefer heredocs.<sup>[[link](#percent-parens)]</sup>

    ```ruby
    # bad - no interpolation needed
    %(<div class="text">Some text</div>)
    # should be '<div class="text">Some text</div>'

    # bad - no double-quotes
    %(This is #{quality} style)
    # should be "This is #{quality} style"

    # bad - multiple lines
    %(<div>\n<span class="big">#{exclamation}</span>\n</div>)
    # should be a heredoc.

    # good - requires interpolation, has quotes, single line
    %(<tr><td class="name">#{name}</td>)
    ```

* <a name="percent-r"></a>Use `%r` only for regular expressions matching *more
    than* one '/' character.<sup>[[link](#percent-r)]</sup>

    ```ruby
    # bad
    %r(\s+)

    # still bad
    %r(^/(.*)$)
    # should be /^\/(.*)$/

    # good
    %r(^/blog/2011/(.*)$)
    ```

* <a name="percent-x"></a>Avoid the use of %x unless you're going to invoke a
    command with backquotes in it (which is rather unlikely).
    <sup>[[link](#percent-x)]</sup>

    ```ruby
    # bad
    date = %x(date)

    # good
    date = `date`
    echo = %x(echo `date`)
    ```

## Rails

* <a name="next-line-return"></a>When immediately returning after calling
    `render` or `redirect_to`, put `return` on the next line, not the same line.
    <sup>[[link](#next-line-return)]</sup>

    ```ruby
    # bad
    render :text => 'Howdy' and return

    # good
    render :text => 'Howdy'
    return

    # still bad
    render :text => 'Howdy' and return if foo.present?

    # good
    if foo.present?
      render :text => 'Howdy'
      return
    end
    ```

### Scopes
* <a name="scope-lambda"></a>When defining ActiveRecord model scopes, wrap the
    relation in a `lambda`.  A naked relation forces a database connection to be
    established at class load time (instance startup).
    <sup>[[link](#scope-lambda)]</sup>

    ```ruby
    # bad
    scope :foo, where(:bar => 1)

    # good
    scope :foo, -> { where(:bar => 1) }
    ```

## Be Consistent

> If you're editing code, take a few minutes to look at the code around you and
> determine its style. If they use spaces around all their arithmetic
> operators, you should too. If their comments have little boxes of hash marks
> around them, make your comments have little boxes of hash marks around them
> too.

> The point of having style guidelines is to have a common vocabulary of coding
> so people can concentrate on what you're saying rather than on how you're
> saying it. We present global style rules here so people know the vocabulary,
> but local style is also important. If code you add to a file looks
> drastically different from the existing code around it, it throws readers out
> of their rhythm when they go to read it. Avoid this.

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

## Translation

  Este guia também está disponível em outros idiomas:

  - ![cn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/China.png) **Chinese (Simplified)**: [1c7/ruby-airbnb](https://github.com/1c7/ruby-airbnb)
