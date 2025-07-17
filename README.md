# Pokédex
A **Pokédex** é uma aplicação web desenvolvida com Vue.js com TypeScript que permite aos usuários explorar e visualizar informações sobre diferentes pokémons. Através da integração com a [PokéAPI](https://pokeapi.co/), o sistema exibe uma lista paginada de criaturas com seus nomes e imagens e etc, simulando uma verdadeira enciclopédia Pokémon digital.

Com uma interface simples e interativa, a Pokédex possibilita:

- Visualização em tempo real de pokémons disponíveis na API

- Navegação entre páginas usando sistema de paginação

- Apresentação de informações dos pokémons de forma organizada

- Aprendizado prático sobre consumo de APIs, componentes Vue, e manipulação de dados assíncronos

Este projeto foi idealizado com fins educacionais, visando o desenvolvimento de habilidades em programação front-end, especialmente no uso de frameworks modernos e organização de código com componentes reutilizáveis.

## Configuração recomendada da IDE

[VSCode](https://code.visualstudio.com/) + [Vetur](https://marketplace.visualstudio.com/items?itemName=Vue.vetur) (e desative o Volar).

## Suporte a Tipagem para Imports de `.vue` em TypeScript

O TypeScript, por padrão, não consegue lidar com informações de tipo de arquivos `.vue` , então substituímos o CLI `tsc` pelo `vue-tsc` para verificação de tipos. Nos editores de código, precisamos do [Vetur](https://marketplace.visualstudio.com/items?itemName=Vue.vetur) to para que o serviço de linguagem do TypeScript reconheça os tipos dos arquivos `.vue`.

## Configuração do projeto

```sh
npm install
```

### Compilar e recarregar automaticamente durante o desenvolvimento

```sh
npm run dev
```

### Verificar tipos, compilar e minificar para produção

```sh
npm run build
```

### Verificar qualidade do código com ESLint

```sh
npm run lint
```
