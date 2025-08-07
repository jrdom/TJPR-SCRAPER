# TJPR Scraper

Um scraper para coletar jurisprudências e baixar acórdãos em PDF do Tribunal de Justiça do Paraná (TJPR).

## Funcionalidades

- Busca jurisprudências por termo de pesquisa
- Filtra resultados por intervalo de datas de julgamento ou publicação
- Extrai metadados das decisões (processo, relator, órgão julgador, data, ementa)
- Baixa automaticamente os PDFs dos acórdãos encontrados
- Salva os resultados em um arquivo CSV

## Como usar

### Instalação

Certifique-se de ter Python 3.8+ instalado e instale as dependências:

```bash
pip install requests beautifulsoup4 pandas tqdm
```

### Exemplo básico

```python
from scraper_tjpr import TJPRScraper

# Instanciar o scraper (os PDFs serão salvos na pasta 'pdfs_tjpr')
scraper = TJPRScraper(download_dir="pdfs_tjpr")

# Executar pesquisa
df = scraper.cjsg(
    termo="IDPJ",
    paginas=5,  # Número de páginas a buscar
    data_julgamento_de="01/01/2025",  # Data inicial (DD/MM/AAAA)
    data_julgamento_ate="31/12/2025"  # Data final (DD/MM/AAAA)
)

# Salvar resultados em CSV
df.to_csv("jurisprudencia_tjpr.csv", index=False, encoding="utf-8-sig")
```

### Parâmetros da função `cjsg`

- `termo`: Termo de pesquisa (obrigatório)
- `paginas`: Número de páginas a buscar (padrão: 1)
- `data_julgamento_de`: Data inicial de julgamento (formato DD/MM/AAAA)
- `data_julgamento_ate`: Data final de julgamento (formato DD/MM/AAAA)
- `data_publicacao_de`: Data inicial de publicação (formato DD/MM/AAAA)
- `data_publicacao_ate`: Data final de publicação (formato DD/MM/AAAA)

## Estrutura de arquivos

- `pdfs_tjpr/`: Pasta onde os PDFs serão salvos (criada automaticamente)
- `jurisprudencia_tjpr.csv`: Arquivo CSV com os metadados das decisões

## Observações

- O scraper foi desenvolvido para fins educacionais e de pesquisa
- O código pode precisar de ajustes caso o site do TJPR sofra alterações

## Limitações

- Não implementa consulta a processos de 1º e 2º grau (apenas jurisprudência)
- Pode ser bloqueado se muitas requisições forem feitas em curto período
