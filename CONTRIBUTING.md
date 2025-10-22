# Contributing to Constitutional Lock-in Index Project

Thank you for your interest in contributing to this research project! This document provides guidelines for contributing data, analysis, or methodological improvements.

---

## 🎯 Types of Contributions

### 1. **Additional Country Case Studies**

**Current coverage**: 10 countries (Argentina, Brazil, Germany, India, Spain, Chile, Mexico, Portugal, Greece, New Zealand)

**Expansion priorities**:
- Latin America: Colombia, Peru, Uruguay, Venezuela
- Europe: France, Poland, Hungary, Czech Republic
- Asia: South Korea, Japan, Taiwan, Philippines
- Africa: South Africa (already excellent CLI = 0.27, expand cases)

**Requirements for new country data**:
- Minimum 5 constitutional reform attempts (1991-2025)
- CLI component scores (0-1 scale for all 5 components)
- Primary source documentation (legislative records, court decisions)
- Reality Filter tags for all empirical claims

**How to contribute**:
1. Fork repository
2. Create directory: `data/[country_name]/`
3. Add files:
   - `reform_attempts.csv` (standardized format, see template)
   - `cli_components.csv` (component scores with justification)
   - `sources.md` (full bibliography with URLs when available)
4. Submit Pull Request with title: `feat: Add [Country] case studies`

---

### 2. **Alternative Statistical Specifications**

**Current model**: Logistic regression with McFadden R² = 0.74

**Potential improvements**:
- Mixed-effects models (country random effects)
- Time-series analysis (CLI evolution over time)
- Bayesian regression with informative priors
- Machine learning models (random forests, gradient boosting)
- Instrumental variables (address endogeneity concerns)

**How to contribute**:
1. Fork repository
2. Create new R/Python script in `code/alternative_models/`
3. Document model specification in comments
4. Compare with main results (Table 1 in paper)
5. Submit PR with title: `analysis: Alternative specification - [Model Name]`

---

### 3. **Methodology Refinements**

**Current protocols**:
- RootFinder (judicial precedent genealogy)
- Reality Filter (confidence tagging)
- CLI Coding Manual (component scoring)

**Potential improvements**:
- Inter-coder reliability testing (Krippendorff's α)
- Automated text analysis (NLP for judicial decisions)
- Network analysis for precedent evolution
- Fuzzy-set QCA as robustness check

**How to contribute**:
1. Fork repository
2. Create document in `methodology/improvements/`
3. Provide worked example on existing data
4. Submit PR with title: `methodology: [Improvement Description]`

---

### 4. **Data Quality Improvements**

**Help us verify existing data**:
- Check primary source citations (dead links?)
- Verify CLI component scores (coding errors?)
- Update reform outcome data (new legislative activity 2024-2025?)
- Correct typos or inconsistencies

**How to report issues**:
1. Open GitHub Issue with label: `data-quality`
2. Specify: Country, Case ID, Variable, Current Value, Correct Value
3. Provide primary source citation for correction
4. We will verify and update dataset

---

## 📋 Contribution Standards

### **Reality Filter Requirements**

All contributions must follow Reality Filter protocol:

| Tag | Description | Required Documentation |
|-----|-------------|------------------------|
| `[VERIFIED]` | Primary source directly accessed | Full citation with URL or archive location |
| `[PARAPHRASE]` | Reconstructed from secondary sources | Academic source citation |
| `[INFERENCE]` | Logical conclusion from premises | Explicit reasoning chain |
| `[ESTIMATION]` | Calculation based on verified data | Formula and data sources |
| `[CONJECTURE]` | Provisional hypothesis | Falsification criteria stated |

**Example**:
```markdown
❌ BAD: "Germany's CLI score is 0.41."

✅ GOOD: "Germany's CLI score is 0.41 [ESTIMATION: Formula = 0.25(0.35) + 0.25(0.40) + 
0.20(0.45) + 0.15(0.50) + 0.15(0.40), component scores from BVerfG case law analysis 
1990-2024, see data/germany/cli_components.csv]."
```

---

### **Data Format Standards**

#### Reform Attempts CSV Template

File: `data/[country]/reform_attempts.csv`

```csv
case_id,country,year,domain,reform_success,explicit_clause,cli_score,cli_text_vagueness,cli_judicial_activism,cli_treaty_hierarchy,cli_precedent_weight,cli_amendment_difficulty,reform_description,primary_source
DEU_LABOR_2003,Germany,2003,labor,1,1,0.41,0.35,0.40,0.45,0.50,0.40,"Hartz IV labor market reform","Bundestag Drucksache 15/1516"
```

**Column specifications**:
- `case_id`: Country code (ISO 3166-1 alpha-3) + domain + year
- `reform_success`: 1 = passed AND implemented, 0 = rejected OR blocked
- `explicit_clause`: 1 = constitutional text has entrenchment clause, 0 = no
- CLI scores: All float values 0.00-1.00 (two decimal places)
- `reform_description`: Max 200 characters
- `primary_source`: Full citation (legislative record, court decision, official gazette)

---

### **CLI Component Scoring Guidelines**

See full manual: [`methodology/CLI_Coding_Manual.md`](methodology/CLI_Coding_Manual.md)

**Quick reference**:

| Component | 0.0-0.3 (Low) | 0.4-0.6 (Medium) | 0.7-1.0 (High) |
|-----------|---------------|------------------|----------------|
| **Text Vagueness** | Precise rules | Mixed rules/principles | Abstract principles only |
| **Judicial Activism** | Textualist courts | Moderate balancing | Expansive rights creation |
| **Treaty Hierarchy** | Domestic supremacy | Treaty = Constitution | Treaty > Constitution |
| **Precedent Weight** | Advisory only | Persuasive authority | Binding stare decisis |
| **Amendment Difficulty** | Simple majority | Supermajority (60-66%) | Near-impossible (75%+) |

---

## 🔬 Quality Control Process

All contributions undergo peer review:

1. **Automated checks**:
   - CSV format validation
   - CLI formula consistency check
   - Primary source URL accessibility test

2. **Manual review**:
   - Verify primary sources (random sample 20%)
   - Check Reality Filter tag appropriateness
   - Assess inter-coder reliability (if multiple contributors)

3. **Integration**:
   - Merge into main branch
   - Update master dataset
   - Re-run statistical analysis
   - Update README with new results (if changed)

---

## 📝 Pull Request Checklist

Before submitting PR, ensure:

- [ ] All CSV files have correct column names and data types
- [ ] Primary sources cited for all `[VERIFIED]` claims
- [ ] Reality Filter tags present on empirical claims
- [ ] Code runs without errors (test with `Rscript code/test_integration.R`)
- [ ] Documentation updated (README, CODEBOOK, or METHODOLOGY as appropriate)
- [ ] No large binary files (use `.gitignore` to exclude PDFs/DOCX)
- [ ] Commit messages follow format: `type(scope): description`
  - Types: `feat`, `fix`, `docs`, `data`, `analysis`, `methodology`
  - Example: `feat(brazil): Add 5 new labor reform cases`

---

## 🤝 Code of Conduct

### Academic Integrity

- **No plagiarism**: All contributions must be your own work or properly cited
- **No fabrication**: All data must come from verifiable primary sources
- **Transparency**: Disclose any conflicts of interest (e.g., advocacy positions)

### Collaboration Principles

- **Respectful discourse**: Critique ideas, not people
- **Open science**: Share data and code openly (CC BY 4.0 license)
- **Credit**: Contributors will be acknowledged in papers and repository

### Authorship

**Significant contributions** (e.g., 5+ country case studies, major methodological innovation) may warrant co-authorship on future papers. We follow [ICMJE authorship criteria](http://www.icmje.org/recommendations/browse/roles-and-responsibilities/defining-the-role-of-authors-and-contributors.html):

1. Substantial contributions to conception/design OR acquisition/analysis/interpretation
2. Drafting OR revising critically for intellectual content
3. Final approval of version to be published
4. Agreement to be accountable for all aspects

**Minor contributions** (e.g., typo fixes, single case study) will be acknowledged in Acknowledgments section.

---

## 📧 Contact for Contribution Inquiries

**Project Maintainer**: Ignacio Adrian Lerer  
**Email**: adrian@lerer.com.ar  
**GitHub**: [@adrianlerer](https://github.com/adrianlerer)

**Typical response time**: 48-72 hours

---

## 🙏 Thank You!

This project aims to advance empirical constitutional law research through open collaboration. Your contributions help build a more rigorous and comprehensive understanding of institutional lock-in mechanisms.

**Together, we can operationalize Bidart Campos' intuition and test it against global evidence.**

---

**Last Updated**: October 21, 2025
