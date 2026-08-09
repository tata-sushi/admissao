# Admissão — Tatá Sushi

Processo de admissão em formato de conversa. O candidato responde as perguntas
e anexa os documentos pelo celular; ao final o RH recebe a ficha completa.

**No ar:** https://admissao.tatasushi.tech

## Como editar a conversa

Todo o roteiro está num único array chamado `ROTEIRO`, no topo do `<script>` do
`index.html`. Para mudar uma pergunta, a ordem dos passos ou os documentos
pedidos, basta mexer ali — o resto do código não precisa ser tocado.

Cada passo é um objeto. Os tipos disponíveis:

| Tipo | O que faz |
|---|---|
| `fala` | O bot só fala e segue sozinho |
| `texto` | Pergunta aberta, com máscara e validação opcionais |
| `opcoes` | Botões de resposta rápida |
| `upload` | Envio de documento (foto ou arquivo) |
| `revisao` | Mostra tudo que foi coletado, com botão de editar |
| `fim` | Cartão de conclusão com o protocolo |

Campos comuns a qualquer passo:

- `id` — identificador do passo (usado para voltar e editar)
- `grupo` — nome da etapa que aparece no painel lateral
- `condicao` — função que recebe os dados; se retornar `false`, o passo é pulado

Exemplo de um passo condicional:

```js
{ id:'linhas', tipo:'texto', grupo:'Endereço', campo:'linhas', rotulo:'Linhas',
  condicao: d => d.vale_transporte === 'sim',
  pergunta:'Quais conduções você usa até a unidade?',
  validar: v => v.trim().length >= 3 || 'Me conta pelo menos uma linha.' }
```

## Ver os dados coletados

O botão **Ver dados** (no rodapé do painel lateral) abre o JSON exato que o
aplicativo vai receber — dados do candidato e situação de cada documento. É por
esse formato que a integração com o back-end deve ser feita.

## Ainda não implementado

- **Nada é salvo.** Recarregar a página recomeça a conversa do zero.
- **Os arquivos não sobem para lugar nenhum** — ficam apenas na memória do
  navegador durante a sessão.
