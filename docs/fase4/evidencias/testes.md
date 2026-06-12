# Evidências de Testes

## 1. Ambiente

Os resultados correspondem ao commit `ba6db878b9dfa36fb034916612c4cf58ddf43475`, avaliado em 11/06/2026.

---

## 2. Backend TypeScript

Comando:

```bash
npm run test:coverage -- --runInBand
```

Resultado:

| Item | Valor |
| :--- | ----: |
| Suítes | 6 aprovadas |
| Testes | 45 aprovados |
| Statements | 19,67% |
| Branches | 10,55% |
| Functions | 26,03% |
| Lines | 20,11% |

<p align="center">Tabela 1 - Resultado dos testes Jest do backend. Fonte: Equipe Carol Shaw, 2026.</p>

---

## 3. Serviços Python

Comando:

```bash
python -m pytest -c pytest.ini
```

Resultado:

| Item | Valor |
| :--- | ----: |
| Testes coletados | 47 |
| Aprovados | 36 |
| Falhas esperadas (`xfail`) | 10 |
| Ignorados | 1 |
| Tempo | 24,02 s |

<p align="center">Tabela 2 - Resultado dos testes Pytest. Fonte: Equipe Carol Shaw, 2026.</p>

O `pytest.ini` aplica `--cov=.` dentro de `tests-python`. Assim, o relatório mede predominantemente os próprios arquivos de teste, e não os módulos de produção. Por essa razão, o percentual de cobertura Python não foi usado na avaliação.

---

## 4. Frontend Svelte

Comandos:

```bash
npm run test:unit -- --passWithNoTests
npm run check
```

Resultados:

- o frontend não possui arquivos de teste reconhecidos pelo Vitest;
- o comando terminou com sucesso somente porque `--passWithNoTests` estava habilitado;
- o `svelte-check` encontrou 10 erros e 3 avisos em 8 arquivos;
- entre os problemas estão variáveis públicas de ambiente não declaradas, parâmetros com tipo implícito e incompatibilidades de tipos em componentes.

---

## 5. Uso na Avaliação

Os resultados demonstram que existem testes no backend e nos serviços Python, mas não permitem calcular M3. A especificação do produto não fornece a quantidade de cenários de teste requeridos, que é o denominador obrigatório da métrica.

[Voltar para Manutenibilidade](../manutenibilidade.md)
