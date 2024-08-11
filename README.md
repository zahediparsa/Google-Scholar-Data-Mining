# Iranian University Professors and Articles Data Analysis

This project involves the collection, processing, and analysis of data related to Iranian universities, their professors, and their published articles, primarily sourced from Google Scholar. The aim is to filter and classify academic content based on specific criteria, using a large language model (LLM) for classification.

## Table of Contents

- [Iranian University Professors and Articles Data Analysis](#iranian-university-professors-and-articles-data-analysis)
  - [Table of Contents](#table-of-contents)
  - [Project Overview](#project-overview)
    - [Data Size](#data-size)
  - [Data Structure](#data-structure)
    - [University Table](#university-table)
    - [Professor Table](#professor-table)
    - [Article Table](#article-table)
  - [Preprocessing Steps](#preprocessing-steps)
    - [Step 0: Calculate h-index and i10-index](#step-0-calculate-h-index-and-i10-index)
    - [Step 1: Filter Universities](#step-1-filter-universities)
    - [Step 2: Filter Professors](#step-2-filter-professors)
    - [Step 3: Filter Articles](#step-3-filter-articles)
    - [Data Size (after preprocessing)](#data-size-after-preprocessing)
  - [Article Classification](#article-classification)
    - [Subject Classification](#subject-classification)

## Project Overview

This project focuses on scraping data related to Iranian universities, professors, and their articles from Google Scholar. After the initial data collection, the data is filtered based on a set of criteria. Finally, the articles are classified into different subjects using an LLM model.

### Data Size

| Data Type   | Quantity  |
|-------------|-----------|
| Universities| 90        |
| Professors  | ~50,000   |
| Articles    | ~1.5 million |

## Data Structure

The project involves three main tables:

### University Table

| Column Name     | Description                                |
|-----------------|--------------------------------------------|
| university_name | Name of the university.                    |
| town            | City where the university is located.      |
| is_governmental  | is the university a subset of government universities? 1 or 0|

### Professor Table

| Column Name   | Description                                       |
|---------------|---------------------------------------------------|
| id            | Unique identifier for the professor.              |
| name          | Name of the professor.                            |
| university    | University with which the professor is affiliated.|
| user_id       | Google Scholar ID of the professor.               |
| affiliation   | Affiliation details of the professor.             |
| v_email_at    | Verified email domain.                            |
| cited_by      | Number of citations the professor has received.   |
| interests     | Research interests of the professor.              |
| h-index       | The h-index of the professor. *(Added later)*     |
| i10-index     | The i10-index of the professor. *(Added later)*   |

### Article Table

| Column Name | Description                                       |
|-------------|---------------------------------------------------|
| title       | Title of the article.                             |
| GS_link     | Google Scholar link to the article.               |
| year        | Year of publication.                              |
| cite        | Number of citations the article has received.     |
| main_authors| Main authors of the article.                      |
| more_info   | Additional information related to the article.    |
| link_ids    | List of Google Scholar IDs of the authors.        |

## Preprocessing Steps

### Step 0: Calculate h-index and i10-index

Before filtering, the `h-index` and `i10-index` are calculated for all professors to assess their academic impact.

### Step 1: Filter Universities

- **Exclude Non-Governmental Universities:** Remove all universities that are not government-funded.
- **Exclude Medical Universities:** Remove all universities that are specialized in medical sciences.

### Step 2: Filter Professors

- **Remove Professors from Excluded Universities:** Any professor affiliated with universities removed in Step 1 is excluded.
- **Remove Professors with Less Than 100 Citations:** Professors with fewer than 100 citations are removed.

### Step 3: Filter Articles

- **Keep Articles from 2020 to 2022:** Only articles published between 2020 and 2022 are retained.
- **Remove Articles by Excluded Professors:** Any article authored by professors excluded in Step 2 is removed from the dataset.

### Data Size (after preprocessing)

| Data Type   | Quantity  |
|-------------|-----------|
| Universities| 66        |
| Professors  | ~15,000   |
| Articles    | ~350,000  |

## Article Classification

The remaining articles are classified into folloing subjects using a large language model (Llama3.1:8b).

### Subject Classification

<table border="0">
  <tr>
    <td>Agricultural and Biological Sciences</td>
    <td>Business, Management and Accounting</td>
    <td>Energy</td>
  </tr>
  <tr>
    <td>Arts and Humanities</td>
    <td>Chemical Engineering</td>
    <td>Engineering</td>
  </tr>
  <tr>
    <td>Biochemistry, Genetics and Molecular Biology</td>
    <td>Chemistry</td>
    <td>Environmental Science</td>
  </tr>
  <tr>
    <td>Computer Science</td>
    <td>Decision Sciences</td>
    <td>Health Professions</td>
  </tr>
  <tr>
    <td>Dentistry</td>
    <td>Earth and Planetary Sciences</td>
    <td>Immunology and Microbiology</td>
  </tr>
  <tr>
    <td>Materials Science</td>
    <td>Mathematics</td>
    <td>Medicine</td>
  </tr>
  <tr>
    <td>Neuroscience</td>
    <td>Nursing</td>
    <td>Pharmacology, Toxicology and Pharmaceutics</td>
  </tr>
  <tr>
    <td>Physics and Astronomy</td>
    <td>Psychology</td>
    <td>Social Sciences</td>
  </tr>
  <tr>
    <td>Veterinary</td>
    <td>Economics, Econometrics and Finance</td>
    <td></td>
  </tr>
</table>
