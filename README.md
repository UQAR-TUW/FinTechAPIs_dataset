# FinTechAPIs Dataset

The FinTechAPIs dataset is an expert-annotated dataset of finance API descriptions built from
open-source [OpenAPI](https://www.openapis.org/) documents extracted from public repositories.

## Description

The [`fintechapis.csv`](fintechapis.csv) **semicolon separated `.csv`** file comprises 6 columns:

- `filename`: Index of the dataset. References the original OpenAPI filename.
- `content`: The API description. All API descriptions are in this format:

  ```text
  TITLE: {title}
  DESCRIPTION:
      {description}
  ENDPOINTS:
      - {endpoint 1}
        {description/summary of endpoint 1}
      - {endpoint 2}
        {description/summary of endpoint 2}
      ...
  ```

- `junior`: Label attributed by the junior software engineer annotator.
- `senior`: Label attributed by the senior software engineer annotator.
- `expert`: Label attributed by the domain-expert annotator.
- `consensus`: The label of the API description determined by the *junior*, *senior*, and *expert* annotators. A majority vote
  approach is used to compute the *consensus* label. Therefore, for each document, at least two out of the three
  annotators must select the same label for it to be considered the *consensus* label. If no such majority is reached,
  the *consensus* label is `NO_CONSENSUS`.

## Label Distribution

Below are the labels and their distribution in the dataset, calculated from the `consensus` column.

| consensus     | count |
|:--------------|------:|
| banking       |    41 |
| payment       |    26 |
| loan-mortgage |    24 |
| user-password |    22 |
| client        |    21 |
| transfer      |    21 |
| currency      |    20 |
| savings       |    20 |
| trading       |    19 |
| blockchain    |    19 |
| other         |    10 |
| NO_CONSENSUS  |     6 |

There are **249** documents in this dataset.

## API Discovery Process

All original OpenAPI documents were either discovered on [APIs.guru](https://github.com/APIs-guru/openapi-directory)
or [SwaggerHub](https://app.swaggerhub.com/search). Then, with a custom extraction tool, specific sections of the
OpenAPI documents were extracted to produce API descriptions like the one presented in the [description](#description)
section, which are easier to read and more compact than OpenAPI descriptions.

## API Labelling Process

The labelling process was carried out using proprietary software. This software first allows the entire set of
documents to be divided into smaller, random batches. These batches are then distributed to
annotators, who use the application to label the documents. During this process, all categorized documents
are automatically uploaded to a GitHub repository, enabling the dataset administrator to collect the results and
extract the consensus among all annotators. To date, over 600 APIs were manually selected from public repositories
and more than 250 were labelled by the *junior*, *senior* and *expert* annotators.
