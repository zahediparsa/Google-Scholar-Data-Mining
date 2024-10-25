# Iranian University Professors and Articles Data Analysis

This project involves collecting, processing, and analyzing data related to Iranian universities, their professors, and their published articles, sourced from Google Scholar. The aim is to filter and classify academic content based on specific criteria, using a large language model (LLM) for classification.

## Table of Contents

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
- [Feature Extraction](#feature-extraction)
  - [Breadth and Depth Calculation](#breadth-and-depth-calculation)

## Project Overview

This project focuses on scraping data (scrapping code can be found here https://github.com/Mmli081/Articles-analysis) related to Iranian universities and professors and their articles from Google Scholar. After the initial data collection, the data is filtered based on a set of criteria. Finally, the articles are classified into different subjects using an LLM model.

### Data Size

| Data Type    | Quantity     |
| ------------ | ------------ |
| Universities | 90           |
| Professors   | ~50,000      |
| Articles     | ~1.5 million |

## Data Structure

The project involves three main tables:

### University Table

| Column Name                 | Description                                                                 |
| --------------------------- | --------------------------------------------------------------------------- |
| university_name             | Name of the university.                                                     |
| town                        | City where the university is located.                                       |
| is_governmental             | Indicates if the university is government-funded (1 for yes, 0 for no).     |
| touch_with_10               | Number of subjects where the university has published more than 10 articles.*(Added later)* |
| depth_with_200              | Number of subjects where the university has published more than 200 articles.*(Added later)* |
| depth_with_uni_mean         | Number of subjects where the article count exceeds the university-specific average. *(Added later)* |
| depth_with_subject_mean     | Number of subjects where the article count exceeds the subject-specific average. *(Added later)* |

### Professor Table

| Column Name | Description                                        |
| ----------- | -------------------------------------------------- |
| id          | Unique identifier for the professor.               |
| name        | Name of the professor.                             |
| university  | University with which the professor is affiliated. |
| user_id     | Google Scholar ID of the professor.                |
| affiliation | Affiliation details of the professor.              |
| v_email_at  | Verified email domain.                             |
| cited_by    | Number of citations the professor has received.    |
| interests   | Research interests of the professor.               |
| h-index     | The h-index of the professor. *(Added later)*      |
| i10-index   | The i10-index of the professor. *(Added later)*    |

### Article Table

| Column Name  | Description                                        |
| ------------ | ---------------------------------------------------|
| title        | Title of the article.                              |
| GS_link      | Google Scholar link to the article.                |
| year         | Year of publication.                               |
| cite         | Number of citations the article has received.      |
| main_authors | Main authors of the article.                       |
| more_info    | Additional information related to the article.     |
| link_ids     | List of Google Scholar IDs of the authors.         |
|llama_subjects| titles classified using Llama3.1:8b *(Added later)*|

## Preprocessing Steps

### Step 0: Calculate h-index and i10-index

Before filtering, the `h-index` and `i10-index` are calculated for all professors to assess their academic impact.

### Step 1: Filter Universities

- **Exclude Non-Governmental Universities:** Remove all universities that are not government-funded.
- **Exclude Medical Universities:** Remove all universities that specialize in medical sciences.

### Step 2: Filter Professors

- **Remove Professors from Excluded Universities:** Any professor affiliated with universities removed in Step 1 is excluded.
- **Remove Professors with Less Than 100 Citations:** Professors with fewer than 100 citations are removed.

### Step 3: Filter Articles

- **Keep Articles from 2020 to 2022:** Only articles published between 2020 and 2022 are retained.
- **Remove Articles by Excluded Professors:** Any article authored by professors excluded in Step 2 is removed from the dataset.

### Data Size (after preprocessing)

| Data Type    | Quantity |
| ------------ | -------- |
| Universities | 66       |
| Professors   | ~15,000  |
| Articles     | ~230,000 |

## Article Classification

The remaining articles are classified into the following subjects using a large language model (Llama3.1:8b).

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
    <td>Veterinary</td>
  </tr>
  <tr>
    <td>Biochemistry, Genetics and Molecular Biology</td>
    <td>Chemistry</td>
    <td>Environmental Science</td>
  </tr>
  <tr>
    <td>Computer Science</td>
    <td>Decision Sciences</td>
    <td>Economics, Econometrics and Finance</td>
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
</table>

## Feature Extraction

### Breadth and Depth Calculation

For each university, the following metrics were calculated:

- **Breadth (touch_with_10):** This metric counts the number of subjects where the university has published more than 10 articles. It indicates how widely the university's research output is spread across different subjects.

- **Depth with University Mean (depth_with_uni_mean):** This metric counts the number of subjects where the university has published more articles than the calculated threshold specific to that university (based on the square root of the total number of articles from the university). It offers a relative measure of depth compared to the university's overall output.

- **Depth with Subject Mean (depth_with_subject_mean):** This metric counts the number of subjects where the university has published more articles than the calculated threshold specific to that subject (based on the square root of the total number of articles in that subject across all universities). It provides a relative measure of depth compared to the overall output in that subject.

- **Depth (depth_with_200):** This metric counts the number of subjects where the university has published more than 200 articles. It highlights the subjects where the university has significant research output, indicating areas of specialization.
