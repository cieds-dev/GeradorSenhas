# Ferramentas de Senha – CIEDS

Duas páginas HTML para uso interno da equipe de TI, que funcionam direto no navegador, **sem instalação, sem servidor e sem internet**. Todo o processamento acontece localmente na máquina do usuário: nada é enviado ou salvo em lugar nenhum.

## Ferramentas

| Arquivo | O que faz |
|---|---|
| `gerador-de-senhas.html` | Gera senhas aleatórias e complexas (tamanho, tipos de caractere e quantidade configuráveis). |
| `senha-por-regra.html` | Monta a senha de um portal a partir de uma base e de uma regra de substituição de vogais, para que a TI possa refazê-la quando necessário. |

## Estrutura do projeto

```
.
├── CIEDS.png                  # logo exibida no cabeçalho (mesma pasta dos HTMLs)
├── gerador-de-senhas.html
├── senha-por-regra.html
└── README.md
```

## Como usar

1. Baixe ou clone o repositório.
2. Mantenha os arquivos `.html` na mesma pasta do `CIEDS.png`.
3. Dê dois cliques no arquivo desejado para abrir no navegador (Chrome, Edge, Firefox etc.).

Se o `CIEDS.png` não estiver na pasta, as páginas funcionam normalmente, apenas sem o logo.

## Gerador de senhas aleatórias

- Tamanho de 8 a 64 caracteres.
- Opções: minúsculas, maiúsculas, números, símbolos e "evitar caracteres parecidos" (`l`, `I`, `1`, `O`, `0`).
- Gera de 1 a 20 senhas de uma vez, cada uma com botão **Copiar**.
- Garante pelo menos um caractere de cada tipo selecionado.
- Usa `crypto.getRandomValues`, o gerador aleatório criptograficamente seguro do navegador.

## Senha por regra

A senha é construída em três partes:

```
[base] + [símbolo] + [vogais da base trocadas por símbolos]
```

Regra padrão de substituição:

| Vogal | A | E | I | O | U |
|---|---|---|---|---|---|
| Símbolo | `!` | `@` | `#` | `(` | `&` |

Exemplo com a base `Producao@`:

- Vogais da base: o, u, a, o → `(`, `&`, `!`, `(`
- Senha gerada: `Producao@(&!(`

Comportamento:

- A base digitada no campo **Portal** é respeitada exatamente como está, incluindo maiúsculas e minúsculas.
- Se a base já termina com o símbolo configurado, ele não é repetido.
- Se for digitado um endereço (por exemplo `producao.com.br` ou `https://producao.com.br/login`), a ferramenta usa apenas o nome antes do primeiro ponto, sem alterar maiúsculas e minúsculas.
- A opção **Ajustar a regra** permite trocar o símbolo intermediário e o símbolo de cada vogal sem editar o código.
- Se a senha final tiver menos de 12 caracteres, a página exibe um aviso, pois alguns sistemas exigem tamanho mínimo maior.

## Considerações de segurança

A ferramenta **Senha por regra** é um método de memorização, não criptografia. Por isso:

- Quem descobrir a regra ou uma única senha consegue deduzir as demais.
- Substituições comuns de vogais por símbolos são facilmente testadas por programas de quebra de senha.
- A regra deve ser tratada como segredo e ficar restrita à equipe de TI. Se ela vazar, todas as senhas geradas por ela ficam comprometidas.
- Evite incluir a regra real ou senhas reais neste repositório.

Sempre que possível, prefira:

- Senhas aleatórias (ferramenta `gerador-de-senhas.html`) guardadas em um gerenciador de senhas compartilhado (Bitwarden, KeePass etc.).
- Verificação em duas etapas nos sistemas que a suportarem, principalmente em contas compartilhadas.

## Tecnologias

HTML, CSS e JavaScript puros, em arquivo único por ferramenta. Sem dependências externas.

## Licença

Uso interno. Defina aqui a licença do projeto, se aplicável.
