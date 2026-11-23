# Simulador de preço de cursos

> Projeto inspirado em uma demanda real da minha carreira: a ausência de uma diretriz clara e fixa de custeio para cursos oferecidos aos públicos interno e externo. A ferramenta padroniza a precificação pela metodologia Cost Plus e define o ponto de equilíbrio do número de participantes, conforme a estrutura de custo × valor.

Ferramenta para calcular o custo e o preço de venda de cursos de suporte à vida (BLS, ACLS, PALS e similares) oferecidos por hospitais e centros de treinamento.

**Versão web (celular e navegador):** https://fabiano27.github.io/simulador-cursos/

## O que faz

- Cadastro de cursos, profissionais (valor/hora), insumos, custos indiretos, impostos/margem e públicos (externo, conveniado, interno).
- Simulação por turma: custo fixo, custo variável por aluno, custo por aluno, preço de venda, ponto de equilíbrio e resultado.
- Tabela de preços por público.
- Histórico de simulações salvas.

## Modelo de cálculo

- Custo por aluno = (custos fixos da turma + alunos × custo variável) ÷ alunos
- Método cost plus: preço = custo por aluno × (1 + markup) ÷ (1 − impostos)
- Ponto de equilíbrio = custos fixos ÷ (preço líquido de impostos − custo variável por aluno)
- A aba **Comparar propostas** (versão web) coloca propostas salvas lado a lado e destaca o melhor valor de cada indicador.

Exemplo (ACLS, 16h, 12 alunos, 3 médicos instrutores, 8% de impostos e 20% de markup): custo por aluno de R$ 973, preço de cerca de R$ 1.270 e equilíbrio em 10 alunos.

## Duas versões

| Versão | Pasta | Como usar |
|---|---|---|
| Python + HTML (SQLite) | `app/` | `python app/app.py` e abra `http://localhost:8000` |
| Web/celular (um único HTML) | `docs/` | Abra `docs/index.html` no navegador ou use o GitHub Pages |

A versão Python (sem os testes pré-carregados e sem a aba de comparação) usa só a biblioteca padrão (Python 3.8+) e grava os dados em `simulador.db`.
A versão web grava os dados no próprio aparelho (localStorage). Use a aba **Dados** para gerar e restaurar backup em texto.

## Testes pré-carregados (versão web)

A versão web já traz duas propostas salvas, visíveis na aba **Comparar propostas**. Os custos são exemplos.

| | Teste 01 | Teste 02 |
|---|---|---|
| Curso | Curta duração: BLS | Especialização em Obstetrícia |
| Carga horária / alunos | 8h / 15 | 360h / 25 |
| Custos fixos da turma | R$ 3.040 | R$ 81.000 |
| Custo variável por aluno | R$ 230 | R$ 1.150 |
| Custo por aluno | R$ 432,67 | R$ 4.390,00 |
| Markup (cost plus) | 30% | 20% |
| Preço de venda (externo) | R$ 602,54 | R$ 5.643,28 |
| Ponto de equilíbrio | 10 alunos | 20 alunos |
| Resultado da turma | R$ 1.947 | R$ 21.950 |

Impostos considerados (Belo Horizonte/MG, 2026, Lucro Presumido): ISS 3% (educação e treinamento, Lei 8.725/2003) + PIS 0,65% + Cofins 3% = 6,65% sobre o preço. IRPJ e CSLL ficam dentro do markup. Entidades filantrópicas podem ter tratamento diferente. Confirme alíquotas e enquadramento com a contabilidade e com a Prefeitura de Belo Horizonte.

Para recarregar os testes, use **Dados > Recarregar testes 01 e 02**.

## Publicar a versão web no GitHub Pages

1. No repositório, abra **Settings > Pages**.
2. Em **Source**, escolha **Deploy from a branch**, branch `main` e pasta `/docs`.
3. Salve. O endereço aparece na mesma tela em alguns minutos.

## Estrutura

```
simulador-cursos/
├── README.md
├── LICENSE
├── .gitignore
├── app/
│   └── app.py        # servidor Python + interface HTML + SQLite
└── docs/
    └── index.html    # versão web autônoma (GitHub Pages)
```

## Observações

- Os valores de exemplo são ilustrativos. Substitua pelos custos reais da sua instituição.
- Confirme com a contabilidade o tratamento tributário (ISS, filantropia, fundação de apoio).
- O custo de oportunidade dos profissionais assistenciais deve entrar no valor/hora.
- A versão Python aceita acessos apenas da própria máquina. Para uso em rede, acrescente autenticação.

## Licença

MIT. Veja o arquivo `LICENSE`.

## Autor

Fabiano Antunes Gomes (Fantunnes) · GitHub: [FABIANO27](https://github.com/FABIANO27)
