# Global Fashion Retail – Análise de Público-Alvo & Alinhamento de Campanhas de Desconto

Este repositório reúne todas as etapas de análise do **público-alvo** (clientes) e de validação das **campanhas de desconto**. O objetivo é verificar se as promoções estão alinhadas ao perfil real dos clientes de uma varejista global de moda e propor ajustes estratégicos.

---

## 1. Visão Geral dos Dados

### 1.1 `customers.csv`  
- **Tamanho**: 1 643 306 registros  
- **Colunas (9)**:  
  1. `Customer ID`  
  2. `Name`  
  3. `Email`  
  4. `Telephone`  
  5. `City`  
  6. `Country`  
  7. `Gender`  
  8. `Date Of Birth`  
  9. `Job Title` (≈ 36 % nulos)  

### 1.2 `discounts.csv`  
- **Tamanho**: 181 registros (campanhas)  
- **Colunas (6)**:  
  1. `Start` (data de início, formato YYYY-MM-DD)  
  2. `End` (data de término, formato YYYY-MM-DD)  
  3. `Discont` (profundidade do desconto, ex.: 0.25 = 25 %)  
  4. `Description` (texto livre)  
  5. `Category` (Feminine, Masculine, Children; ≈ 10 registros nulos)  
  6. `Sub Category` (ex.: “Dresses and Jumpsuits”, “Coats”, “T-shirts and Polos”; ≈ 10 nulos)  

---

## 2. Análise Demográfica dos Clientes

1. **Idade**  
   - Convertemos `Date Of Birth` para `datetime` e calculamos `Age = floor((hoje – Date Of Birth) / 365 dias)`.  
   - Criamos a coluna `Age Band` com as faixas: `< 18`, `18-24`, `25-34`, `35-44`, `45-54`, `55-64`, `65+`.  
   - **Distribuição (1,64 M total)**:  
     - `< 18`: 0,4 %  
     - `18-24`: **39,2 %**  
     - `25-34`: **24,9 %**  
     - `35-44`: 20,6 %  
     - `45-54`: 9,9 %  
     - `55-64`: 4,4 %  
     - `65+`: 0,9 %  
   - **Insight**: **65 %** da base está em `18-34` (Gen Z + Millennials). Idade média ≈ 31,5 anos (mediana 28).  

2. **Gênero**  
   - Mapeamos `Gender` para “M” (Masculino), “F” (Feminino) e “D” (Diverso/Outro).  
   - **Distribuição**:  
     - **M: 58,7 %** (≈ 964 562)  
     - **F: 41,2 %** (≈ 677 041)  
     - D ou ausente: 0,1 % (≈ 1 703)  

3. **País**  
   - Mais de 190 nacionalidades. *Top 7* concentram ≈ 100 %:  
     - 🇺🇸 Estados Unidos: 21,6 %  
     - 🇨🇳 China: 20,7 %  
     - 🇪🇸 Espanha: 14,5 %  
     - 🇩🇪 Alemanha: 12,5 %  
     - 🇫🇷 França: 12,0 %  
     - 🇬🇧 Reino Unido: 11,6 %  
     - 🇵🇹 Portugal: 7,2 %  

4. **Cidades (Top 10)**  
   - New York, Los Angeles, Shanghai, Beijing, Madrid, Barcelona, Berlin, Paris, London, Lisbon (≈ 15 % da base).  

5. **Profissão (`Job Title`)**  
   - **639 cargos** distintos; 36 % de registros nulos.  
   - **Top 5 mais frequentes** (≈ 5 % do total):  
     1. Museum/Gallery Exhibitions Officer  
     2. Social Worker  
     3. Chemical Engineer  
     4. Dentist  
     5. PHP Developer  
   - **Insight**: Alta heterogeneidade — não há um único segmento profissional dominante.

---

## 3. Scorecard Resumido do Público-Alvo

| Métrica                     | Valor                            |
|-----------------------------|----------------------------------|
| **Total de clientes**       | 1 643 306                        |
| **Faixa etária dominante**  | 18-24 (39,2 %)                   |
| **Gen Z + Millennials**     | 65 % (18-34 anos)                |
| **Idade média / mediana**   | 31,5 anos / 28 anos              |
| **Gênero**                  | M: 58,7 % • F: 41,2 % • D: 0,1 % |
| **Top 3 países**            | 🇺🇸 21,6 % • 🇨🇳 20,7 % • 🇪🇸 14,5 % |
| **Top 10 cidades**          | NY, LA, Shanghai, Beijing, etc.  |
| **% com Job Title preenchido** | 64 %                           |
| **Top 5 cargos**            | Distribuição dispersa            |

**Principais conclusões**  
- Público **jovem** (Gen Z/Millennials) → foco em mobile, tendências fast fashion, conteúdo digital.  
- Leve **viés masculino** (≈ 59 %), mas público feminino (41 %) ainda significativo.  
- Mercados‐âncora: **EUA + China** (≈ 42 % juntos); Europa Ocidental (Espanha, Alemanha, França, Reino Unido) com público ligeiramente mais maduro (25-44 anos).

---

## 4. Análise de Campanhas de Desconto

### 4.1 Panorama Geral  
- **Total de registros**: 181 campanhas (171 com `Category`/`Sub Category` populados).  
- **Período**: 01 jan 2020 a 31 mar 2025.  
- **Frequência**: ≈ 34 campanhas/ano; duração típica: 13–14 dias (mín 10, máx 17).

### 4.2 Segmentação por Categoria  
| Categoria   | Nº Campanhas | % Campanhas | Público-alvo demográfico (%) |
|-------------|-------------:|------------:|------------------------------|
| **Feminine**  |           64 |       37,4 % | Mulheres: 41,2 %             |
| **Masculine** |           54 |       31,6 % | Homens: 58,7 %               |
| **Children**  |           53 |       31,0 % | Pais (35-54 anos ≈ 30,5 %)   |

> **Insight de gap**  
> - *Masculine* está **sub-representado**: campanha 31,6 % vs 58,7 % da base masculina → gap de ≈ 27 pp.  
> - *Feminine* ligeiramente abaixo: 37,4 % vs 41,2 % → gap de ≈ 3,8 pp.  
> - *Children* alinhado (31 % vs ~30 % pais nas faixas etárias 35-54).

### 4.3 Profundidade de Desconto  
- **Valores praticados**:  
  - 20  % → 30 campanhas  
  - 25  % → 40 campanhas  
  - 35  % → 30 campanhas  
  - 40  % → 36 campanhas  
  - 45  % → 35 campanhas  
  - 50  % → 5 campanhas  
  - 60  % → 5 campanhas  
- **Média geral** ≈ 34 %.  
- **Por Categoria**:  
  - *Children*: 32 % (range 20 – 45 %)  
  - *Masculine*: 33 %  
  - *Feminine*: 34 %  

### 4.4 Sub-Categorias Principais (Top 5)  
| Sub Category                                         | Nº Campanhas |
|------------------------------------------------------|-------------:|
| Dresses and Jumpsuits                                |           16 |
| Girl and Boy (1–5 yrs, 6–14 yrs)                     |           16 |
| Coats and Blazers                                    |           12 |
| Sweaters and Knitwear                                |           11 |
| Sweaters and Sweatshirts                             |           11 |

> **Insight**:  
> - Foco maior em itens *Feminine* e *Children*.  
> - Sub-categorias masculinas (e.g. T-shirts, Shirts, Polos) aparecem menos, reforçando o gap no segmento masculino.

---

## 5. Gap Analysis: Campanhas × Público

| Segmento            | % no Público | % nas Campanhas | Gap    |
|---------------------|-------------:|----------------:|-------:|
| **Masculine (Homens)**   |       58,7 % |          31,6 % | –27,1 pp |
| **Feminine (Mulheres)**  |       41,2 % |          37,4 % | –3,8  pp |
| **Children (Pais 35-54)** |       30,5 %*|          31,0 % | +0,5  pp |

> *Estimado a partir das faixas 35-54 anos; assume pais como proxy.

- Não há segmentação explícita de `age_min`/`age_max` em `discounts.csv`. Sugerimos mapear cada campanha ao perfil demográfico do conjunto de clientes que efetivamente utilizou o cupom.  
- Recomenda-se incluir `Country` ou `Region` em futuras campanhas para avaliar ROI por mercado (EUA, China, Europa Ocidental).

---

## 6. Principais Recomendações

1. **Aumentar share de campanhas “Masculine”**  
   - Passar de 31,6 % → ≥ 50 % para alinhar-se aos 58,7 % de clientes homens.  
   - Priorizar sub-categorias masculinas (T-shirts, Shirts, Polos) com descontos ≥ 35 % (atualmente média é 33 %).

2. **Focar em “Feminine” high-potential**  
   - Manter ou ligeiramente elevar campanhas femininas (37,4 % → 41,2 %).  
   - Concentrar em *Dresses*, *Coats* em períodos sazonais (pré-verão, férias).  
   - Utilizar micro-influenciadores para engajar Gen Z feminino nas redes sociais.

3. **Otimização para “Children” & Pais (35-54)**  
   - Ajustar datas para volta às aulas e Dia das Crianças; manter canal digital+e-mail.  
   - Validar se o público-pai representa exatamente 30 % ou se há sobreposição com millennials.

4. **Segmentação por idade e canal**  
   - Coletar dados de “redeem” (quem usou cupom) e cruzar com `Age Band`, `Gender` e `Country`.  
   - Criar campanhas direcionadas:  
     - “Campanha 18-24” → conteúdo no TikTok/Reels (mobile-first).  
     - “Campanha 35-44” → e-mail/SMS, fidelidade (VIP cards).  

5. **Mensuração e A/B Tests**  
   - Adotar métricas por segmento:  
     - **Redemption Rate** (ordens / clientes targeted).  
     - **Revenue incremental** (pós-campanha).  
     - **Ticket Médio** vs faixa etária e gênero.  
   - Realizar testes de profundidade de desconto:  
     - Ex.: “Masculine 25 % vs 35 % vs 45 %” para avaliar elasticidade.


---

## 7. Próximos Passos e Extensões

1. **Enriquecer perfil de clientes**  
   - Incluir colunas de LTV, número de compras, ticket médio, canal preferido.  
   - Realizar clusterização (K-means) para criar personas comportamentais.  

2. **Campanhas Avançadas**  
   - Incluir coluna `Country` e `Age Min/Max` em `discounts.csv` para análise mais granular.  
   - Construir dashboards interativos (e.g. Plotly, Power BI) para monitorar performance em tempo real.  

3. **Modelagem de Propensão**  
   - Desenvolver modelo preditivo (logistic regression, XGBoost) para identificar clientes mais propensos a resgatar cada tipo de cupom.  
   - Automatizar geração de segmentos de alto ROI.  

---
