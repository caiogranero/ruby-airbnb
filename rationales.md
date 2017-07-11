# Rationales

Esse documento contém os motivos e justificativas das decisões expostas no guia de estilo principal [Style guide](./README.md).

## Índice
  1.  [Tamanho das linhas](#tamanho-das-linhas)

### Tamanho das linhas

Manter o visual do código compactado (forçando a limitação em 100 caracteres por linha) faz com que seja mais fácil de entender. Por exemplo, você não tem que avançar/voltar a tela para ver o que está acontecendo -- você pode ver tudo junto.

Aqui estão alguns exemplos da nossa base de dados de código que mostra algumas técnicas para diminuir complexidades do código em multiplas linhas, sendo que todas respeitam o limite de 100 caracteres. Algumas técnicas são: 

* Uso ilimitado de notações para continuação da linha, como: `(` `{` `[`
* Métodos encadeados, terminando métodos que não foram concluídos com `.`
* Criando grandes textos, colocando strings próximas a outras e separando com barra invertida para novas linhas.
* Quebra de longos blocos lógicos com quebra-de-linha após operadores como
  `&&` e `||`

```ruby
scope = Translation::Phrase.includes(:phrase_translations).
  joins(:phrase_screenshots).
  where(:phrase_screenshots => {
    :controller => controller_name,
    :action => JAROMIR_JAGR_SALUTE,
  })
```

```ruby
translation = FactoryGirl.create(
  :phrase_translation,
  :locale => :is,
  :phrase => phrase,
  :key => 'phone_number_not_revealed_time_zone',
  :value => 'Símanúmerið þitt verður ekki birt. Það er aðeins hægt að hringja á '\
            'milli 9:00 og 21:00 %{time_zone}.'
)
```

```ruby
if @reservation_alteration.checkin == @reservation.start_date &&
   @reservation_alteration.checkout == (@reservation.start_date + @reservation.nights)

  redirect_to_alteration @reservation_alteration
end
```

```erb
<% if @presenter.guest_visa_russia? %>
  <%= icon_tile_for(I18n.t("email.reservation_confirmed_guest.visa.details_header",
                           :default => "Visa for foreign Travelers"),
                    :beveled_big_icon => "stamp") do %>
    <%= I18n.t("email.reservation_confirmed_guest.visa.russia.details_copy",
               :default => "Foreign guests travelling to Russia may need to obtain a visa...") %>
  <% end %>
<% end %>
```

Os códigos acima são muito mais fáceis de ler do que os abaixo:

```ruby
scope = Translation::Phrase.includes(:phrase_translations).joins(:phrase_screenshots).where(:phrase_screenshots => { :controller => controller_name, :action => JAROMIR_JAGR_SALUTE })

translation = FactoryGirl.create(:phrase_translation, :locale => :is, :phrase => phrase, :key => 'phone_number_not_revealed_time_zone', :value => 'Símanúmerið þitt verður ekki birt. Það er aðeins hægt að hringja á milli 9:00 og 21:00 %{time_zone}.')

if @reservation_alteration.checkin == @reservation.start_date && @reservation_alteration.checkout == (@reservation.start_date + @reservation.nights)
  redirect_to_alteration @reservation_alteration
end
```

```erb
<% if @presenter.guest_visa_russia? %>
  <%= icon_tile_for(I18n.t("email.reservation_confirmed_guest.visa.details_header", :default => "Visa for foreign Travelers"), :beveled_big_icon => "stamp") do %>
    <%= I18n.t("email.reservation_confirmed_guest.visa.russia.details_copy", :default => "Foreign guests travelling to Russia may need to obtain a visa prior to...") %>
  <% end %>
<% end %>
```
